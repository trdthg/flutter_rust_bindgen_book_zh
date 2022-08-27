# `justfile`

这个文件定义了 [just] 命令的 "配方"，它们和 `make` 与 MakeFile 类似。[just] 使用 Rust 构建，并在传统的
Makefile 语法基础上改进，更好地支持条件语句、参数、跨平台兼容性等。

在某些设置中，通过 `brew install llvm` 安装不会使 LLVM 库对其他可执行文件可见，这会给 `ffigen` 带来了问题。
`flutter_rust_bridge_codegen` 使用它作为 C-to-Dart 代码生成器。

运行 `just` 默认会运行 `gen` 和 `lint` 任务。

## `just gen`

生成 Rust 绑定并把它们放到正确的文件夹。[Generating new code](generate.md)
这部分会详细介绍如何修改任务脚本以执行附加任务。

## `just lint`

运行 Dart 和 Rust 默认的 linter。

## `just clean`

运行 Flutter 和 Rust 默认的 clean 命令。通常在调试和 build 相关的问题时有用。

[just]: https://github.com/casey/just
