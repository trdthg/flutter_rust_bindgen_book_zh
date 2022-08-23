# 多文件

在大型项目中，把所有的文件都放在一个 `api.rs` 是不够的，我们通常想把它分离到 `api_of_one_module.rs`,
`api_of_another_module.rs` 等多个文件里。

你只需要指定所有的 Rust 输入文件以及输出位置即可，这里有一个例子：

```shell
flutter_rust_bridge_codegen \
  --rust-input "$REPO_DIR/native/src/api_1.rs" "$REPO_DIR/native/src/api_2.rs" \
  --dart-output "$REPO_DIR/lib/bridge_generated_api_1.dart" "$REPO_DIR/lib/bridge_generated_api_2.dart" \
  --class-name ApiClass1 ApiClass2 \
  --rust-output generated_api_1 generated_api_2
```

更多信息在 [这篇文章](../article/generate_multiple_files.md)。
