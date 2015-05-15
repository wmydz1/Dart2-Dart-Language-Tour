# 元数据

使用元数据来给你的代码提供附加信息。

元数据注解以 *@* 字符开头，后面跟一个编译时的常量引用（例如 *deprecated*）或者调用常量构造器的语句。

所有的 Dart 代码中支持三个注解：*@deprecated*，*@override* 和*@proxy*。*@override* 和*@proxy*的用法示例，请查看[类的继承](#)。以下是 *@deprecated* 用法的示例：

```
class Television {
  /// _Deprecated: Use [turnOn] instead._
  @deprecated
  void activate() {
    turnOn();
  }

  /// Turns the TV's power on.
  void turnOn() {
    print('on!');
  }
}
```

你可以定义你自己的元数据注解。下面的例子定义了一个有两个参数的 *@todo* 注解：

```
library todo;

class todo {
  final String who;
  final String what;

  const todo(this.who, this.what);
}
```

下面是使用 *@todo* 注解的例子：

```
import 'todo.dart';

@todo('seth', 'make this do something')
void doSomething() {
  print('do something');
}
```

元数据可以出现在库、类、*typedef*、类型参数、构造器、工厂、函数、属性、参数、变量声明、*import* 或 *export* 指令之前。你可以在运行时通过反射来取回元数据。
