# 附录

> 注意：一些文档可能过时了。请在 ci.yaml, 主文档，justfile 等等查看最新版本，etc to see an up-to-date
> version. 本附录将进行大修。

## 发行新版本

通常是由库的拥有者做的 (@fzyzcjy),所以你基本不需要做这一步。如果你需要发布一个新版本，至少需要进行以下步骤。Bump 一些版本，在
changelog 中改变版本号，并使用 `cargo check`来自动更新实例的依赖版本。

```
just release
```

## 运行代码生成器的简单代码

只需要从
[CI codegen.yml](https://github.com/fzyzcjy/flutter_rust_bridge/blob/master/.github/workflows/codegen.yml)
复制即可。

```
(cd frb_codegen && cargo run --package flutter_rust_bridge_codegen --bin flutter_rust_bridge_codegen -- --rust-input ../frb_example/pure_dart/rust/src/api.rs --dart-output ../frb_example/pure_dart/dart/lib/bridge_generated.dart --dart-format-line-length 120 && cargo run --package flutter_rust_bridge_codegen --bin flutter_rust_bridge_codegen -- --rust-input ../frb_example/with_flutter/rust/src/api.rs --dart-output ../frb_example/with_flutter/lib/bridge_generated.dart --c-output ../frb_example/with_flutter/ios/Runner/bridge_generated.h --dart-format-line-length 120)
```

## 格式化 和 lint

```
(cd frb_codegen && cargo fmt --all); (cd frb_rust && cargo fmt --all); (cd frb_macros && cargo fmt --all); (cd frb_example/pure_dart/rust && cargo fmt --all); (cd frb_example/with_flutter/rust && cargo fmt --all);
(cd frb_codegen && cargo clippy); (cd frb_rust && cargo clippy); (cd frb_macros && cargo clippy); (cd frb_example/pure_dart/rust && cargo clippy); (cd frb_example/with_flutter/rust && cargo clippy);
(cd frb_dart && dart format . --line-length 80); (cd frb_example/pure_dart/dart && dart format . --line-length 120); (cd frb_example/with_flutter && dart format . --line-length 120);
(cd frb_dart && dart analyze --fatal-infos); (cd frb_example/pure_dart/dart && dart analyze --fatal-infos); (cd frb_example/with_flutter && dart analyze --fatal-infos);
```

## 升级依赖的版本

```
flutter pub upgrade flutter_rust_bridge
cargo update -p flutter_rust_bridge
```
