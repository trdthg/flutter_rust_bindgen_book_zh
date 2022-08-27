# `native/native.xcodeproj`

这是由 [`cargo-xcode`](https://lib.rs/crates/cargo-xcode) 生成的 Xcode 项目文件夹，用于生成 Rust
代码库。

iOS 和 MacOS 的根项目会把这个文件夹作为 _子项目_ 导入，并在 build 时依赖它。

为你的目标设备配置合适的 `cate-type` 非常重要的。确保你的 `Cargo.toml` 中有这几行：

```toml
[lib]
crate-type = ["lib", "cdylib", "staticlib"]
```

一些说明：

- `lib` 对于非库项目时必须的，例如 tests 和 benchmarks
- `staticlib` 对 iOS 是必须的
- `cdylib` 是用于其他平台
