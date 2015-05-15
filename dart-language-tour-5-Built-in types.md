
##内置类型
Dart语言对以下类型的特殊支持：

+ 数字 number
+ 字符串 strings
+ 布尔 booleans
+ 列表 lists（也称为数组arrays）
+ 图 maps
+ 符号 symbols
可以初始化的任何使用文字这些特殊类型的一个对象。例如，*'this is a string'*是字符串常量，而*ture*的是一个布尔值。

因为在 Dart 中，每一个变量是指一个对象，即一个类的实例，通常可以使用构造函数初始化变量的对象实例。一些内置的类型都有自己的构造函数。例如，你可以使用 Map() 构造函数来创建一个映射，使用代码，如 new Map()。

###Numbers

Dart 数字有两种形式：

+ int
整数值，通常应在范围-253到253

+ double
64位（双精度）浮点数，作为指定由IEEE 754制定标准；

无论int和double是num的子类型。该数字类型包括基本运算符，如+， - ，/和*，以及位运算符，例如 >>。 num的类型也是在那里你会发现 abs()，ceil()，和 floor() ，以及其他的方法。如果num及其亚型没有你要找的内容，Math库可能有。

注意：-253到253范围之外的整数，目前在从 Dart 代码生成 JavaScript 中比同样的 Dart 代码在 Dart 虚拟机运行效果不同。其原因是，Dart 中数字可以被指定到具有任意精度的整数，但 JavaScript不可以。详情请参阅[issue 1533](http://dartbug.com/1533)。

整数是没有小数点的数字。以下是定义整数常量的一些例子：

```dart
var x = 1;
var hex = 0xDEADBEEF;
var bigInt = 34653465834652437659238476592374958739845729;
```
如果一个号码包括一个小数，这是一个Double类型的。以下是定义Double文字的一些例子：

```dart
var y = 1.1;
var exponents = 1.42e5;
```
如何把字符串转换成一个数字，反之亦然：
```dart
// String -> int
var one = int.parse('1');
assert(one == 1);

// String -> double
var onePointOne = double.parse('1.1');
assert(onePointOne == 1.1);

// int -> String
String oneAsString = 1.toString();
assert(oneAsString == '1');

// double -> String
String piAsString = 3.14159.toStringAsFixed(2);
assert(piAsString == '3.14');
```

int 类型规定了传统按位移位（<<，>>），与（＆）和或（|）运算符。例如：

```dart
assert((3 << 1) == 6);  // 0011 << 1 == 0110
assert((3 >> 1) == 1);  // 0011 >> 1 == 0001
assert((3 | 4)  == 7);  // 0011 | 0100 == 0111
```

###字符串 Strings

Dart字符串是UTF-16编码单元的序列。可以使用单或双引号来创建一个字符串：
```dart
var s1 = 'Single quotes work well for string literals.';
var s2 = "Double quotes work just as well.";
var s3 = 'It\'s easy to escape the string delimiter.';
var s4 = "It's even easier to use the other delimiter.";
```

你可以通过使用 ${expression} 把一个表达式的值放进字符串。如果表达式是一个标识符，你可以跳过{}。为了获得相应对象的字符串，Dart 调用对象的 toString（）方法。

```dart
var s = 'string interpolation';

assert('Dart has $s, which is very handy.' ==
       'Dart has string interpolation, ' +
       'which is very handy.');
assert('That deserves all caps. ' +
       '${s.toUpperCase()} is very handy!' ==
       'That deserves all caps. ' +
       'STRING INTERPOLATION is very handy!');
```
注：运算符*==*测试两个对象是否是等价的。两个字符串是等价的，如果它们包含的代码单元相同的序列。

可以利用相邻字符串或*+*运算符连接字符串：

```dart
var s1 = 'String ' 'concatenation'
         " works even over line breaks.";
assert(s1 == 'String concatenation works even over '
             'line breaks.');

var s2 = 'The + operator '
         + 'works, as well.';
assert(s2 == 'The + operator works, as well.');
```

另一种方法来创建一个多行字符串：使用三引号用单或双引号：

```dart
var s1 = '''
You can create
multi-line strings like this one.
''';

var s2 = """This is also a multi-line string.""";
```

可以通过带有 r 的前缀来创建一个“raw”的字符串：

```dart
var s = r"In a raw string, even \n isn't special.";
```
可以使用 Unicode 转义代替字符串：

// Unicode 转义工作：[heart]
```dart
// 转义: [heart]
print('Unicode escapes work: \u2665');
```
有关使用字符串的更多信息，请参见[字符串和正则表达式](https://www.dartlang.org/docs/dart-up-and-running/ch03.html#strings-and-regular-expressions)。

###布尔值 booleans

为了表示布尔值，Dart 有一个名为bool的类型。只有两个对象具有 bool 类型：布尔文字，true 和 false。

当Dart需要一个布尔值，仅值 true 被视为真。所有其他值被视为假。不像在 JavaScript 中，值，如1，“aString”，someObject 都视为假的。

例如，请考虑下面的代码，这是有效 JavaScript 代码也是有效的Dart代码：

```dart
var name = 'Bob';
if (name) {
  // JavaScript中会产生打印，而Dart中不会
  print('You have a name!');
}
```
如果将上面代码作为JavaScript代码运行，它将打印 “You have a name!” ，因为名字是一个非空的对象。然而，在Dart在生产模式下运行时，上面的代码不会打印，因为在所有的名字被转换为假（因为 name！= true）。在 DART 运行检查模式，前面的代码抛出一个异常，因为该名称变量不是一个 bool。

下面的代码行为不同的 JavaScript 和 Dart 另一个例子：

```dart
if (1) {
  print('JS prints this line.');
} else {
  print('Dart in production mode prints this line.');
  // 但在checked模式下会抛出一个异常，因为1不是一个boolean
}
```
注意：只有在生产模式，而不是检查模式，前面的两个示例工作。在检查模式下，一个例外是，当需要一个boolean值，而此时一个非布尔时使用，异常会被抛出。
Dart针对布尔值的设计是为了避免可能出现的时候许多值可以被视为真而产生怪异的行为。这意味着，不能使用代码像if（nonbooleanValue），应该明确检查值。例如：
```dart
// 检查一个空字符串.
var fullName = '';
assert(fullName.isEmpty);

// 检查为零.
var hitPoints = 0;
assert(hitPoints <= 0);

// 检查是否为空.
var unicorn;
assert(unicorn == null);

// 检查NaN.
var iMeantToDoThis = 0 / 0;
assert(iMeantToDoThis.isNaN);
```

###List列表

几乎每一个编程语言中最常见的集合就是数组或有序组对象了。在Dart，数组是列表对象，所以我们通常只是将其称为lists。

Dart列表书面上看起来像JavaScript数组常量。
这里有一个简单的Dart列表：

```dart
var list = [1, 2, 3];
```
列表使用从零开始的索引，其中0为第一个元素,list.length-1是最后一个元素的索引。你可以得到一个列表的长度，就像在JavaScript中一样，参阅列表元素：

```dart
var list = [1, 2, 3];
assert(list.length == 3);
assert(list[1] == 2)
```
列表类型有很多方法，方便操纵名单。有关列表的详细信息，请参见[泛型(Generics)](https://www.dartlang.org/docs/dart-up-and-running/ch02.html#generics)和[集合(Collections)](https://www.dartlang.org/docs/dart-up-and-running/ch03.html#collections)。

###图Maps

在一般情况下，一个图（map）是一个对象，相关联的键和值。这两个键和值可以是任何类型的对象。每个键只发生一次，但是可以使用相同的值多次。对于mapDart提供map文字和Map类型支持。

这里有几个简单的Dart图的例子，图用文字创建：
```dart
var gifts = {
// 键            值
  'first' : 'partridge',
  'second': 'turtledoves',
  'fifth' : 'golden rings'
};

var nobleGases = {
//键       值
  2 :   'helium',
  10:   'neon',
  18:   'argon',
};
```
可以使用一个Map构造相同的对象：
```dart
var gifts = new Map();
gifts['first'] = 'partridge';
gifts['second'] = 'turtledoves';
gifts['fifth'] = 'golden rings';

var nobleGases = new Map();
nobleGases[2] = 'helium';
nobleGases[10] = 'neon';
nobleGases[18] = 'argon';
```

添加新键值对到现有的map就像你在JavaScript中：
```
var gifts = {'first': 'partridge'};
gifts['fourth'] = 'calling birds'; // 增加键值对
```
检索map的值(以在 JavaScript 中相同的方式)：
```dart
var gifts = {'first': 'partridge'};
assert(gifts['first'] == 'partridge');
```
如果你寻找的关键词不在图里，则返回空（null）：

```dart
var gifts = {'first': 'partridge'};
assert(gifts['fifth'] == null);
```

使用 .length，以获得map中键值对的数目：

```dart
var gifts = {'first': 'partridge'};
gifts['fourth'] = 'calling birds';
assert(gifts.length == 2);
```
有关映射的更多信息，请参见泛型和图。

###符号 symbols

一个符号对象表示在Dart程序中声明的操作符或标识。你可能不会需要使用这些符号，但他们对于由名字指向的API是很有用的，因为时常要改变的是标识符的名字，而不是标识符的符号。

为了得到符号的标识，使用符号的文本，只是＃后跟标识符：

```dart
#radix
#bar
```
有关符号的详细信息，请参阅[Dart：镜子 - 反射(dart:mirrors-reflection)]()。