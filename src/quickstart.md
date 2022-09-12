# 快速开始

像平常一样编写你的 Rust 函数和类型定义。

```rust,ignore
// 一个普通的 Rust 函数 ...
pub fn draw_tree(root: TreeNode, mode: DrawMode) -> Result<Vec<u8>> { /* ... */ }

// ... 和一些丰富的类型
pub struct TreeNode { pub value: String, pub children: Vec<MyTreeNode> }
pub enum DrawMode { Colorful {palette: String}, Grayscale }
```

安装代码生成器 `flutter_rust_bridge_codegen`:

```bash
cargo install flutter_rust_bridge_codegen
# 或者使用 cargo-binstall
cargo binstall flutter_rust_bridge_codegen
# 或者使用 scoop (Windows)
scoop bucket add frb https://github.com/Desdaemon/scoop-repo
scoop install flutter_rust_bridge_codegen
# 或者使用 Homebrew
brew install desdaemon/repo/flutter_rust_bridge_codegen
```

<small>(感谢 @Desdaemon 将脚本发布到 brew/scoop)</small>

接着运行代码生成。

<small>注意：安装需要一些步骤。你可以查看 [教程](tutorial_with_flutter.md), [从模板创建项目](template.md)
或者 [与现有项目集成](integrate.md) 等章节获取更多信息.</small>

```bash
flutter_rust_bridge_codegen --rust-input path/to/api.rs \
                            --dart-output path/to/bridge_generated.dart
```

绑定代码生成之后，你可以在 Flutter/Dart 中无缝使用：

```dart
api.drawTree(TreeNode(value: "root", ...), Colorful(palette: "viridis"));
```

> 译者注：如果你在代码生成时遇到了这个错误 `fatal error: 'stdbool.h' file not found`
> 可以尝试阅读：[dart-lang/ffigen/issues/257](https://github.com/dart-lang/ffigen/issues/257#issuecomment-1061788936)
