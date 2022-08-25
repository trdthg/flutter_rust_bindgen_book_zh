# 集成到安卓

设置过程与 [Android setup](../template/setup_android.md) 相同。
所以请继续按照那里的步骤进行。当你完成后，我们将继续修改现有的工具链以适应 Rust。

设置 Cargo 与 Gradle 一起运行的方法有很多，本指南将介绍两种主要方式：任务钩子（hooking onto tasks），以及与 CMake 集成。
