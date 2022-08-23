# Summary

[介绍](./src/index.md)

# Part I: 核心

- [x] [🧭 快速开始](./src/quickstart.md)
- [x] [📚 教程：一个 Flutter 和 Rust 构建的 app](./src/tutorial_with_flutter.md)
- [x] [🎼 特性](./src/feature.md)
  - [x] [语言转换](./src/./src/feature/lang.md)
    - [x] [对应关系总览](./src/feature/lang_simple.md)
    - [x] [Vec 和 数组](./src/feature/lang_vec.md)
    - [x] [结构体](./src/feature/lang_struct.md)
    - [x] [枚举](./src/feature/lang_enum.md)
    - [x] [外部类型](./src/feature/lang_external.md)
    - [x] [Option](./src/feature/lang_option.md)
    - [x] [方法](./src/feature/lang_methods.md)
    - [x] [返回值类型](./src/feature/lang_return_types.md)
  - [x] [零拷贝](./src/feature/zero_copy.md)
  - [x] [流 / 迭代器](./src/feature/stream.md)
  - [x] [Dart 异步](./src/feature/async_dart.md)
  - [x] [Dart 同步](./src/feature/sync_dart.md)
  - [x] [并发](./src/feature/concurrency.md)
  - [x] [Handler](./src/feature/handler.md)
  - [x] [初始化](./src/feature/init.md)
  - [x] [Rust 异步](./src/feature/async_rust.md)
  - [x] [多文件](./src/feature/multiple_files.md)
  - [x] [在 build.rs 中运行](./src/feature/build_rs.md)
  - [x] [可取消的任务](./src/feature/cancelable_task.md)
  - [x] [对象池](./src/feature/object_pool.md)
  - [x] [杂项](./src/feature/misc.md)

# Part II: 用户指南

- [ ] [从模板创建](./src/template.md)
  - [ ] [创建一个新项目](./src/template/setup.md)
    - [ ] [安卓设置](./src/template/setup_android.md)
    - [ ] [IOS 设置](./src/template/setup_ios.md)
    - [ ] [Web 设置](./src/template/setup_web.md)
    - [ ] [Windows 和 Linux](./src/template/setup_desktop.md)
    - [ ] [其他平台](./src/template/setup_others.md)
  - [ ] [模板之旅](./src/template/tour.md)
    - [ ] [native/src/api.rs](./src/template/tour_api.md)
    - [ ] [`android/app/build.gradle`](./src/template/tour_gradle.md)
    - [ ] [`native/native.xcodeproj`](./src/template/tour_native_proj.md)
    - [ ] [`justfile`](./src/template/tour_justfile.md)
    - [ ] [`rust.cmake`](./src/template/tour_cmake.md)
  - [ ] [代码生成](./src/template/generate.md)
    - [ ] [安装 codegen](./src/template/generate_install.md)
    - [ ] [添加代码](./src/template/generate_adding_code.md)
    - [ ] [使用 build_runner](./src/template/generate_build_runner.md)
    - [ ] [收尾工作](./src/template/generate_finish.md)
- [ ] [集成到现有项目](./src/integrate.md)
  - [ ] [创建一个新 crate](./src/integrate/new_crate.md)
  - [ ] [安装依赖](./src/integrate/deps.md)
  - [ ] [与 Android 集成](./src/integrate/android.md)
    - [ ] [Hooking onto tasks](./src/integrate/android_tasks.md)
    - [ ] [在 Gradle 中使用 CMake](./src/integrate/android_cmake.md)
  - [ ] [与 iOS/MacOS 集成](./src/integrate/ios.md)
    - [ ] [创建 Rust 项目](./src/integrate/ios_proj.md)
    - [ ] [链接该项目](./src/integrate/ios_linking.md)
    - [ ] [生成代码绑定](./src/integrate/ios_gen.md)
    - [ ] [使用假头文件](./src/integrate/ios_headers.md)
  - [ ] [与 Windows and Linux 集成](./src/integrate/desktop.md)
  - [ ] [与 Web 集成](./src/integrate/web.md)
  - [ ] [使用动态连接库](./src/integrate/usage.md)
  - [ ] [收尾工作](./src/integrate/finish.md)

# Part III: 贡献指南

- [ ] [总览](./src/contributing/overview.md)
- [ ] [整体设计](./src/contributing/design.md)
- [ ] [附录](./src/contributing/appendix.md)

# Part IV: 更多文档

- [ ] [教程：Pure Dart](./src/tutorial_pure_dart.md)
- [ ] [安全问题](./src/safety.md)
- [ ] [疑难解答](./src/troubleshooting.md)
- [ ] [命令行参数](./src/command_line.md)
- [ ] [从零开始设置 Fluuter/Rust 环境](./src/set_up_from_scratch.md)
- [ ] [文章](./src/article.md)
  - [ ] [Rust 异步](./src/article/async_in_rust.md)
  - [ ] [生成多文件](./src/article/generate_multiple_files.md)
