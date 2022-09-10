# Troubleshooting

## The generated store_dart_post_cobject() has the wrong signature / `'stdarg.h' file not found` in Linux / `stdbool.h` / ...

Try to run code generator with working directory at `/`, or set the environment
variable:

```bash
export CPATH="$(clang -v 2>&1 | grep "Selected GCC installation" | rev | cut -d' ' -f1 | rev)/include"
```

as described in [ffigen #257](https://github.com/dart-lang/ffigen/issues/257),
or add include path as is described in
[#108](https://github.com/fzyzcjy/flutter_rust_bridge/issues/108). This is a
problem with Rust's builtin `Command`. See also:
[#472](https://github.com/fzyzcjy/flutter_rust_bridge/issues/472) &
[#494](https://github.com/fzyzcjy/flutter_rust_bridge/issues/494).

## Issue with `store_dart_post_cobject`

If calling rust function gives the error below, please consider running **cargo
build** again. This can happen when the generated rs file is not included when
building is being done.

```sh
[ERROR:flutter/lib/ui/ui_dart_state.cc(209)] Unhandled Exception: Invalid argument(s): Failed to lookup symbol 'store_dart_post_cobject': target/debug/libadder.so: undefined symbol: store_dart_post_cobject
```

## Error running `cargo ndk`: `ld: error: unable to find library -lgcc`

Downgrade Android NDK to version 22. This is an
[ongoing issue](https://github.com/bbqsrc/cargo-ndk/issues/22) with `cargo-ndk`,
a library unrelated to flutter_rust_bridge but solely used to build the
examples, when using Android NDK version 23. (See
[#149](https://github.com/fzyzcjy/flutter_rust_bridge/issues/149))

## Fail to run `flutter_rust_bridge_codegen` on MacOS, "Please supply one or more path/to/llvm..."

If you are running macOS, you will need to specify a path to your llvm:

```shell
flutter_rust_bridge_codegen --rust-input path/to/your/api.rs --dart-output path/to/file/being/bridge_generated.dart --llvm-path /usr/local/homebrew/opt/llvm/
```

You can install llvm using `brew install llvm` and it will be installed at
`/usr/local/homebrew/opt/llvm/` by default.

## Freezed file is sometimes not generated when it should be

If your `.freezed.dart` or `.g.dart` seems outdated, ensure you have run the
`build_runner`.

Related: https://github.com/fzyzcjy/flutter_rust_bridge/issues/330

## `Can't create typedef from non-function type.`

Ensure min sdk version of Flutter `pubspec.yaml` is at least 2.13.0 to let
`ffigen` happy.

https://github.com/fzyzcjy/flutter_rust_bridge/issues/334

## Generated code is so long

Indeed all generated code are necessary (if you find something that can be
simplified, file an issue). Moreover, other code generation tools also generate
long code - for example, when using Google protobuf, a very popular
serialization library, I see >10k lines of Java code generated for a quite
simple source proto file.

## 为什么需要 Dart `2.14.0`

这个库并不需要 Dart SDK `>=2.14.0`, 但是最新的 `ffigen` 工具需要。所以才会在 `pubspec.yaml` 的
`environment` 中限制 `sdk: ">=2.14.0 <3.0.0"`. 如果你需要摆脱这个限制，请考虑使用更老版本的 `ffigen` 工具。

## 其它问题？

不要犹豫
[open an issue](https://github.com/fzyzcjy/flutter_rust_bridge/issues/new/choose)!
我通常会在几分钟或者是几小时内回复 (当然除了我睡觉时 :D).
