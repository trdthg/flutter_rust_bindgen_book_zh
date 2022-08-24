# 安卓设置

对于安卓平台，你需要安装一部分组件：

## Rust 编译目标

交叉编译到安卓需要一些额外的组件，你可以通过下面的命令安装：

```shell
rustup target add \
    aarch64-linux-android \
    armv7-linux-androideabi \
    x86_64-linux-android \
    i686-linux-android
```

## JDK 8

Android Studio 依赖于 `javax` 库存在于 Java 运行时，验证安装成功的唯一可靠的方法是安装一个老版本的 Java。在类 Unix
系统上，你可以使用 [asdf](https://asdf-vm.com/) 或者类似的工具去管理你的 Java 版本。模板在 `.tool-versions`
文件中定义了一个已知的可以正常运行的 Java 版本。

> 译者注：`.tool-versions` 是 asdf 的配置文件

## [Android NDK]

安装：

> Android Studio > SDK Manager > SDK Tools > uncheck Hide Obsolete Packages >
> NDK (version 22)

> 译者注：用户也可以不下载 Android Studio，直接通过 sdkmanager 在命令行安装。

[Android NDK], 或者说 Native Development Kit, 确保了使用其他语言编写的代码可以通过 JNI 或者说
[Java Native Interface] 运行在 JVM 上。我们会把 Cargo 创建的动态连接库和项目的打包结果打包在一起。

跟着上面的步骤，你应该会把 NDK 安装到了 `$ANDROID_SDK_HOME/ndk` 文件夹，ANDROID_SDK_HOME 通常是：

- Windows: `%APPDATA%\Local\Android\sdk`
- MacOS: `~/Library/Android/sdk`
- Linux: 通过设置环境变量 ANDROID_SDK_HOME, 或者 `~/Android/sdk`

[An issue] 在构建 Rust `core` 库时，只有 NDK 22 和更早版本可以使用。

## `ANDROID_NDK` Gradle 配置

```shell
echo "ANDROID_NDK=(path to NDK)" >> ~/.gradle/gradle.properties
```

下一步，你需要设置 NDK 对 Gradle 可见。根据你的系统有不同的设置方法，但是一般都可以在 `~/.gradle/gradle.properties`
里配置以下内容：

```
ANDROID_NDK=(path to NDK)
```

或者是修改当前项目文件夹，android 目录里的同名文件。

## [cargo-ndk]

```shell
cargo install cargo-ndk --version 2.6.0
```

[cargo-ndk] 是一个 cargo 插件，它能够将代码编译到适合的 JNI 而 typedef DartPostCObjectFnType =
ffi.Pointer< ffi.NativeFunction<ffi.Bool Function(DartPort,
ffi.Pointer<ffi.Void>)>>; typedef DartPort = ffi.Int64;c
不需要额外的配置。运行上述命令进行安装。cargo-ndk 2.7.0 版本引入了一些变化，破坏了对 NDK 22 版本的支持，所以 目前必须使用 2.6.0。

## 可选的 NDK 设置

你也可以选择最新版本的 NDK，它比 22 版本要好。但是你需要 Hack
部分代码去解决一个报错：[unable to find library -lgcc error].

### Android NDK

安装最新版本的 NDK:

> Android Studio > SDK Manager > SDK Tools > NDK (Side by side)

### [cargo-ndk]

如果你使用的是版本高于 22 的 NDK，那么你需要 `cargo-ndk` 2.7.0 或者更新版本。

```
cargo install cargo-ndk --version ^2.7.0
```

A workaround may be under development in the cargo-ndk project. Until it is
finished, you need to manually create four text files to redirect calls from
libgcc to libunwind ([reference]):

1. Find out all the 4 folders containing file `libunwind.a`.
   - On Windows, it is similar to:
     ```
     C:\Users\Administrator\AppData\Local\Android\Sdk\ndk\24.0.8215888\toolchains\llvm\prebuilt\windows-x86_64\lib64\clang\14.0.1\lib\linux\x86_64\
     ```

   - On macOS Monterey, it is similar to:
     ```
     ~/Library/Android/sdk/ndk/24.0.8215888/toolchains/llvm/prebuilt/darwin-x86_64/lib64/clang/14.0.1/lib/linux/x86_64/
     ```
   The three other folders end with `aarch64`, `arm`, `i386` instead of
   `x86_64`.

2. Create 4 text files named `libgcc.a` in the four folders mentioned above with
   this contents

   ```
   INPUT(-lunwind)
   ```

[Android NDK]: https://developer.android.com/ndk
[Java Native Interface]: https://docs.oracle.com/javase/7/docs/technotes/guides/jni/spec/jniTOC.html
[An issue]: https://github.com/rust-lang/rust/pull/85806
[cargo-ndk]: https://github.com/bbqsrc/cargo-ndk
[unable to find library -lgcc error]: https://github.com/bbqsrc/cargo-ndk/issues/22
[reference]: https://github.com/rust-lang/rust/pull/85806#issuecomment-1096266946
