# 创建一个新的 crate

首先，你需要在项目文件夹里创建一个新的 Rust crate，运行 `cargo new --lib`。建议将 crate
的根目录设为和其他项目同等级别，这样有助于简化配置过程。

```
├── android
├── ios
├── lib
├── linux
├── macos
├── $crate
│   ├── Cargo.toml
│   └── src
├── test
├── web
└── windows
```

这部分中我们会把你的 crate 称为 `$crate`。除非有其他说明，crate 文件夹和 crate 名称意义相同。

接着，在你的 `Cargo.toml` 加上这两行：

```diff
+[lib]
+crate-type = ["staticlib", "cdylib"]
```

这两个行配置会让你的 crate 在 MacOS 和 iOS 上构建为一个静态库。在其他平台上则是动态库。根据你的需要进行配置。如果你
需要编写单元测试或基准测试，也可以把 `"rlib"` 加进去。
