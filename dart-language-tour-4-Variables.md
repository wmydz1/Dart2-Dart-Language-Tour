
##变量
下面是创建变量并对其赋值的一个例子：
```dart
var name = 'Bob';
```
变量都是引用，变量name包含对一个 String 对象值是 “Bob” 的引用。

###默认值

未初始化的变量具有 null 的初始值。即使数字类型变量最初为 null ，因为数字是对象。

```dart
int lineCount;
assert(lineCount == null);
// 变量 (尽管会赋值数值)被初始化为 null.
```

注：assert() 调用在生产模式(production mode)下是被忽略的。在检查模式下，aeesrt(condition) 抛出一个异常，除非条件为真。有关详细信息，请参阅 Assert 部分。

###可选类型
你必须在你的变量声明中添加静态类型选项：

```dart
String name='Bob';
```
添加类型是一种清晰地表达你意图的方式。工具如编译器和编辑器可以使用这些类型来帮助你，通过为错误和代码完成提供漏洞预警和代码补全。

注：本章参照风格指南推荐的使用var,而不是为局部变量做类型标注。

###final 和 const

如果从不打算改变一个变量，使用 final 或者 const 代替 var 或者其他类型。一个 final 变量只能被设置一次；一个 const 变量是一个编译时常数。

被声明为 final 的顶层或类变量第一次使用时被初始化：
```dart
final name = 'Bob'; // Or: final String name = 'Bob';
// name = 'Alice';  // 取消注释会产生一个错误
```

	注：延迟初始化变量最终有助于应用程序启动更快。

使用常量作为要编译的常数变量。如果 const 的变量是在类级别，将其标记为静态常量。 （实例变量不能是const。）如果你声明的变量，设置该值为编译时常数设置，如文字，一个 const 变量，或常数算术运算的结果：

```dart
const bar = 1000000;       //压力单位(dynes/cm2)
const atm = 1.01325 * bar; // 标准大气压
```
