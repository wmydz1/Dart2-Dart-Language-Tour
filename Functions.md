#函数
下面是一份关于如何使用函数的示例：

```
void  printNumber(num number) {
	print('The number is $number.');
}
```

尽管上面这个指导的格式声明了参数和返回值的类型，实际上你可以不这么做:

```
printNumber(num number) { // 没有声明类型也是可以的
	print('The number is $number.');
}
```

对于仅含有一个表达式的方法，你可以使用一种简写的语法：

```
void printNumber(num number) =>
	print('The number is $number.');
```

`=> 表达式;`语法是`{ return 表达式 }`的简写。在`printNumber()`方法中，这个表达式调用了顶级函数`print()`。

>注意：只有一个表达式能够在箭头符（=>）和分号（;）之间出现，语句是不可以这样使用的。比如，你不能把 if 语句放在这两个符号之间，但是一个三元运算符（?:）是可以的。
>

调用函数的方法如下：

`printNumber(123)`

一个函数可以有两种类型的参数：必要参数和可选参数。所有的必要参数都应放在可选参数之前，当必要参数已经全部列出时，才能在后面加入可选参数。

##可选参数
可选参数可以是可选位置参数或者可选命名参数，但不能既是可选位置参数又是可选命名参数。

这两种可选参数都可以定义默认值。但是默认值必须是编译时的常量，比如字面值。如果没有为之提供默认值，那么该参数的默认值将会是 null。

###可选命名参数
在调用函数的时候，你可以通过`paraName: Value`的形式使用有命名的参数。比如：

```enableFlags(bold: true, hidden: false);```

当定义一个函数的时候，使用`{param1, param2, ...}`来声明有命名的参数：

```
/// 将 bold 和 hidden 作为你声明的参数的值
enableFlages({bool bold, bool hidden}) {
	// ...
}
```

使用冒号来设置默认值：

```
/// 把 bold 和 hidden 作为参数的值，并将默认值设为 false
enableFlags({bool bold: false, bool hidden: false}) {
	// ...
}

// bold 将会是 true， hidden 则是false
enableFlags(bold:true);
```

###可选位置参数
把一组函数的参数放在`[]`之内可以把它们标记为可选位置参数：

```
Sring say(String from, String msg, [String device]) {
	var result = '$from says #msg';
	if (device != null) {
		result = '$result with a $device';
	}
	return result;
}
```

下面是不使用可选参数调用上述方法的一个实例：

```
assert(say('Bob', 'Howdy') == 'Bob says Howdy');
```

接下来则是使用可选参数调用的实例：

```
assert(say('Bob', 'Howdy', 'smoke signal') == 
	'Bob says Howdy with a smoke signal');
```

可选位置参数使用`=`来声明默认值：

```
String say(String from, String msg,
	[String device = 'carrier', String mood]) {
	var result = '$from says $msg';
	if (device != null) {
	    result = '$result (in a $mood mood)';
	}
	return result;
}

assert(say('Bob', 'Howdy') == 
	'Bob says Howdy with a carrier pigeon');
```

##main函数
每一个应用都必须有一个顶级函数`main()`，这个函数就是整个应用的入口函数。`main()`函数返回值类型为`void`并且有一个可选参数`List<String>`。 

下面是一份关于网络应用的`main()`函数示例：

```
void main() {
	querySelector("#sample_text_id")
		..text = "Click me!"
		..onClick.listen(reverseText);
}
```

>提示：代码前的`..`操作符是级联操作符，用于允许用户在一个对象上实现多个操作。更多关于级联操作符的内容请见[Classes](./Classes.md)。
>

下面是一个命令行应用的带参数的`main()`函数示例：

```
// 这个应用应该在命令行中这样启动：
// dart args.dart 1 test
void main(List<String> arguments) {
	print(arguments);
	
	assert(arguments.length == 2);
	assert(int.parse(arguments[0] == 1);
	assert(arguments[1] == 'test');
}
```

你可以在[args library](https://pub.dartlang.org/packages/args)上了解如何定义和分析命令行参数。

##作为对象的函数
你可以把一个函数当做参数传给另一个函数。比如：

```
printElement(element) {
	print(element);
}

var list = [1, 2, 3];

// 将 printElement 作为参数传递给其他函数
list.forEach(printElement);
```

你也可以把一个函数定义为一个变量，就像下面这样：

```
var loudify = (msg) => '!!! ${msg.toUpperCase()} !!!';
assert(loudify('hello') == '!!! HELLO !!!);
```

###语法作用域
Dart 是语法作用域型的语言，也就是说变量的生命周期是genuine代码的布局静态决定的。你可以“在大括号之外追溯”来看一下变量是否存在于这个区域中。

下面是一份关于嵌套的带参函数在不同的作用域等级上的示例：

```
var topLevel = true;

main() {
	var indideMain = true;
	
	myFunction() {
		var insideFunction = true;
		
		nestedFunction() {
			var insideNestedFunction = true;
			
			assert(topLevel);
			assert(insideMain);
			assert(insideFunction);
			assert(insideNestedFunction);
		}
	}
}
```

请留意`nestedFunction()`是怎样使用不同作用域上的变量的，最好从最内层开始一直分析到最外层。

###语法的封闭性
封闭指的是一个函数可以访问其语法作用域内的变量，即使这个函数是在变量本身的作用域之外被调用的。

函数内部会包含在临近作用域内所定义的变量。在下一个示例中，`makeAdder()`捕获了变量`addBy`。不管返回的函数在哪里被调用，它都可以使用`addBy`。

```
/// 返回一个把 addBy 作为参数的函数
Function makeAdder(num addBy) {
	return (num i) => addBy + 1;
}

main() {
	// 创建一个加2的函数
	var add2 = makeAdder(2);
	// 创建一个加4的函数
	var add4 = makeAdder(4);
	
	assert(add2(3) == 5);
	assert(add4(3) == 7);
}
```

##函数的等价性测试
下面是关于顶级函数、静态方法和实例方法的等价性测试：

```
foo() {} // 一个顶级函数

class SomeClass {
	static void bar() {} // 一个静态方法
	void baz() {} // 一个示例方法
}

main() {
	var x;
	
	// 比较顶级函数
	x = foo;
	assert(A.bar == x);
	
	// 比较实例方法
	var v = new A(); // A的实例1
	var w = new A(); // A的实例2
	var y = w;
	x = w.baz;
	
	// 这些封闭引用了相同的示例对象（A的实例2）
	// 所以它们是等价的
	assert(y.baz == x);
	
	// 这些封闭引用的十不同实例，所以它们不等价
	aessert(v.baz != w.baz);
}
```

##返回值
所有的函数都有返回值。如果没有定义返回值，那么语句`return null`将会隐式地加到函数体的最后。