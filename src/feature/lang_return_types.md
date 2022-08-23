# 返回值类型

返回值类型可以是 `anyhow::Result<YourType>`, 或者直接是你的类型 `YourType` .

## 示例

```rust,noplayground
pub fn f(a: i32, b: i32) -> i32 { a + b }

pub fn g(a: i32, b: i32) -> anyhow::Result<i32> { Ok(a + b) }
```
