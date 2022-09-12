# 对象池

当你的 Rust 侧有一些大型的对象时，你可能不想让它在 Rust 和 Dart 之间反复复制。这是，对象池就派上用场了：你只需要在 Rust 和 Dart
之间传递一个 "对象句柄"（实际上只是几个整数），Rust 会把这个句柄转换为真实的对象。

安装：和 [cancelable tasks](cancelable_task.md) 一样，请查看文档。
