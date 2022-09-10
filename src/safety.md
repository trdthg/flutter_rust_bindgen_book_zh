# 安全顾虑

该库使用 CI 工作流，并会在设置过程中自动运行 [Valgrind](https://www.valgrind.org/) ，当 Dart 程序使用该库调用
Rust 程序时，Valgrind 能及时发现内存安全问题
<sub>( 注意：即时你只运行一个简单的 hello-world Dart 程序，Valgrind 也会检测到几百个错误。请查看
[this Dart lang issue](https://github.com/dart-lang/sdk/issues/47346)
了解更多。因此，我检查了 Valgrind 报告的 "definitely lost", 并且手动在库里搜索 -
如果报告的所有错误都和该库无关，那么它就是安全的)</sub>

除此之外，与 Flutter 的集成也是通过 CI 完成。确保了使用该库的 Flutter 应用不会产生问题。

大多数代码都是 safe Rust. `unsafe` 代码主要来自 `support::box_from_leak_ptr` 和
`support::vec_from_leak_ptr`. 他们被用于处理指针和数组，我会遵循高票数的答案和官方文档编写相关代码。

我在我的个人 Flutter 项目 (`yplusplus`, or `why++`) 里非常频繁的使用到了该库。那些 app
已经用于生产环境，并且运行非常稳定，如果我自己观察到了任何问题，我会修复相关 bug。

CI 同时会运行 `run_codegen` 工作流，确保生成的代码可以通过编译。最后，CI 还会运行代码格式化和 linter(`fmt`,
`clippy`, `dart analyze`, `dart format`), linter 也能捕获到一些常见错误。
