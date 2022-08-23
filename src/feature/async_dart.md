# Dart 中的异步

默认情况下，生成的代码都是异步的。所以 `fn f(..) -> String` 将被转换为 `Future<String> f(..)`，多了一个
`Future`。

为什么？Flutter UI 是单线程的。如果你使用同步方法（一些老的 binding 就是这样的），在 Rust 代码执行时，UI 渲染将被阻塞。如果你的
Rust 代码进行一次复杂运算需要耗时 100ms，那么你的 UI 就会完全冻结 100ms，用户就不乐意了 😡。

另一方面，有了生成的异步 Dart 绑定，你就可以在 Dart/Flutter 的主隔离区直接调用，Rust 代码不会阻塞 Flutter UI。

async 和 `Future` 在 Flutter/Dart 中几乎无处不在，并且有着非常好的内部支持，完全不用担心 :D。

注意：一个常见的误解是在 Dart 的其他隔离区调用 Rust 代码（例如
"线程"），而不是主隔离区。这是完全没必要的，只会徒增你的心智负担。如上所述，即使你的 Rust 只用 100ms 就能完成，async 也只需要花费 0.1
ms，并且不会阻塞你的 UI。
