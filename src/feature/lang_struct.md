# 结构体

一般的 Rust 结构体都是支持的，你甚至能够使用递归字段，比如：

```rust,noplayground
pub struct TreeNode {
    pub value: String,
    pub children: Vec<MyTreeNode>,
    pub parent: Box<MyTreeNode>
}
```

如果一个结构体的字段是一个结构体或者枚举，请为它加上一层 `Box`, 否则会导致编译时错误。例如 `struct A {b: B}` 应该使用
`struct A {b: Box<B>}` 代替。

## 元组结构体

元组结构体 `struct Foo(A, B)` 会被翻译为 `class Foo { A field0; B field1; }`, 因为 Dart
没有匿名字段。

## Non-final 字段

在结构体字段上添加 `#[(non_final)]`, Dart 中对应的字段就会是 non-final 的。默认情况下，所有生成的字段都被设为
final，因为 Rust 默认情况下是不可变的。

## Dart 元数据注释

你可以使用 `frb` 宏中的 `dart_metadata` 参数添加 dart 元数据注解。

> TODO! You can add dart metadata annotations using `dart_metadata` parameter in
> `frb` macro.

- 对于那些被 dart 提前引入的注解（例如 `@deprecated`）,只需将注解作为一个 Rust 字面量。
  > TODO! For annotations that are prelude by dart (e.g. `@deprecated`), just
  > put annotation as a Rust literal.

- 如果你需要使用到 import, 把 import 部分的代码追加到注解字面量之后。当前支持两种 import 格式：
  - `import 'somepackage'`
  - `import 'somepackage' as somename`, `somename` 部分会成为注解的前缀
- 多个注解间使用 `,` 分割

具体的例子如下。

## `freezed` Dart classes

如果你想让生成的 Dart 类是 [`freezed`](https://pub.dev/packages/freezed)的（类似于 Kotlin 中的
data-classes），只需要在结构体前添加 `#[frb(dart_metadata=("freezed"))]`，它会为你生成需要的东西。

## 示例

### Example 1: 递归字段

```rust,noplayground
pub struct MyTreeNode {
    pub value: Vec<u8>,
    pub children: Vec<MyTreeNode>,
}
```

转换为：

```Dart
class MyTreeNode {
  final Uint8List value;
  final List<MyTreeNode> children;
  MyTreeNode({required this.value, required this.children});
}
```

注意：如果你想了解 `Future` , 看看这里 [async_dart](async_dart.md).

### Example 2: Metadata

```rust,noplayground
#[frb(dart_metadata=("freezed", "immutable" import "package:meta/meta.dart" as meta))]
pub struct UserId {
    pub value: u32,
}
```

转换为：

```dart
import 'package:meta/meta.dart' as meta;

@freezed
@meta.immutable
class UserId with _$UserId {
  const factory UserId({
    required int value,
  }) = _UserId;
}
```
