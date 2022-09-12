# 并发

多个 Rust 函数能够同时运行，并且是并发的运行。因为我们默认会使用一个线程池去执行 Rust
代码。但是，你可以完全自定义这里的行为（甚至是完全舍弃线程池）。

## 示例

看一下下面的例子：

```rust,noplayground
pub fn compute() {
  thread::sleep(Duration::from_millis(1000));
}
```

下面的 Dart 代码使用了它：

```dart
var a = compute();
var b = compute();
var c = compute();
await Future.wait([a, b, c]); // 你可能需要提前学习 Dart 中的 `Future` and `async` 读懂这行代码
```

总体运行时间是 1s 而不是 3s，因为多个 `compute` 函数是并发执行的。
