# Option

Dart 对于可能为空的字段有特殊的语法 - `?`，我们会自动把 `Option` 翻译为 `?`。你可以查看
[官方文档](https://dart.dev/null-safety) 了解更多。

此外，`flutter_rust_bridge` 也能够处理 Dart 中的 `required` 关键字：如果一个参数不能为空，它就会被标记为
`required`，同时你必须提供一个值。如果它可以为空，那就不需要 `required`，Dart 的惯例是默认为 null。

## 示例

```rust,noplayground
pub struct Element {
    pub tag: Option<String>,
    pub text: Option<String>,
    pub attributes: Option<Vec<Attribute>>,
    pub children: Option<Vec<Element>>,
}

pub fn parse(mode: String, document: Option<String>) -> Option<Element> { ... }
```

转换为：

```Dart
Future<Element?> handleOptionalStruct({required String mode, String? document});

class Element {
  final String? tag;
  final String? text;
  final List<Attribute>? attributes;
  final List<Element>? children;
  Element({this.tag, this.text, this.attributes, this.children});
}
```

注意：如果你对 `Future` 感兴趣，请看 [这里](async_dart.md).
