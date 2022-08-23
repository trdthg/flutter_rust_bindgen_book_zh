# Zero copy

`ZeroCopyBuffer<Vec<u8>>` (以及与它类似的东西，比如 `ZeroCopyBuffer<Vec<i8>>`) 可以无需拷贝将数据从
Rust 发送到 Dart. 因此，可以节约拷贝数据的开销，如果你的数据很大（比如一张高分辨率图像），开销可能会很高。

## Example

```rust,noplayground
pub fn draw_tree(tree: Vec<TreeNode>) -> ZeroCopyBuffer<Vec<u8>> { ... }
```

转换为：

```Dart
Future<Uint8List> drawTree({required List<TreeNode> tree});
```

生成的 Dart 代码看起来和没有用 `ZeroCopyBuffer` 的几乎一样。但是它的内部实现已经改变，完全不需要内存拷贝！

注意：如果你对 `Future` 感兴趣，请看 [这里](async_dart.md).
