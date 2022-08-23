# 方法

支持带有方法的结构体。包括静态方法和非静态方法。

## 示例

```rust,noplayground
pub struct SumWith { pub x: u32 }

impl SumWith {
    pub fn sum(&self, y: u32) -> u32 { self.x + y }
    pub fn sum_static(x: u32, y: u32) -> u32 { x + y }
}
```

转换为

```Dart
class SumWith {
  final FlutterRustBridgeExampleSingleBlockTest bridge;
  final int x;

  SumWith({
    required this.bridge,
    required this.x,
  });

  Future<int> sum({required int y, dynamic hint}) => ..
  static Future<int> sum({required int x, required int y, dynamic hint}) => ..
}
```

注意：如果你对 `Future` 感兴趣，请看 [这里](async_dart.md).
