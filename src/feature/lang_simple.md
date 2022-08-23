# 简单的对应关系

下面是一个简短的概览，显示了代码生成器可以生成的内容（并非完备）。有些行附带超链接，里面有更详细的解释。

| Rust                                              | Dart                        |
| ------------------------------------------------- | --------------------------- |
| [`Vec<u8>`, `Vec<i8>`..](lang_vec.md)             | `Uint8List`, `Int8List`, .. |
| [`Vec<T>`](lang_vec.md)                           | `List<T>`                   |
| [`[T; N]`](lang_vec.md)                           | `List<T>`                   |
| [`struct { .. }`, `struct( .. )`](lang_struct.md) | `class`                     |
| [`enum { A, B }`](lang_enum.md)                   | `enum`                      |
| [`enum { A(..) }`](lang_enum.md)                  | `@freezed class`            |
| [`use ...`](lang_external.md)                     | act normally                |
| [`Option<T>`](lang_option.md)                     | `T?`                        |
| `Box<T>`                                          | `T`                         |
| comments                                          | same                        |
| `Result::Err`, panic                              | `throw Exception`           |
| `i8`, `u8`, .., `usize`                           | `int`                       |
| `f32`, `f64`                                      | `double`                    |
| `bool`                                            | `bool`                      |
| `String`                                          | `String`                    |
| `()`                                              | `void`                      |
