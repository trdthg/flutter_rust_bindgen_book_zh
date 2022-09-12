# 设计总览

> 这篇文档正在编写中。Tracking issue:
> https://github.com/fzyzcjy/flutter_rust_bridge/issues/593

## 文件结构

- `frb_codegen`: 代码生成器。它接收 `api.rs` 作为输入，并输出 Rust and Dart 代码文件。
- `frb_example`: 例子。
  - `pure_dart`: 不只是一个例子，更重要的是作为端到端的测试。
  - `with_flutter`: 集成到 Flutter 的例子。
  - `pure_dart_multi`: 展示多文件的使用。
- `frb_dart`: 对 Dart 库的支持 - 需要由用户引入。
- `frb_rust`: 对 Rust 库的支持 - 需要由用户引入。
- `frb_macros`: `frb_rust` 独立的一部分。<small> 由于 proc macro 的限制，所以它是一个独立的
  crate。</small>
- `book`: 文档。
- `.github`: GitHub 相关。
  - `workflows/ci.yaml`: CI 工作流的定义。

## 代码生成结构

流程如下：

```
----------    src/parser    ----------    src/generator     ---------------
| api.rs | ---------------> | src/ir | -------------------> | Rust & Dart |
----------                  ----------                      ---------------
```

- 输入 (即图中的 `api.rs`), 是由用户提供的手工编写的 Rust 代码。
- 解析器 (`src/parser`) 将输入的代码 (其实是 [syn](https://crates.io/crates/syn) 树) 转换为 IR.
- IR (`src/ir`), 或者说 internal representation, 是一种结构，用来表示我们感兴趣的代码的信息。
- 生成器 (`src/generator`) 将 IR 转换为最终的输出。更具体一点就是 `src/generator/dart` 生成 Dart 代码，
  `src/generator/rust` 生成 Rust 代码，`src/generator/c` 生成 (部分) C 代码。
- 最终的输出 (图中的 `Rust & Dart`) 被写入到对应的文件。

## 数据流

> 建议读者配合着 IDE 的代码跳转功能一同查看

让我们看一下当调用一个函数时发生了什么。

假设用户调用了一个（生成的）名为 `func` 的 Dart 函数 `func({required String str})`。下面是详细的调用过程：

1. 生成的 Dart 函数，`func({required String str})`, 首先会将参数类型进行转换，将 "_Dart api data_"
   (即用户提供的数据) 转换为 "_Dart wire data_" (即真正在 Dart 和 Rust 间传递的数据)。再具体一点，它会调用
   `_api2wire_String(str)` 并得到一个指针 `ffi.Pointer<wire_uint_8_list>` (因为 `String`
   类型在底层使用 `pub struct wire_uint_8_list { ptr: *mut u8, len: i32 }`) 表示。
2. 接着可以用拿到的底层数据结构 `wire_uint_8_list` 调用 Dart 版本的 `wire_func`。在此之前，我们已经使用代码生成器生成了
   Rust 的 `wire_func` 函数，并使用 `cbindgen` 生成对应的 C 函数，使用 `ffigen` 得到对应的 Dart
   函数。在这里，我们调用 Dart 版本的 `wire_func`。注意，因为我们使用的是和 C
   语言兼容的函数，所以我们只能传递类似于指针的低级数据类型，而不是高级的安全的数据类型。
3. 当 Rust 版的 `wire_func` 被调用时，也会对参数类型进行转换。即使用 `.wire2api()` 将 "_Rust wire data_"
   (`wire_uint_8_list`，在 Dart 和 Rust 间传递的数据) 转换为 "_Rust api data_" (在这里就是
   `String`, 用户真正使用的数据).
4. 携带着转换后的 "_Rust api data_" 调用 `FLUTTER_RUST_BRIDGE_HANDLER`。handler
   是用户自定义的，所以用户可以提供他们自己的实现，而不是使用默认的线程池等。默认情况下，我们的 Handler 使用一个线程池，并在里面调用
   `api.rs` 中定义的由用户编写的 Rust 函数
5. 调用用户编写的 `fn func(str: String) -> String { ... }`，并得到返回值。
6. 返回值类型是一个 `String`，它会被传递到 Dart 侧。这是通过 Dart 提供的 API
   实现的。[`Dart_PostCObject`](https://github.com/dart-lang/sdk/blob/fd0d3b254690007d0ebc84175f30fa7d7491ec3e/runtime/include/dart_native_api.h#L124)，这个项目允许我们提供
   C 的结构体，并自动转换到 Dart 的数据。我们使用了一个 Rust 安全的 wrapper `allo-isolate` 去通信，因为它允许 Dart
   代码可以是异步的而不是同步。
7. 现在让我们回到 Dart 一侧，你应该会接收到一些 Dart 对象（其实就是 "_Dart wire data_"）。接着我们会使用一些类似于
   `_wire2api_SomeType` 的函数将它们转换为最终的 "_Dart api data_"。注意，这里提到的 "wire2api" 只定义在
   Dart 一侧，它的作用就是将 "_Dart_ wire data" 转换为 "_Dart_ api data"，和之前定义在 Rust
   中的不一样。举个例子，由于 `Dart_PostCObject` 并没有提供构建任意的结构体（类）的方法，我们必须将 Rust
   结构体中的所有字段作为一个列表传递，并使用 `wire2api` 转换为对应的 Dart 类。
8. 最终的结果会以 Dart 函数的返回值出现，即用户刚开始调用的 `func` 函数。到此为止，函数调用的整个过程就结束了！

## 内存安全

如何保障内存安全？这个具体需要具体问题具体分析。例如，假设我们想看一个 `String` 是如何从 Dart 传递给 Rust 的。那么我们需要关注的是
Dart 的 `_api2wire_String` 和 Rust 的 `.wire2api()`。

实际上 `String` 是通过委派给 `Vec<u8>` 生成的，所以我们需要检查和 String 和 `Vec<u8>` 相关
的代码。经过一系列跳转，你会看到下面的代码：

```dart
ffi.Pointer<wire_uint_8_list> _api2wire_String(String raw) {
  return _api2wire_uint_8_list(utf8.encoder.convert(raw));
}

ffi.Pointer<wire_uint_8_list> _api2wire_uint_8_list(Uint8List raw) {
  final ans = inner.new_uint_8_list_0(raw.length);
  ans.ref.ptr.asTypedList(raw.length).setAll(0, raw);
  return ans;
}
```

以及

```rust,noplayground
impl Wire2Api<Vec<u8>> for *mut wire_uint_8_list {
    fn wire2api(self) -> Vec<u8> {
        unsafe {
            let wrap = support::box_from_leak_ptr(self);
            support::vec_from_leak_ptr(wrap.ptr, wrap.len)
        }
    }
}

impl Wire2Api<String> for *mut wire_uint_8_list {
    fn wire2api(self) -> String {
        let vec: Vec<u8> = self.wire2api();
        String::from_utf8_lossy(&vec).into_owned()
    }
}

pub struct wire_uint_8_list {
    ptr: *mut u8,
    len: i32,
}
```

换句话说，String（或者 `Vec<u8>`）被转换为了一个原始结构体，它带有指针和长度字段。对内存的操作非常小心，因此不会造成泄漏或重复释放。

我们同时还使用了 Valgrind 进行检查，我本人已经在生产环境中使用它，并没有发现任何问题，所以不用担心内存问题。

## 想了解更多？请告诉我

你还想了解哪些方面？请在 Github 上创建一个 Issue，我会告诉你更多 :)
