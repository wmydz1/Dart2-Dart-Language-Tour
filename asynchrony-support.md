#异步的支持
Dart 添加了一些新的语言特性用于支持异步编程。最通常使用的特性是 `async` 方法和 `await` 表达式。Dart 的库有很多方法返回 `Future` 和 `Stream` 的对象。这些方法是异步的。它们在建立一个可能的耗时操作比如 ` I/O` 操作之后返回，无需等待操作完成

当你需要使用 `Future` 来表示一个值时，你有两个选择。  

- 使用 `async` 和 `await`
- 使用 `Future API`
  
同样的，当你需要从 `Stream` 获取值的时候，你有两个选择。  

- 使用 `async` 和一个异步的 for 循环 (`await for`)
- 使用 ` Stream API`

代码使用 `async` 和 `await` 是异步的，它看起来很像同步的代码。比如这里有一些代码使用 `await` 等待一个异步函数的执行结果：  

`await lookUpVersion()`  

使用 `await`，代码必须在用 `async` 标记

```
checkVersion() async {
  var version = await lookUpVersion();
  if (version == expectedVersion) {
    // Do something.
  } else {
    // Do something else.
  }
}
```

你可以使用 `try`, `catch`, 和 `finally` 处理和清理使用 `await` 的代码。

```
try {
  server = await HttpServer.bind(InternetAddress.LOOPBACK_IP_V4, 4044);
} catch (e) {
  // React to inability to bind to the port...
}
```

##声明异步函数
一个异步函数是一个用 `async` 修饰符标记的函数。虽然一个异步函数可能执行耗时操作，它可以在任何方法体执行之前返回。

```
checkVersion() async {
  // ...
}

lookUpVersion() async => /* ... */;

```

在函数中添加关键字 `async ` 使得它返回一个 `Future`，比如想想这个函数异步，它返回一个字符串。  

`String lookUpVersionSync() => '1.0.0';`  

如果你想更改它成为异步方法-因为在以后的实现中将会非常耗时-它的返回值是一个 `Future` 。

`Future<String> lookUpVersion() async => '1.0.0';`

请注意函数体不需要使用 `Future API`，如果必要 Dart 将会自己创建 `Future` 对象。

## 与 Futures 使用 await 表达式

一个 `await`表达式具有以下形式

`await expression`

在异步方法中你可以使用 `await` 多次。比如，下列代码等待了函数的执行结果三次。

```
var entrypoint = await findEntrypoint();
var exitCode = await runExecutable(entrypoint, args);
await flushThenExit(exitCode);
```

在 `await 表达式`， `表达式` 的值通常是一个 `Future` 对象；如果不是，这个值会自动转成一个 `Future`，一个 `Future` 对象表明希望返回一个对象。`await 表达式` 的值就是返回的对象。在对象可用之前，await 表达式将会一直处于暂停状态。

**如果 `await` 没有起作用，确认它是一个异步方法。**比如，在你的 `main()` 函数里面使用`await` ，`main()` 函数体必须被 `async` 标记：

```
main() async {
  checkVersion();
  print('In main: version is ${await lookUpVersion()}');
}
``` 

##与 Streams 使用异步循环

一个异步循环具有一下形式：

```
await for (variable declaration in expression) {
  // Executes each time the stream emits a value.
}
```  

`表达式` 的值必须有 `Stream` 类型。执行过程如下：  

1. 在 stream 发出一个值之前等待
2. 执行 for 循环的主体，把变量设置为发出的值。
3. 重复 1 和 2，直到 Stream 关闭


如果要停止监听 stream ，你可以使用 `break` 或者 `return` 声明，跳出循环取消来自 `stream` 订阅 。

**如果一个异步 for 循环没有正常运行，确认它是一个异步方法。** 比如，使用异步的 for 循环你的应用的 `main()` 方法，main() 的方法体必须被 `await` 标记。

```
main() async {
  ...
  await for (var request in requestServer) {
    handleRequest(request);
  }
  ...
}
```    

更多关于异步编程的信息，看 ` dart:async` 库部分的介绍。你也可以看文章 [Dart Language Asynchrony Support: Phase 1 ](https://www.dartlang.org/articles/await-async/)和 [Dart Language Asynchrony Support: Phase 2](https://www.dartlang.org/articles/beyond-async/), 和 [the Dart language specification](https://www.dartlang.org/docs/spec/)  






