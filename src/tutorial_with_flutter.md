# 教程：一个 Flutter 和 Rust 构建的 app

在这个教程中，我们将绘制一个
[曼德博集合（英语：Mandelbrot set，或译为曼德布洛特复数集合）](https://en.wikipedia.org/wiki/Mandelbrot_set)（一个著名的分形）。这个图片会由
Rust 算法生成，并在 Flutter 中绘制，通过这个库通信。

<!-- markdownlint-disable MD033 -->
<details>
<summary>(点击查看：Mandelbrot set 是什么：)</summary>

曼德博集合是由复数 `c` 组成的点的集合，对于这些点，均满足函数：
`f_c(z) = z^{2} + c`，不同的参数可能使序列的绝对值逐渐发散到无限大，也可能收敛在有限的区域内。曼德博集合 M
就是使序列不延伸至无限大的所有复数 c 的集合。曼德勃罗集的图像显示了一个精心设计的、无限复杂的边界
随着放大倍数的增加，逐渐显示出越来越细的递归细节。放大倍数时，显示出越来越细的递归细节。

<p align="center">
<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/a/a4/Mandelbrot_sequence_new.gif/220px-Mandelbrot_sequence_new.gif">
</p>

图片来源：维基百科

</details>

## 获取代码

请[安装 Flutter](https://flutter.dev/docs/get-started/install) (可以选择
[桌面支持](https://flutter.dev/desktop)，如果你想把程序运行在桌面上而不是手机),
[安装 Rust](https://www.rust-lang.org/learn/get-started), 熟悉一下之后，接着克隆样例代码：

```shell
git clone https://github.com/fzyzcjy/flutter_rust_bridge && cd flutter_rust_bridge/frb_example/with_flutter
```

## 可选：运行代码生成器

这一步是可选的，因为我已经在 [快速入门](./quickstart.md) 时生成了源代码，你是你再次运行也不会看到任何改变。

一旦你修改了 `api.rs`，就需要再次运行代码生成。代码生成器所需要的更多依赖可以在
[Installing dependencies](integrate/deps.md) 查看

## 运行 app

### 前言：命令细节

如果你需要了解命令的各个细节，可以查看
[CI 工作流](https://github.com/fzyzcjy/flutter_rust_bridge/blob/master/.github/workflows/ci.yaml)。`flutter_android_test`,
`flutter_ios_test`, `flutter_windows_test`, `flutter_macos_test` 和
`flutter_linux_test` 演示了从一台新机器上运行该项目所需要的所有命令

> 译者注：如果您的遇到运行失败，缺少环境等问题，请参考上述 CI 工作流。下面的 cargo ndk 等部分工具，和对应的交叉编译环境需要单独安装，具体请参考
> CI 工作流。

### Android app

- 把 `ANDROID_NDK=(path to NDK)` 添加到 `android/gradle.properties`
- 接着运行 `cargo ndk -o ../android/app/src/main/jniLibs build`.
- 最后像平时一样运行 `flutter run`.

**注意**: [这个教程](https://stackoverflow.com/q/69515032/4619958) 能够帮你在构建 Flutter
程序时自动运行 cargo.

### iOS app

- 打开 `Cargo.toml` 并把 `cdylib` 修改为 `staticlib`
- 接着运行
  `cargo lipo && cp target/universal/debug/libflutter_rust_bridge_example.a ../ios/Runner`
  编译 Rust 代码，并复制静态连接库。
- 最后像平时一样运行 `flutter run`.

**注意**: [这个教程](https://stackoverflow.com/q/69515032/4619958) 能够帮你在构建 Flutter
程序时自动运行 cargo.

### Windows app

假设 [Flutter 桌面支持](https://flutter.dev/desktop#set-up) 已经配置完成，你可以直接运行
`flutter run`。更多细节可以在
[#66](https://github.com/fzyzcjy/flutter_rust_bridge/issues/66).

### Linux app

和 Windows 一样。如果你是通过 `snap` 安装的 Flutter, 请注意一下
[#53](https://github.com/canonical/flutter-snap/issues/53).

### MacOS app

和 Windows 一样。(P.S. 本质上说，`cargo-xcode` 被用于自动化)