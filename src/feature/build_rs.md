# 在 `build.rs` 中运行

执行代码生成器有两种方法。第一种也是最明显的方法是直接在命令行中执行 `flutter_rust_bridge`。

另一种方法时集成到 `build.rs` 里。通过这种方法，代码生成器会在编译 Rust 项目时自动触发。更多信息请看
[build.rs](https://github.com/fzyzcjy/flutter_rust_bridge/blob/master/frb_example/pure_dart/rust/build.rs)
文件。
