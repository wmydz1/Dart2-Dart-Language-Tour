
##重要的概念

当学习Dart语言的时候，把这些事实和概念记在脑子里：
+ 每个变量都是一个对象，每个对象是一个类的实例。甚至数字，函数，和null都是对象。所有对象都继承自[Object](http://api.dartlang.org/dart_core/Object.html)类

+ 指定静态类型（如num前面的例子中）讲清意图，用 tools 开启静态检查，但它是可选的。 （可能注意到当你调试代码，没有指定类型的变量会得到一个特殊的类型： dynamic ）

+ Dart解析所有的代码运行之前。可以对Dart提供提示，例如，通过使用类型或编译时间常数来捕获错误或帮助代码运行更快。

+ Dart支持顶级函数（如main()）也支持类或者对象（静态和实例方法分别支持）里的函数。还可以在函数里创建函数（嵌套或局部功能）。

+ 类似的，Dart支持顶级变量，以及依赖于类或对象（静态变量和实例变量）变量。实例变量有时被称为域或属性。

+ 与Java不同，Dart不具备关键字public，protected和private。如果一个标识符以下划线（_）开始，那么它和它的库都是私有的。有关详细信息，请参阅 [Libraries and visibility](https://www.dartlang.org/docs/dart-up-and-running/ch02.html#libraries-and-visibility)。

+ 标识符可以字母或（_）开始，或者是字符加数字的组合开头。

+ 有时，判断是一个表达式还是一个语句会很重要，所以我们要准确了解这两个单词。

+ Dart tools可报告两类问题：警告(warning)和错误(error)。警告只是迹象表明，代码可能无法正常工作，但他们不会阻止程序的执行。错误可以是编译时或运行时,编译时的错误阻止代码执行;当代码执行时一个运行时的错误会导致一个[异常（exception）](https://www.dartlang.org/docs/dart-up-and-running/ch02.html#exceptions)被抛出。

+ Dart有两种运行模式：生产 (production) 和检查 (checked) 。我们建议在检查模式开发和调试，并将其部署到生产模式。
 + Production mode是Dart程序一个速度优化的默认运行模式。Production mode忽略[断言语句（assert statements）](https://www.dartlang.org/docs/dart-up-and-running/ch02.html#assert)和静态类型。

 + Checked mode 是开发人员友好的方式，可以帮助你在运行时捕捉一些类型的错误。例如，如果分配一个非数字来声明为一个 num 变量，然后在检查模式会抛出异常。

