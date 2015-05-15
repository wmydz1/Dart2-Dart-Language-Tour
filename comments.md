# 注释

Dart 支持单行注释、多行注释和文档注释。

## 单行注释

单行注释由 ```//``` 开始。每一行中 ```//``` 到行尾之间的内容会被 Dart 编译器忽略。

```
main() {
  // TODO: refactor into an AbstractLlamaGreetingFactory?
  print('Welcome to my Llama farm!');
}
```

## 多行注释

一段多行注释由 ```/*``` 开始，由 ```*/``` 结束。在```/*``` 和 ```*/``` 之间的内容会被 Dart 编译器忽略（除非他们是文档注释；请看下面的部分）。多行注释可以嵌套。

```
main() {
  /*
   * This is a lot of work. Consider raising chickens.

  Llama larry = new Llama();
  larry.feed();
  larry.exercise();
  larry.clean();
   */
}
```

## 文档注释

文档注释是由 ```///``` 或 ```/**``` 开始的多行或单行注释。在连续的行上使用 ```///``` 的效果等同于多行注释。

在一段文档注释中，Dart 编译器忽略所有除括号内的文本。你可以使用括号来引用类、方法、属性、顶级变量、函数和参数。括号中的名字会在被文档化程序元素的词法范围内解析。

下面是一个引用了其它类和参数的文档注释的例子：

```
/// A domesticated South American camelid (Lama glama).
///
/// Andean cultures have used llamas as meat and pack
/// animals since pre-Hispanic times.
class Llama {
  String name;

  /// Feeds your llama [Food].
  ///
  /// The typical llama eats one bale of hay per week.
  void feed(Food food) {
    // ...
  }

  /// Exercises your llama with an [activity] for
  /// [timeLimit] minutes.
  void exercise(Activity activity, int timeLimit) {
    // ...
  }
}
```

在生成的文档中， ```[food]``` 变成了指向 Food 类的 API 文档连接。

为了转换 Dart 代码并生成 HTML 文档，你可以使用 SDK 的[文档生成器](https://www.dartlang.org/tools/dartdocgen/)。生成文档的示例，请参阅 [Dart API 文档](http://api.dartlang.org/)。关于如何组织你的文档，请参阅[文档注释准则](https://www.dartlang.org/articles/doc-comment-guidelines/)。
