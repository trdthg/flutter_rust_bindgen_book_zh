# 教程：Pure Dart

**注意**: 如果你想了解每一条具体命令，
[CI workflow](https://github.com/fzyzcjy/flutter_rust_bridge/blob/master/.github/workflows/test.yaml)
中的 `valgrind_test` 部分也是有用的。

和之前的教程不一样，这个教程里 Rust 只和 Dart 本身集成，没有 Flutter.

## 拿到示例代码

请 [下载 Dart](https://dart.dev/get-dart),
[下载 Rust](https://www.rust-lang.org/learn/get-started),并熟悉一下。接着运行
`git clone https://github.com/fzyzcjy/flutter_rust_bridge`, 例子在
`frb_example/pure_dart`.

## (可选) 手动运行代码生成

注意：代码会在运行完 `cargo build` 后，通过 _build.rs_
里的构建脚本自动生成。所以这一步是可选的。即使你再次运行，代码也不会发生什么改变。

安装代码生成器：`cargo install flutter_rust_bridge_codegen`.

运行：
`flutter_rust_bridge_codegen --rust-input frb_example/pure_dart/rust/src/api.rs --dart-output frb_example/pure_dart/dart/lib/bridge_generated.dart`
(你可以将
[CI workflow](https://github.com/fzyzcjy/flutter_rust_bridge/blob/master/.github/workflows/codegen.yml)
最为查阅手册.) (对 Windows 用户，你可能需要在路径里用 `\\` 代替 `/`.)

## Run "Dart+Rust" app

你可以将 `frb_example/pure_dart/dart/lib/main.dart` 作为一个普通的 Dart 程序运行，唯一不同的是，你需要提供
Rust 的动态连接库 (简单起见，这里我只演示动态链接库的方法，但你当然可以使用其他方法）详细步骤如下。

在 `frb_example/pure_dart/rust` 目录下运行 `cargo build` 将 Rust 代码编译为 `.so` 文件。接着执行
`dart frb_example/pure_dart/dart/lib/main.dart frb_example/pure_dart/rust/target/debug/libflutter_rust_bridge_example.so`
去运行 Dart 程序。

(如果你的运行出现问题，请看 "Troubleshooting" 部分) (如果你的平台是 MacOS, Rust 应该会生成`.dylib`, 请把命令里的
`...dylib` 替换为 `...so`)

P.S. 这个例子里并没有 UI 或其他功能，你只能看到一些测试通过的信息。
