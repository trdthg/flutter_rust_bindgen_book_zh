# Vec and 数组

## `Vec<u8>`, `Vec<i8>`, ...

在 Dart 中，当你想表达一个长字节数组，例如大图片或一些二进制 blob，人们通常会使用 `Uint8List` 而不是
`List<int>`，因为前者的性能更好。

`flutter_rust_bridge` 也为你考虑到了这一点。当你使用到 `Vec<u8>`（或
`Vec<i8>`，`Vec<i32>`，等）时，它将被翻译成 `Uint8List` 或其它类似的结构。

## `Vec<T>`

当你使用 `Vec<T>`，并且 T 是 `u8`、`i8` 等以外的类型时，它将被转换成正常的 `List<T>`。

## `[T; N]`

由于 Dart 没有对静态大小的数组进行特殊处理，所以它也会被转换为 `List<T>`。

## 例子

```rust,noplayground
pub fn draw_tree(tree: Vec<TreeNode>) -> Vec<u8> { ... }
```

转换为：

```Dart
Future<Uint8List> drawTree({required List<TreeNode> tree});
```

注意：如果你对 `Future` 感兴趣，请看 [这里](async_dart.md).
