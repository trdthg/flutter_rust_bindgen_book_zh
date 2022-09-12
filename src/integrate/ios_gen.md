# 生成绑定

现在我们已经完成了大部分的工作，让我们来编译我们的 Rust 程序。如果你刚才创建了你的 crate，请继续 在 _$crate/src/api.rs_
处添加一个新文件，并将其内容替换为下面的代码片段或其他内容。

```rust,ignore
pub fn greet() -> String {
    "Hello from Rust! 🦀".into()
}
```

接着在 `$crate/src/lib.rs` 添加：

```diff
+mod api;
```

## 运行代码生成

在我们编译之前，我们需要先生成绑定。从项目根目录运行这些命令：

```bash
{{#include command.sh.txt}}
```

> **注意：** 每次修改 Rust 代码后都会使用到这些命令。

运行这个命令可以得到由 Rust 库导出的函数和类型的 C 头文件。我们需要确保它来保持符号不被剥离。
