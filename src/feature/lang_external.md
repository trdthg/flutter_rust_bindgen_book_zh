# 外部类型

## 定义在相同 crate 中不同文件里的类型

`use` 语句可以正常使用。例如：添加 `use crate::data::{MyEnum, MyStruct};`后，你可以正常的使用 `MyEnum` 和
`MyStruct`。

### 示例

```rust,noplayground
use crate::data::{MyEnum, MyStruct};

pub fn use_imported_things(my_struct: MyStruct, my_enum: MyEnum) { ... }
```

转换为：

```Dart
// Well it just behaves normally as you expect
Future<void> useImportedThings({required MyStruct myStruct, required MyEnum myEnum});
```

注意：如果你对 `Future` 感兴趣，请看 [这里](async_dart.md).

## 其他 crate 中的类型

这个功能被称为 "镜像 (mirror)". 简单来说，对于你想使用的外部类型，你需要重新编写一次作为镜像。这个镜像只会在代码生成时负责告知
`flutter_rust_bridge` 所需的类型信息。下面的例子里有详细的语法。

不用担心它会打破 DRY (Don’t Repeat Yourself) 原则，也不用担心你可能写错一个字段。因为如果镜像和原始类型不完全一致就会导致编译错误。

更多信息： [#352](https://github.com/fzyzcjy/flutter_rust_bridge/pull/352)

当多个结构体有相同的字段时，你可以使用下面的语法只重写一遍。
`#[frb(mirror(FirstStruct, SecondStruct, ThirdStruct))]`.
([#619](https://github.com/fzyzcjy/flutter_rust_bridge/pull/619))

### 示例

<!-- TODO! -->

```rust,noplayground
// Mirroring example:
// The goal of mirroring is to use external objects without needing to convert them with an intermediate type
// In this case, the struct ApplicationSettings is defined in another crate (called external-lib)

// To use an external type with mirroring, it MUST be imported publicly (aka. re-export)
pub use external_lib::{ApplicationEnv, ApplicationMode, ApplicationSettings};

// To mirror an external struct, you need to define a placeholder type with the same definition
#[frb(mirror(ApplicationSettings))]
pub struct _ApplicationSettings {
    pub name: String,
    pub version: String,
    pub mode: ApplicationMode,
    pub env: Box<ApplicationEnv>,
}

// It works with basic enums too
// Enums with struct variants are not yet supported
#[frb(mirror(ApplicationMode))]
pub enum _ApplicationMode {
    Standalone,
    Embedded,
}

#[frb(mirror(ApplicationEnv))]
pub struct _ApplicationEnv {
    pub vars: Vec<String>,
}

// This function can directly return an object of the external type ApplicationSettings because it has a mirror
pub fn get_app_settings() -> ApplicationSettings {
    external_lib::get_app_settings()
}

// Similarly, receiving an object from Dart works. Please note that the mirror definition must match entirely and the original struct must have all its fields public.
pub fn is_app_embedded(app_settings: ApplicationSettings) -> bool {
    // println!("env: {}", app_settings.env.vars[0]);
    match app_settings.mode {
        ApplicationMode::Standalone => false,
        ApplicationMode::Embedded => true,
    }
}
```

用一个结构体去镜像多个结构体：

```rust,noplayground
// *不* 需要这样做
#[frb(mirror(MessageId))]
pub struct MId(pub [u8; 32]);
#[frb(mirror(BlobId))]
pub struct BId(pub [u8; 32]);
#[frb(mirror(FeedId))]
pub struct FId(pub [u8; 32]);

// 只要编写一次就足够了
#[frb(mirror(MessageId, BlobId, FeedId))]
pub struct Id(pub [u8; 32]);
```
