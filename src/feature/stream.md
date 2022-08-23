# Stream 流 / 迭代器

_`Stream` / `Iterator`_

Stream 是什么？简单来说：调用一次，返回多次，类似于 Iterator。

> 译者注：实现了 Future 的迭代器

Flutter 的 [Stream](https://dart.dev/tutorials/language/streams) 是一个功能强大的抽象。

例如，你的 Rust 代码可能在运行一个十分复杂的算法，并且每隔几百毫秒，就能找到一种新的解决方案。在这个情况下，它可以直接将这部分内容回复给
Flutter，并立即渲染到 UI。用户无需等到算法完全结束就能看到部分结果。

至于细节方面，一个带有下面函数签名的 Rust 函数 `fn f(sink: StreamSink<T>, ..) -> Result<()>`
会被翻译为：`Stream<T> f(..)`。

注意：你可以永远持有这个 `StreamSink`，并且自由使用，甚至在 Rust 函数返回后。下面的 logger
例子证明了这点（`create_log_stream` 函数几乎是立即返回，但是你可以在一小时之后使用 `StreamSink`）。

`StreamSink` 可以被放在函数的任何地方。例如 `fn f(a: i32, b: StreamSink<String>)` 和
`fn f(a: StreamSink<String>, b: i32)` 都是合法的。

## 示例

下面的例子只是为了加深你对 Stream 特性的理解。

### Example: 适用于生产环境的 Logger

在我的 app（已经应用在生产环境）里，我使用了下面的策略处理 Rust 日志：使用常规的 Rust 方法记录日志，比如 `info!` 和 `debug!`
宏。接着日志会在两个地方得到处理：一方面是通过不同平台特定的方法打印（就像安卓平台的 Logcat 和 IOS 的 NSLog）另一个是通过 Stream
发送到 Dart 端并进一步处理 (例如保存到文件，或者是发送给服务端等)。

完整的代码可以在这里查看[#486](https://github.com/fzyzcjy/flutter_rust_bridge/issues/486)。

### Example: 简单的 logger

让我们实现了一个简单的日志系统（改编自我在生产环境中使用 `flutter_rust_bridge` 构建的日志系统），Rust 代码可以向 Dart
端发送日志。

Rust 端 `api.rs`:

```rust,noplayground
pub struct LogEntry {
    pub time_millis: i64,
    pub level: i32,
    pub tag: String,
    pub msg: String,
}

// 用于展示的简化代码
// 为了成功编译，你需要一个 OnceCell，或者 Mutex，或者 RwLock
// 更多资料：https://github.com/fzyzcjy/flutter_rust_bridge/issues/398
lazy_static! { static ref log_stream_sink: StreamSink<LogEntry>; }

pub fn create_log_stream(s: StreamSink<LogEntry>) {
    stream_sink = s;
}
```

现在 Rust 编译器应该会向你抱怨 `LogEntry` 没有实现 `IntoDart`。这是符合预期的，因为 `flutter_rust_bridge`
会为你生成相关实现。修复它也很简单再次运行 `flutter_rust_bridge_codegen` 即可

生成的 Dart 代码：

```Dart
Stream<LogEntry> createLogStream();
```

在 Dart 中使用：

```dart
Future<void> setup() async {
    createLogStream().listen((event) {
      print('log from rust: ${event.level} ${event.tag} ${event.msg} ${event.timeMillis}');
    });
}
```

现在我们能够愉快的在 Rust 中用日志记录任何东西：

```rust,noplayground
log_stream_sink.add(LogEntry { msg: "hello I am a log from Rust", ... })
```

当然了，你也可以跟着 Rust 中的 `log` 库去实现一个自己的 logger，只需要在外面包装一层 stream sink，就可以使用标准的 Rust
日志机制，例如 `info!`。我在我在我的项目中就是这么做的。

### Example: 简单定时器

Credits:
[this](https://gist.github.com/Desdaemon/be5da0a1c6b4724f20093ef434959744) and
[#347](https://github.com/fzyzcjy/flutter_rust_bridge/issues/347).

```rust,noplayground
use anyhow::Result;
use std::{thread::sleep, time::Duration};

use flutter_rust_bridge::StreamSink;

const ONE_SECOND: Duration = Duration::from_secs(1);

// can't omit the return type yet, this is a bug
pub fn tick(sink: StreamSink<i32>) -> Result<()> {
    let mut ticks = 0;
    loop {
        sink.add(ticks);
        sleep(ONE_SECOND);
        if ticks == i32::MAX {
            break;
        }
        ticks += 1;
    }
    Ok(())
}
```

然后在 Dart 中使用：

```dart
import 'package:flutter/material.dart';
import 'ffi.dart';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Demo',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: const MyHomePage(title: 'Flutter Demo Home Page'),
    );
  }
}

class MyHomePage extends StatefulWidget {
  const MyHomePage({Key? key, required this.title}) : super(key: key);
  final String title;

  @override
  State<MyHomePage> createState() => _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage> {
  late Stream<int> ticks;

  @override
  void initState() {
    super.initState();
    ticks = api.tick();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text(widget.title),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: <Widget>[
            const Text("Time since starting Rust stream"),
            StreamBuilder<int>(
              stream: ticks,
              builder: (context, snap) {
                final style = Theme.of(context).textTheme.headline4;
                final error = snap.error;
                if (error != null)
                  return Tooltip(
                      message: error.toString(),
                      child: Text('Error', style: style));

                final data = snap.data;
                if (data != null) return Text('$data second(s)', style: style);

                return const CircularProgressIndicator();
              },
            )
          ],
        ),
      ),
    );
  }
}
```
