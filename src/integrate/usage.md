# 使用动态连接库

如果一切顺利，运行 `flutter run` 就会自动构建你的 Rust 库，Flutter 二进制文件，并将二者连接起来。现在唯一要做的事情就是使用它！

把
[这个文件](https://raw.githubusercontent.com/Desdaemon/flutter_rust_bridge_template/main/lib/ffi.dart)
下载到 `lib/ffi.dart`,接着修改下面几行：

```diff
 // Re-export the bridge so it is only necessary to import this file.
 export 'bridge_generated.dart';
 import 'dart:io' as io;

-const _base = 'native';
+const _base = '$crate';

 // On MacOS, the dynamic library is not bundled with the binary,
 // but rather directly **linked** against the binary.
 final _dylib = io.Platform.isWindows ? '$_base.dll' : 'lib$_base.so';
```
