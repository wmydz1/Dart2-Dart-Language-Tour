
##关键词
下面表格列出了Dart 语言的关键词；

|      |           | |||
| ------------- |:-------------:| -----:| ---:|---:|
| abstract <sup>1</sup> | continue  | false| new | this |
|as <sup>1</sup>| default| final|null|throw|
|assert|deferred <sup>1</sup>| finally|operator <sup>1</sup>|true|
|async <sup>2</sup>|do|for|part <sup>1</sup>|try|
|async* <sup>2</sup>| dynamic <sup>1</sup>| get <sup>1</sup>|rethrow|typedef <sup>1</sup>|
|await <sup>2</sup>|else|if|return|var|
|break|enum|implements <sup>1</sup>|set <sup>1</sup>|void|
|case|export <sup>1</sup>|import <sup>1</sup>|static <sup>1</sup>|while|
|catch|external <sup>1</sup>|in|super|with|
|class|extends|is|switch|yield <sup>2</sup>|
|const|factory<sup>1</sup>|library <sup>1</sup>|sync* <sup>2</sup>|yield* <sup>2</sup>|
 
+ 上标1的单词是内置的标识符(built-in identifiers)。避免使用表格内的标识作为符标识，而且从来不使用它们作为类(class)或类型(type)的名称。内置标识符存在，以方便从 JavaScript 到 Dart 的移植。例如，如果一些JavaScript代码中有一个名为工厂的变量，当你将代码移植到 Datr 中，你不必重新命名它。

+ 上标2的单词是的Dart1.0版本之后添加异步支持较新的、有限的保留字。不能使用async，await，或yield作为在标有async，或sync的任何函数体的标识符。欲了解更多信息，请参见[异步性支持(Asynchrony support)](https://www.dartlang.org/docs/dart-up-and-running/ch02.html#asynchrony)。

+  在关键字表中的所有单词都是保留字。不能使用保留字作为标识符。
 
