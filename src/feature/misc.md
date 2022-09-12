# 杂项

## 把生成代码的定义和实现分开

生成的 `bridge_generated.dart` 文件默认情况下会包含 API 的定义和实现。在生成时，加上 `--dart-decl-output`
参数，它们就会被分开，并且定义中不会包含任何类似于 `dart:ffi` 的东西。

更多信息：[#298](https://github.com/fzyzcjy/flutter_rust_bridge/issues/298).
