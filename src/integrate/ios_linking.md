# 链接该项目

在 Xcode 中打开 `ios/Runner.xcodeproj`, 接着把 `$crate/$crate.xcodeproj` 作为一个
_subproject_ 添加。结果大致是这样：

Open `ios/Runner.xcodeproj` in Xcode, then add `$crate/$crate.xcodeproj` as a
_subproject_ of the Runner project. It should look like this:

![proj-tree](ios_proj_tree.png)

Click on the `Runner` root project, then go to the **Build Phases** tab. First,
expand the **Dependencies** phase, and add **$crate-staticlib** for iOS, or
**$crate-cdylib** for MacOS.

![dep-phase](ios_dep_phase.png)

Then, expand the **Link Binary With Libraries** phase, and add
**lib$crate_static.a** for iOS, or **$crate.dylib** for MacOS.

![link-phase](ios_link_phase.png)
