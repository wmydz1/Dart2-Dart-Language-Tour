
##一个基础的Dart程序
下面的代码运用了 Dart 的许多基础功能：
```dart
//定义一个函数
printNumber(num aNumber) {
  print('The number is $aNumber.'); // 输出至控制台.
}

// 此处是APP开始执行的地方
main() {
  var number = 42; // 声明并初始化变量
  printNumber(number); // 调用函数
}

```

下面是这个程序的使用，适用于所有（或者说几乎所有）的Dart apps;

```dart
//这是注释
```
使用 //来表示剩下的行是一个注释，也可以使用/*...*/来注释，细节请见[注释（Comments）](https://www.dartlang.org/docs/dart-up-and-running/ch02.html#comments);

**num**

一种变量类型。其他一些内置类型有 String, int 和 bool;

**42**

一个数字，数字是一种编译常量。

**print()**

一个手动的方式来展示输出。


**'...'(或者"...")**

一个字符串；

$variableName (或者 ${expression})
字符串插值：包括一个变量或表达式的字符串，相当于一个字符串内。欲了解更多信息，请参见[字符串](https://www.dartlang.org/docs/dart-up-and-running/ch02.html#strings)。

main()
是一个特殊的、必要、顶级的函数，应用程序开始执行的地方。欲了解更多信息，请参阅[main()函数](https://www.dartlang.org/docs/dart-up-and-running/ch02.html#the-main-function)。

var
一种特殊的方式来声明变量，不用特指变量类型；

	注意：我们的代码参照[Dart风格指南（Dart Style Guide](),例如我们使用了两个空格缩进。
