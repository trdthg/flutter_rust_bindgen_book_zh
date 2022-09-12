# 枚举

众所周知，Rust 的 `enum` 功能强大，而且表达力强 - 它允许每一个枚举的变体关联不同的数据。Dart 没有内置这种枚举，但是不用担心 - 我们会使用
Dart 中的 `freezed` 库自动翻译为等价的结构。第一眼看上去，`freezed` 的语法可能看上去很奇怪，但是请阅读一下
[它的文档](https://pub.dev/packages/freezed), 看看它的强大之处。

## 示例

```rust,noplayground
pub enum KitchenSink {
    Empty,
    Primitives {
        /// Dart field comment
        int32: i32,
        float64: f64,
        boolean: bool,
    },
    Nested(Box<KitchenSink>),
    Optional(
        /// Comment on anonymous field
        Option<i32>,
        Option<i32>,
    ),
    Buffer(ZeroCopyBuffer<Vec<u8>>),
    Enums(Weekdays),
}
```

转换为：

```Dart
@freezed
class KitchenSink with _$KitchenSink {
  /// Comment on variant
  const factory KitchenSink.empty() = Empty;
  const factory KitchenSink.primitives({
    /// Dart field comment
    required int int32,
    required double float64,
    required bool boolean,
  }) = Primitives;
  const factory KitchenSink.nested(
    KitchenSink field0,
  ) = Nested;
  const factory KitchenSink.optional([
    /// Comment on anonymous field
    int? field0,
    int? field1,
  ]) = Optional;
  const factory KitchenSink.buffer(
    Uint8List field0,
  ) = Buffer;
  const factory KitchenSink.enums(
    Weekdays field0,
  ) = Enums;
}
```

它们由 freezed 中的 [all functionalities](https://pub.dev/packages/freezed) 驱动。
