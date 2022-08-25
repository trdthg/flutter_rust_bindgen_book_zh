# CMake 和 Gradle

如果你之前看过 _windows_ 或 _linux_ 文件夹，你会看到 一个名为 _CMakeLists.txt_ 的文件。这个文件是 CMake
工具链的定义文件，Flutter 使用它来构建 Windows 和 Linux 应用程序。你也可以在 Gradle 上使用
这个策略，但这种设置超出了本指南的范围，是留给高级人员的。

请参考官方 Android 文档中的
[Add C and C++ code to your project](https://developer.android.com/studio/projects/add-native-code)，围绕
C 语言的特定部分进行修改，并使用 [`Corrosion`](https://github.com/corrosion-rs/corrosion)
这样的工具来集成到 Cargo。这种设置的好处是，你可以重复使用 C 语言工具，并且受益于各种现有成熟技术，如构建缓存。
