# Windows 和 Linux

Windows 和 Linux 共享同一套编译系统（CMake），从零开始设置这两个平台也非常简单。模板该模板使用到了 [Corrosion]
库来加快这一过程，安装 Corrosion 需要先克隆代码，并初始化。跟着 [本指南] 学习如何将 [Corrosion]
安装到你的系统上。安装完成后，请继续修改 `rust.cmake`。

```diff
-# find_package(Corrosion REQUIRED)
+find_package(Corrosion REQUIRED)

-include(FetchContent)
-
-FetchContent_Declare(
-    Corrosion
-    GIT_REPOSITORY https://github.com/AndrewGaspar/corrosion.git
-    GIT_TAG origin/master # Optionally specify a version tag or branch here
-)
-
-FetchContent_MakeAvailable(Corrosion)
```

## Troubleshooting: CMake on Linux

[Corrosion] 对 CMake 的最低版本需求是 3.12，这不是 `CMakeLists.txt` 的默认版本。所以你需要手动修改
`linux/CMakeLists.txt`:

```diff
-cmake_minimum_required(VERSION 3.10)
+cmake_minimum_required(VERSION 3.12)
```

但是它带来了另一个问题，它不允许你通过 Flutter SDK 通过 Snap 构建，因为他的构建过程和 CMake 3.10
绑定。可能的话，建议使用命令行手动安装
Flutter。[canonical/flutter-snap#61](https://github.com/canonical/flutter-snap/pull/61)
地。

一个变通的方法是忽略 `rust.cmake` 并手动配置 CMake 来构建和捆绑 Rust 库。例如
[本评论](https://github.com/fzyzcjy/flutter_rust_bridge/issues/318#issuecomment-1038751426)
是在 ARM Linux 上使用 Flutter。

[Corrosion]: https://github.com/corrosion-rs/corrosion
[本指南]: https://github.com/corrosion-rs/corrosion#installation
