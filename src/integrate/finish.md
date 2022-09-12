# 收尾工作

恭喜！您已经成功地将 Rust 组件通过 `flutter_rust_bridge` 添加到您的 Flutter 程序中，并配置了
`flutter run` 来构建您的 Rust 库并将其链接到程序中。

作为提醒，每次 Rust 代码改变时，以及在你运行`flutter run`之前，你都需要运行这些命令。

```bash
{{#include command.sh.txt}}
# if using Dart codegen
flutter pub run build_runner build
```

## 重命名 Rust bridge 模块

如果你想用 `flutter_rust_bridge_codegen` 的 `--rust-output` 参数，不要忘记更新
`$crate/src/lib.rs` 里引用的模块名

```bash
flutter_rust_bridge_codegen \
    ..
    --rust-output $crate/src/my_bridge.rs
```

then you need to modify this in `lib.rs`:

```diff
-mod bridge_generated;
+mod my_bridge;
```
