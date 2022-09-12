# Dart 中的同步

如果你真的需要生成同步的 Dart 函数，你可以使用 `SyncReturn<Vec<u8>>` 作为返回值类型。

我们建议只在非常快的 Rust 函数上这样做，否则 UI 将被阻塞。

因为同步 Dart 函数使用得很少，所以现在仅支持 `Vec<u8>` 一种类型，其他类型可以通过序列化实现，例如 JSON 和
Protobuf。注意，这种方法极少用到，99% 的 `flutter_rust_bridge` 都不会用到。如果你需要其他类型支持，请提交一个
issue.
