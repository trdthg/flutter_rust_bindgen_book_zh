# Using dummy headers

`flutter_rust_bridge_codegen` 会创建一个 C 头文件，里面列出了 Rust 库导出的所有符号，我们需要使用它确保 Xcode
不会将符号去除。

在项目中添加 `ios/Runner/bridge_generated.h` (或者
`macos/Runner/bridge_generated.h`)，你可以把文件直接拖到项目文件夹中或者点击菜单上的 **Add Files to
"Runner"...** .

如果它还没有出现，请切换到 **Build Phases** 标签页，把 **bridge_generated.h** 文件拖到 **Copy Bundle
Resources**。

## iOS

接下来，在 `ios/Runner/Runner-Bridging-Header.h` 中添加：

```diff
+#import "bridge_generated.h"
```

在 `ios/Runner/AppDelegate.swift` 中添加：

```diff
 override func application(
     _ application: UIApplication,
     didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?
 ) -> Bool {
+    let dummy = dummy_method_to_enforce_bundling()
+    print(dummy)
     ..
 }
```

这里调用 `dummy_method_to_enforce_bundling()`
并打印返回值的步骤非常重要（类似于上面的例子），否则最终的符号还是可能被去除。

## MacOS

Flutter 在 MacOS 上默认不使用符号，我们需要添加我们自己的。在 **Build Settings** 标签页中，把 **Objective-C
Bridging Header** 设置为 **Runner/bridge_generated.h**

最后，在 `macos/Runner/AppDelegate.swift` 文件的某个地方使用一下
`dummy_method_to_enforce_bundling` , 只要 Xcode 不把它当作 dead code 就行。
