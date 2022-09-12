# Hooking onto tasks

这部分与模板的使用方法相同，也是比较简单的方法。如果你还没有安装 `cargo-ndk`，请继续安装。

```
cargo install cargo-ndk
```

接着，在 `android/app/build.gradle` 的最后添加下面几行：

```gradle
[
    new Tuple2('Debug', ''),
    new Tuple2('Profile', '--release'),
    new Tuple2('Release', '--release')
].each {
    def taskPostfix = it.first
    def profileMode = it.second
    tasks.whenTaskAdded { task ->
        if (task.name == "javaPreCompile$taskPostfix") {
            task.dependsOn "cargoBuild$taskPostfix"
        }
    }
    tasks.register("cargoBuild$taskPostfix", Exec) {
        // Until https://github.com/bbqsrc/cargo-ndk/pull/13 is merged,
        // this workaround is necessary.

        def ndk_command = """cargo ndk \
            -t armeabi-v7a -t arm64-v8a -t x86_64 -t x86 \
            -o ../android/app/src/main/jniLibs build $profileMode"""

        workingDir "../../$crate"
        environment "ANDROID_NDK_HOME", "$ANDROID_NDK"
        if (org.gradle.nativeplatform.platform.internal.DefaultNativePlatform.currentOperatingSystem.isWindows()) {
            commandLine 'cmd', '/C', ndk_command
        } else {
            commandLine 'sh', '-c', ndk_command
        }
    }
}
```

注意 ANDROID\_NDK 变量，这是一个 Gradle 属性，它指向你安装的 Android NDK 目录。你可以硬编码这个值，但最可靠的方法是写入到
`~/.gradle/gradle.properties`：

```
ANDROID_NDK=(path to NDK)
```
