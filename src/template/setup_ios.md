# iOS 设置

iOS 需要一些额外的交叉编译目标：

```bash
# 64 bit targets (真机 & 模拟器):
rustup target add aarch64-apple-ios x86_64-apple-ios
# New simulator target for Xcode 12 and later
rustup target add aarch64-apple-ios-sim
# 32 bit targets (你应该不需要这个):
rustup target add armv7-apple-ios i386-apple-ios
```
