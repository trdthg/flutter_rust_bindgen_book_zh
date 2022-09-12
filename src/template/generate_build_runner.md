# 使用 `build_runner`

检查一下你的 `lib/bridge_generated.dart`，你会发现 `Platform` 的定义变为了：

```dart
@freezed
class Platform with _$Platform {
    const factory Platform.unknown() = Unknown;
    const factory Platform.android() = Android;
    const factory Platforn.ios() = Ios;
    const factory Platform.windows() = Windows;
    const factory Platform.unix() = Unix;
    const factory Platform.macOs(
        String field0,
    ) = MacOs;
    const factory Platform.wasm() = Wasm;
}
```

它不再是一个普通的枚举，而是带着一个具有变体的枚举类！现在代码不能通过编译，因为我们还缺少 [`freezed`] 库。[`freezed`]
库也是一个代码生成库，和我们目前为止遇到的有些相似，但是它生成的更多是 Dart 代码。所有的这些库都是在调用 `build_runner`
时进行代码生成的，即执行 `flutter pub run build_runner build` 时。

不管怎么说，为了使这段代码通过编译，我们需要做一些修改：

- 执行下面的代码，添加最新的 [`freezed`] 依赖：

```shell
flutter pub add -d build_runner
flutter pub add -d freezed
flutter pub add freezed_annotation
```

- 更新 `justfile` 文件，在 Rust 代码生成后运行 `build_runner`:

```diff
 gen:
     ..
     # Uncomment this line to invoke build_runner as well
-    # flutter pub run build_runner build
+    flutter pub run build_runner build
```

现在调用 `just` 会同时生成 Rust 绑定和 Dart 代码。

[`freezed`]: https://pub.dev/packages/freezed
