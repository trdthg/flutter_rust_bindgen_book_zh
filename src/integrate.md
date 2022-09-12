# 集成到现有项目

这一部分是中级教程，介绍了如何将 Rust 与现有的 Flutter 项目集成。如果您是 Rust 初学者，或者只是在配置开发环境，我建议你先去看
[the template tour](template/tour.md) 章节，学习 `flutter run` 背后的部分。

在进入教程之前，为了使集成更简单，请更新你的 Flutter SDK，如果可以的话，也请您重新构建项目。

**注意:** 虽然过程很复杂，但是绝大多数原因都不是来源于该库本身，使用原始的 Rust/Flutter FFI 和它一样复杂。换句话说，真正耗时的是搭建
Dart / Flutter + Rust 工具链。
