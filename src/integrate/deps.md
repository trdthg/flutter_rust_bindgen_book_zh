# 安装依赖

下一步，我们需要安装一些构建时和运行时依赖。

## 构建依赖

这些依赖只在 build 时需要：

- [`flutter_rust_bridge_codegen`](https://lib.rs/crates/flutter_rust_bridge_codegen),
  生成 Rust-Dart 胶水代码的核心
- [`ffigen`](https://pub.dev/packages/ffigen), 从 C 头文件中生成 Dart 代码
- 安装 LLVM, 请看
  [Installing LLVM](https://pub.dev/packages/ffigen#installing-llvm), `ffigen`
  会使用到
- (可选) [`cargo-xcode`](https://lib.rs/crates/cargo-xcode),如果你想生成为 IOS 和 MacOS 的
  Xcode 项目

安装这些依赖的简单方法：

- dart 项目

  ```bash
  cargo install flutter_rust_bridge_codegen
  dart pub add --dev ffigen && dart pub add ffi
  # if building for iOS or MacOS
  cargo install cargo-xcode
  ```

- flutter 项目

  ```bash
  cargo install flutter_rust_bridge_codegen
  flutter pub add --dev ffigen && flutter pub add ffi
  # if building for iOS or MacOS
  cargo install cargo-xcode
  ```

另外，这些依赖也可能已经提供了预构建的二进制版本。请自行到包管理器中查找。

## Dart 依赖

在 Dart 这里，`flutter_rust_bridge` 是 `flutter_rust_bridge_codegen` 必需的运行时组件。如果你打算在
Dart 中使用 Rust 的 enum struct，你需要这些依赖：

- `build_runner` (dev)
- `freezed` (dev)
- `freezed_annotation`

它们的是使用方法在 [Using `build_runner`](../generate/build_runner.md)。

```bash
flutter pub add flutter_rust_bridge
# if using Dart codegen
flutter pub add -d build_runner
flutter pub add -d freezed
flutter pub add freezed_annotation
```

## Rust 依赖

和 Dart 类似，Rust 需要 `flutter_rust_bridge` 最为运行时依赖。

在 `Cargo.toml` 里添加：

```diff
+[dependencies]
+flutter_rust_bridge = "1"
```
