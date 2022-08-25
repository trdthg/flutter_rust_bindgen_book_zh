# 与 Windows 和 Linux 集成

本指南将 Windows 和 Linux 桌面应用程序的说明放在一起，因为它们使用相同的构建系统。

和其他平台一样：我们将使用脚本整合到现有的项目。现在我们将借用下模板，把
[rust.cmake](https://raw.githubusercontent.com/Desdaemon/flutter_rust_bridge_template/main/windows/rust.cmake)
下载到你的 "windows" 和 "linux" 文件夹里。请注意，CMake
会拒绝使用位于其工作目录之外的文件，所以在这两个构建文件夹之间会有一些重复的文件。

接下来，在你的`CMakeLists.txt`文件中添加这一行：

```diff
 # Generated plugin build rules, which manage building the plugins and adding
 # them to the application.
 include(flutter/generated_plugins.cmake)

+include(./rust.cmake)

 # === Installation ===
 # Support files are copied into place next to the executable, so that it can
```

## Linux

在 Linux 上，你需要将 CMake 的最低版本提高到 3.12，这是
[Corrosion](https://github.com/corrosion-rs/corrosion) 的要求，`rust.cmake` 依赖
Corrosion。请修改 `linux/CMakeLists.txt` 的这一行：

```diff
-cmake_minimum_required(VERSION 3.10)
+cmake_minimum_required(VERSION 3.12)
```

可选：你可以将 Corrosion 安装到系统上。请查看
[Linux troubleshooting notes](../template/setup_desktop.md).
