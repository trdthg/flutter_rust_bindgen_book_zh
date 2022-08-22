# [flutter_rust_bridge](https://github.com/fzyzcjy/flutter_rust_bridge): 用于 Flutter 和 Rust 的高级内存安全绑定生成器

_High-level memory-safe binding generator for Flutter/Dart <-> Rust_

[![Rust Package](https://img.shields.io/crates/v/flutter_rust_bridge.svg)](https://crates.io/crates/flutter_rust_bridge)
[![Flutter Package](https://img.shields.io/pub/v/flutter_rust_bridge.svg)](https://pub.dev/packages/flutter_rust_bridge)
[![Stars](https://img.shields.io/github/stars/fzyzcjy/flutter_rust_bridge)](https://github.com/fzyzcjy/flutter_rust_bridge)
[![CI](https://github.com/fzyzcjy/flutter_rust_bridge/actions/workflows/ci.yaml/badge.svg)](https://github.com/fzyzcjy/flutter_rust_bridge/actions/workflows/ci.yaml)
[![Example](https://github.com/fzyzcjy/flutter_rust_bridge/actions/workflows/post_release.yaml/badge.svg)](https://github.com/fzyzcjy/flutter_rust_bridge/actions/workflows/post_release.yaml)
[![Codacy Badge](https://api.codacy.com/project/badge/Grade/6afbdad19e7245adbf9e9771777be3d7)](https://app.codacy.com/gh/fzyzcjy/flutter_rust_bridge?utm_source=github.com&utm_medium=referral&utm_content=fzyzcjy/flutter_rust_bridge&utm_campaign=Badge_Grade_Settings)

![Logo](https://github.com/fzyzcjy/flutter_rust_bridge/raw/master/book/logo.png)

想把 [Flutter](https://flutter.dev/)（一个跨平台的热重载快速开发 UI 工具包）和
[Rust](https://www.rust-lang.org/)（一种使每个人都能构建可靠和高效软件的语言）之间的优点结合起来？它来了！

## 🚀 Advantages

- **内存安全**: 完全不用考虑 malloc/free.
- **特性丰富**: 带有值的 `enum`, 根据平台优化的 `Vec`, 可能递归的 `struct`, 大数组零拷贝，`流数据` (迭代器)
  抽象，错误处理 (`Result`), 可取消的任务，并发控制，等。你可以在
  [这里](https://fzyzcjy.github.io/flutter_rust_bridge/feature.html) 查看所有特性。
- **异步支持**: Rust 代码永远不会阻塞 Flutter. 从 Flutter 的主隔离区（线程）`main isolate (thread)`
  中自然的调用 Rust 代码。
- **轻量级**: 这不是一个巨大的包含所有东西框架，所以你可以自由的使用你喜欢的 Flutter 和 Rust 第三方库。<sub>例如，使用
  Flutter 库（比如 MobX）进行状态管理更加优雅简单（相比于在 Rust 中实现）; 使用 Rust 实现一个照片处理的算法更加快速和安全
  (相比于在 Flutter 中实现).</sub>
- **跨平台**: 支持 Android, iOS, Windows, Linux, MacOS
  ([Web](https://github.com/fzyzcjy/flutter_rust_bridge/issues/315) coming soon)
- **易于代码审查 & 方便**: 这个库简单地模拟了人类如何编写模板代码，一点也不神奇！如果你想让说服你自己（或你的团队）相信它是安全的，
  没有多少代码可看。 ([更多](https://fzyzcjy.github.io/flutter_rust_bridge/safety.html)
  safety concerns.)
- **快速**: 它只是一层浅层次的包装（尽管功能丰富），没有想 pritobuf 序列化的开销，因此高性能。(更多的
  [benchmarks](https://github.com/fzyzcjy/flutter_rust_bridge/issues/318#issuecomment-1034536815)
  之后带来) <small>(扔掉了像线程池这样的组件，让它更快)</small>
- **与纯 Dart 兼容:** 尽管名字里包含了 Rust，这个库 100% 兼容
  [Pure Dart](https://github.com/fzyzcjy/flutter_rust_bridge/blob/master/frb_example/pure_dart/README.md)

## 💡 用户指南

请看 [用户指南](https://fzyzcjy.github.io/flutter_rust_bridge/) for
[show-me-the-code](https://fzyzcjy.github.io/flutter_rust_bridge/quickstart.html),
[教程](https://fzyzcjy.github.io/flutter_rust_bridge/tutorial_with_flutter.html),
[特性](https://fzyzcjy.github.io/flutter_rust_bridge/feature.html) and much more.

## 📎 P.S. 方便的 Flutter 测试

如果您想在 Flutter
中方便地编写和调试测试，行为历史、时间回溯、屏幕截图、快速重新执行、视频录制、互动模式等功能，这里有我的另一个开源库：[flutter_convenient_test](https://github.com/fzyzcjy/flutter_convenient_test).

## ✨ 贡献者

<!-- ALL-CONTRIBUTORS-BADGE:START - Do not remove or modify this section -->

[![All Contributors](https://img.shields.io/badge/all_contributors-29-orange.svg?style=flat-square)](#contributors-)

<!-- ALL-CONTRIBUTORS-BADGE:END -->

Thanks goes to these wonderful people
([emoji key](https://allcontributors.org/docs/en/emoji-key) following
[all-contributors](https://github.com/all-contributors/all-contributors)
specification):

<!-- ALL-CONTRIBUTORS-LIST:START - Do not remove or modify this section -->
<!-- prettier-ignore-start -->
<!-- markdownlint-disable -->
<table>
  <tr>
    <td align="center"><a href="https://github.com/fzyzcjy"><img src="https://avatars.githubusercontent.com/u/5236035?v=4?s=100" width="100px;" alt=""/><br /><sub><b>fzyzcjy</b></sub></a><br /><a href="https://github.com/fzyzcjy/flutter_rust_bridge/commits?author=fzyzcjy" title="Code">💻</a> <a href="https://github.com/fzyzcjy/flutter_rust_bridge/commits?author=fzyzcjy" title="Documentation">📖</a> <a href="#example-fzyzcjy" title="Examples">💡</a> <a href="#ideas-fzyzcjy" title="Ideas, Planning, & Feedback">🤔</a> <a href="#maintenance-fzyzcjy" title="Maintenance">🚧</a></td>
    <td align="center"><a href="https://github.com/Desdaemon"><img src="https://avatars.githubusercontent.com/u/36768030?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Viet Dinh</b></sub></a><br /><a href="https://github.com/fzyzcjy/flutter_rust_bridge/commits?author=Desdaemon" title="Code">💻</a> <a href="https://github.com/fzyzcjy/flutter_rust_bridge/commits?author=Desdaemon" title="Tests">⚠️</a> <a href="https://github.com/fzyzcjy/flutter_rust_bridge/commits?author=Desdaemon" title="Documentation">📖</a></td>
    <td align="center"><a href="https://github.com/SecondFlight"><img src="https://avatars.githubusercontent.com/u/6700184?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Joshua Wade</b></sub></a><br /><a href="https://github.com/fzyzcjy/flutter_rust_bridge/commits?author=SecondFlight" title="Code">💻</a></td>
    <td align="center"><a href="https://github.com/smw-wagnerma"><img src="https://avatars.githubusercontent.com/u/66412697?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Marcel</b></sub></a><br /><a href="https://github.com/fzyzcjy/flutter_rust_bridge/commits?author=smw-wagnerma" title="Code">💻</a></td>
    <td align="center"><a href="https://github.com/rustui"><img src="https://avatars.githubusercontent.com/u/90625190?v=4?s=100" width="100px;" alt=""/><br /><sub><b>rustui</b></sub></a><br /><a href="https://github.com/fzyzcjy/flutter_rust_bridge/commits?author=rustui" title="Documentation">📖</a></td>
    <td align="center"><a href="https://adventures.michaelfbryan.com/"><img src="https://avatars.githubusercontent.com/u/17380079?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Michael Bryan</b></sub></a><br /><a href="https://github.com/fzyzcjy/flutter_rust_bridge/commits?author=Michael-F-Bryan" title="Code">💻</a></td>
    <td align="center"><a href="https://bus710.net"><img src="https://avatars.githubusercontent.com/u/8920680?v=4?s=100" width="100px;" alt=""/><br /><sub><b>bus710</b></sub></a><br /><a href="https://github.com/fzyzcjy/flutter_rust_bridge/commits?author=bus710" title="Documentation">📖</a></td>
  </tr>
  <tr>
    <td align="center"><a href="https://scholar.google.com/citations?user=RbAto7EAAAAJ"><img src="https://avatars.githubusercontent.com/u/1213857?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Sebastian Urban</b></sub></a><br /><a href="https://github.com/fzyzcjy/flutter_rust_bridge/commits?author=surban" title="Code">💻</a></td>
    <td align="center"><a href="https://github.com/trobanga"><img src="https://avatars.githubusercontent.com/u/8888869?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Daniel</b></sub></a><br /><a href="https://github.com/fzyzcjy/flutter_rust_bridge/commits?author=trobanga" title="Code">💻</a></td>
    <td align="center"><a href="https://github.com/AlienKevin"><img src="https://avatars.githubusercontent.com/u/22850071?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Kevin Li</b></sub></a><br /><a href="https://github.com/fzyzcjy/flutter_rust_bridge/commits?author=AlienKevin" title="Code">💻</a> <a href="https://github.com/fzyzcjy/flutter_rust_bridge/commits?author=AlienKevin" title="Documentation">📖</a></td>
    <td align="center"><a href="https://valeth.me"><img src="https://avatars.githubusercontent.com/u/3198362?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Patrick Auernig</b></sub></a><br /><a href="https://github.com/fzyzcjy/flutter_rust_bridge/commits?author=valeth" title="Code">💻</a></td>
    <td align="center"><a href="https://antonok.com"><img src="https://avatars.githubusercontent.com/u/22821309?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Anton Lazarev</b></sub></a><br /><a href="https://github.com/fzyzcjy/flutter_rust_bridge/commits?author=antonok-edm" title="Code">💻</a></td>
    <td align="center"><a href="https://github.com/Unoqwy"><img src="https://avatars.githubusercontent.com/u/65187632?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Unoqwy</b></sub></a><br /><a href="https://github.com/fzyzcjy/flutter_rust_bridge/commits?author=Unoqwy" title="Code">💻</a></td>
    <td align="center"><a href="https://feber.dev"><img src="https://avatars.githubusercontent.com/u/1727318?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Febrian Setianto</b></sub></a><br /><a href="https://github.com/fzyzcjy/flutter_rust_bridge/commits?author=feber" title="Documentation">📖</a></td>
  </tr>
  <tr>
    <td align="center"><a href="https://github.com/Syndim"><img src="https://avatars.githubusercontent.com/u/835035?v=4?s=100" width="100px;" alt=""/><br /><sub><b>syndim</b></sub></a><br /><a href="https://github.com/fzyzcjy/flutter_rust_bridge/commits?author=syndim" title="Code">💻</a></td>
    <td align="center"><a href="https://github.com/sagudev"><img src="https://avatars.githubusercontent.com/u/16504129?v=4?s=100" width="100px;" alt=""/><br /><sub><b>sagu</b></sub></a><br /><a href="https://github.com/fzyzcjy/flutter_rust_bridge/commits?author=sagudev" title="Code">💻</a> <a href="https://github.com/fzyzcjy/flutter_rust_bridge/commits?author=sagudev" title="Documentation">📖</a></td>
    <td align="center"><a href="https://bandism.net/"><img src="https://avatars.githubusercontent.com/u/22633385?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Ikko Ashimine</b></sub></a><br /><a href="https://github.com/fzyzcjy/flutter_rust_bridge/commits?author=eltociear" title="Documentation">📖</a></td>
    <td align="center"><a href="https://github.com/alanlzhang"><img src="https://avatars.githubusercontent.com/u/59032810?v=4?s=100" width="100px;" alt=""/><br /><sub><b>alanlzhang</b></sub></a><br /><a href="https://github.com/fzyzcjy/flutter_rust_bridge/commits?author=alanlzhang" title="Code">💻</a> <a href="https://github.com/fzyzcjy/flutter_rust_bridge/commits?author=alanlzhang" title="Documentation">📖</a></td>
    <td align="center"><a href="https://github.com/sccheruku"><img src="https://avatars.githubusercontent.com/u/5800058?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Sai Chaitanya</b></sub></a><br /><a href="https://github.com/fzyzcjy/flutter_rust_bridge/commits?author=sccheruku" title="Code">💻</a></td>
    <td align="center"><a href="https://ares.zone (国内)"><img src="https://avatars.githubusercontent.com/u/40336192?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Ares Andrew</b></sub></a><br /><a href="https://github.com/fzyzcjy/flutter_rust_bridge/commits?author=TENX-S" title="Documentation">📖</a></td>
    <td align="center"><a href="https://github.com/raphaelrobert"><img src="https://avatars.githubusercontent.com/u/9882746?v=4?s=100" width="100px;" alt=""/><br /><sub><b>raphaelrobert</b></sub></a><br /><a href="https://github.com/fzyzcjy/flutter_rust_bridge/commits?author=raphaelrobert" title="Documentation">📖</a></td>
  </tr>
  <tr>
    <td align="center"><a href="https://github.com/thomas725"><img src="https://avatars.githubusercontent.com/u/68635351?v=4?s=100" width="100px;" alt=""/><br /><sub><b>thomas725</b></sub></a><br /><a href="https://github.com/fzyzcjy/flutter_rust_bridge/commits?author=thomas725" title="Documentation">📖</a></td>
    <td align="center"><a href="https://dport.me"><img src="https://avatars.githubusercontent.com/u/7816187?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Daniel Porteous (dport)</b></sub></a><br /><a href="https://github.com/fzyzcjy/flutter_rust_bridge/commits?author=banool" title="Documentation">📖</a></td>
    <td align="center"><a href="https://github.com/w-ensink"><img src="https://avatars.githubusercontent.com/u/46427708?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Wouter Ensink</b></sub></a><br /><a href="https://github.com/fzyzcjy/flutter_rust_bridge/commits?author=w-ensink" title="Documentation">📖</a></td>
    <td align="center"><a href="https://github.com/dbsxdbsx"><img src="https://avatars.githubusercontent.com/u/17372655?v=4?s=100" width="100px;" alt=""/><br /><sub><b>老董</b></sub></a><br /><a href="https://github.com/fzyzcjy/flutter_rust_bridge/commits?author=dbsxdbsx" title="Code">💻</a> <a href="https://github.com/fzyzcjy/flutter_rust_bridge/commits?author=dbsxdbsx" title="Documentation">📖</a></td>
    <td align="center"><a href="https://github.com/lattice0"><img src="https://avatars.githubusercontent.com/u/6632321?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Lattice 0</b></sub></a><br /><a href="https://github.com/fzyzcjy/flutter_rust_bridge/commits?author=lattice0" title="Code">💻</a> <a href="https://github.com/fzyzcjy/flutter_rust_bridge/commits?author=lattice0" title="Documentation">📖</a></td>
    <td align="center"><a href="https://soeur.dev"><img src="https://avatars.githubusercontent.com/u/26034975?v=4?s=100" width="100px;" alt=""/><br /><sub><b>orange soeur</b></sub></a><br /><a href="https://github.com/fzyzcjy/flutter_rust_bridge/commits?author=juzi5201314" title="Documentation">📖</a></td>
    <td align="center"><a href="https://github.com/Roms1383"><img src="https://avatars.githubusercontent.com/u/21016014?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Rom's</b></sub></a><br /><a href="https://github.com/fzyzcjy/flutter_rust_bridge/commits?author=Roms1383" title="Code">💻</a> <a href="https://github.com/fzyzcjy/flutter_rust_bridge/commits?author=Roms1383" title="Documentation">📖</a></td>
  </tr>
  <tr>
    <td align="center"><a href="https://github.com/Cupnfish"><img src="https://avatars.githubusercontent.com/u/40173605?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Cupnfish</b></sub></a><br /><a href="https://github.com/fzyzcjy/flutter_rust_bridge/commits?author=Cupnfish" title="Code">💻</a></td>
  </tr>
</table>

<!-- markdownlint-restore -->
<!-- prettier-ignore-end -->

<!-- ALL-CONTRIBUTORS-LIST:END -->

More specifically, thanks for all these contributions:

- [Desdaemon](https://github.com/Desdaemon): Support not only simple enums but
  also enums with fields which gets translated to native enum or freezed class
  in Dart. Support the Option type as nullable types in Dart. Support Vec of
  Strings type. Support comments in code. Add marker attributes for future
  usage. Add Linux and Windows support for with-flutter example, and make CI
  works for that. Avoid parameter collision. Overhaul the documentation and add
  several chapters to demonstrate configuring a Flutter+Rust project in all five
  platforms. Refactor command module. Precompiled binary CI workflow. Fix bugs.
- [SecondFlight](https://github.com/SecondFlight): Allow structs and enums to be
  imported from other files within the crate by creating source graph.
  Auto-create relavent dir. Fix `store_dart_post_cobject` error with ffigen 6.0.
- [Unoqwy](https://github.com/Unoqwy): Add struct mirrors, such that types in
  the external crates can be imported and used without redefining and copying.
- [antonok-edm](https://github.com/antonok-edm): Avoid converting syn types to
  strings before parsing to improve code and be more robust.
- [lattice0](https://github.com/lattice0): Support methods, such that Rust
  struct impls can be converted to Dart class methods. StreamSink at any
  argument.
- [sagudev](https://github.com/sagudev): Make code generator a `lib`. Add error
  types. Depend on `cbindgen`. Fix LLVM paths. Update deps. Fix CI errors.
- [surban](https://github.com/surban): Support unit return type. Skip
  unresolvable modules. Ignore prefer_const_constructors. Non-final Dart fields.
- [trobanga](https://github.com/trobanga): Add support for `[T;N]` structs. Add
  `usize` support. Add a cmd argument. Separate dart tests.
- [Roms1383](https://github.com/Roms1383): Fix build_runner calling bug. Remove
  global `ffigen` dependency. Improve version check. Fix enum name-variant
  conflicts. Update CI. Code cleanup.
- [dbsxdbsx](https://github.com/dbsxdbsx): Allow generating multiple Rust and
  Dart files.
- [AlienKevin](https://github.com/AlienKevin): Add flutter example for macOS.
  Add doc for Android NDK bug.
- [alanlzhang](https://github.com/alanlzhang): Add generation for Dart metadata.
- [efc-mw](https://github.com/efc-mw): Improve Windows encoding handling.
- [valeth](https://github.com/valeth): Rename callFfi's port.
- [Cupnfish](https://github.com/Cupnfish): Allow multi mirror.
- [sccheruku](https://github.com/sccheruku): Prevent double-generating utility.
- [w-ensink](https://github.com/w-ensink): Improve doc. Fix CI. Refactor. Add
  tests.
- [Michael-F-Bryan](https://github.com/Michael-F-Bryan): Detect broken bindings.
- [bus710](https://github.com/bus710): Add a case in troubleshooting.
- [Syndim](https://github.com/Syndim): Add a bracket to box.
- [banool](https://github.com/banool): Fix symbol-stripping doc.
- [TENX-S](https://github.com/TENX-S): Improve doc. Reproduce a bug.
- [raphaelrobert](https://github.com/raphaelrobert): Remove oudated doc.
- [thomas725](https://github.com/thomas725): Improve doc.
- [juzi5201314](https://github.com/juzi5201314): Improve doc.
- [feber](https://github.com/feber): Fix doc link.
- [rustui](https://github.com/rustui): Fix a typo.
- [eltociear](https://github.com/eltociear): Fix a typo.
