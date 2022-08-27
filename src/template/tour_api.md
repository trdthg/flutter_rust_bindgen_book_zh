# `native/src/api.rs`

这是库默认入口文件，只有定义在这里的函数才能进行代码生成。函数可以引用定义在其他文件中的类型，作为参数或者返回值类型。但是这些类型必须通过 `pub use`
导入，以便它们在 `native/src/bridge_generated.rs` 中可见。

只有定义在当前 crate 的类型有资格进行代码生成。

除此之外，结构和枚举的字段也需要符合上述条件。

要查看目前符合条件的函数和类型，请看
[示例文件](https://github.com/fzyzcjy/flutter_rust_bridge/blob/master/frb_example/pure_dart/rust/src/api.rs).
