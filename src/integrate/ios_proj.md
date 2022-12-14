# 创建 Rust 项目

首先，请按照 [Usage](https://gitlab.com/kornelski/cargo-xcode#usage) 中 `cargo-xcode`
部分的说明进行操作。下面的内容就是从那里引用的，但请注意，它可能已经过时了。

---

确保你的 `$crate/Cargo.toml` 里有下面几行代码：

```toml
[lib]
crate-type = ["lib", "staticlib", "cdylib"]
```

一些说明

- `lib` 对于非库项目时必须的，例如 tests 和 benchmarks
- `staticlib` 对 iOS 是必须的
- `cdylib` 是用于其他平台

请按照您的需求进行配置。接着在 `$crate` 下运行：

```bash
cargo xcode
```

这行命令会生成一个 `$crate/$crate.xcodeproj`，可以导入到其他 Xcode 项目。你只需要为每个 crate
做一次这样的工作。先不要打开这个项目 我们需要先通过父项目对其进行配置。
