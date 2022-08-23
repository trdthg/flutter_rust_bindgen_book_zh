# Handler

默认情况下，frb 使用 `DefaultHandler`，你可以实现你自己的 `Handler` 做你想做的事情。首先，你需要在 Rust 文件中创建一个名为
`FLUTTER_RUST_BRIDGE_HANDLER` 的变量（可能会用到 `lazy_static`）。接着，你不一定需要创建一个新的实现了
`Handler` 的结构体，只需要利用现有的 `SimpleHandler`，并自定义它的泛型参数，例如`Executor`。

## 示例

### Example: 除了 Dart 之外，同时向你的后端报告错误

```rust,noplayground
pub struct MyErrorHandler(ReportDartErrorHandler);

impl ErrorHandler for MyErrorHandler {
    fn handle_error(&self, port: i64, error: handler::Error) {
        send_error_to_your_backend(&error);
        self.0.handle_error(port, error)
    }

    ...
}
```

### Example: 记录执行开始和结束的时间

```rust,noplayground
pub struct MyExecutor(ThreadPoolExecutor<MyErrorHandler>);

impl Executor for MyExecutor {
    fn execute<TaskFn, TaskRet>(&self, wrap_info: WrapInfo, task: TaskFn) {
        let debug_name_string = wrap_info.debug_name.to_string();
        self.thread_pool_executor
            .execute(wrap_info, move |task_callback| {
                Self::log_around(&debug_name_string, move || task(task_callback))
            })
    }
}

impl MyExecutor {
    fn log_around<F, R>(debug_name: &str, f: F) -> R where F: FnOnce() -> R {
        let start = Instant::now();
        debug!("(Rust) execute [{}] start", debug_name);
        let ret = f();
        debug!("(Rust) execute [{}] end delta_time={}ms", debug_name, start.elapsed().as_millis());
        ret
    }
}
```
