##泛型
如果你在API文档寻找基本数组类型或者[List](https://api.dartlang.org/apidocs/channels/stable/dartdoc-viewer/dart:core.List)类型，你将会看到该类型实际上为List`<E>`,其中<...>标记表示此表为一个泛型类型（或为参数化结构）—— 一种含有正规类型参数的类型。按照惯例，类型变量通常为单字符名称，例如E,T,S,K,以及V。

###为何要使用泛型？
因为在Dart中类型是可选的，你不一定使用泛型。或许你想用，可是，因为一些相同的原因你会想在代码中使用其他的类型：这些类型（泛型或者其他类型）可以注释你的文档以及代码，使你的意图更加清晰。
比如，如果你打算使用一个仅仅包含字符串的List，你可以声明它为List`<String>`（可理解为“字符串类型组成的List”），通过这种方式，你的程序员同事，以及你的工具（比如Dart编辑器和调试模式下的Dart虚拟机）能检测到将一个非字符串的变量分配到List中很可能是错误的，这里给出一个样例：  

~~~Dart   
var names = new List<String>();   
names.addAll([‘Seth’,’Kathy’,’Lars’]);  
//...   
names.add(42); //Fails in checked mode (succeeds in production mode).  
~~~   
另外一个使用泛型的原因是为了减少代码的重复。泛型可以让你能共享多个类型的一个接口和实现方式，它在调试模式以及静态分析的错误预警中仍然很有优势。举个例子，当你在创建一个接口来缓存一个对象时： 
  
~~~
abstract class ObjectCache{   
object getByKey(String key);   
setByKey(String key,Object value);   
}   
~~~   
你发现你想要一个字符串专用的接口，所以你创建了另外一个接口：

~~~
abstract class StringCache{
string getByKey(String key);
setByKey(String key,String value);
}
~~~
接下来，你决定你想要一个这种接口的数字专用的接口...你想到了这个方法.   
泛型类型可以减少你创建这些接口的困难。取而代之的是，你只需要创建一个带有一个类型参数的接口即可：

~~~
abstract class Cache<T>{
T getByKey(String key);
setByKey(String key,T value);
}
~~~
在这个代码中，T是一个替代类型，即占位符，你可以将他视为后续被开发者定义的类型。

###使用集合常量
Lis常量以及map常量都能被参数化，参数常量就像你已经见过的常量那样，除非你在左
方括号之前添加`<type>`(对于List）或者`<keyType,valuetype>`(对于map）。当你需要避免调试模式下的类型警告，你或许可以使用参数常量。这里有一个使用常量类型的例子：

~~~
var names = <String>[‘Seth’,’Kathy’,’Lars’];
var pages = <String,String>{
‘index.html’ : ‘homepage’,
‘robots.txt’ : ‘Hints for web robots’,
‘humans.txt’ : ‘We are people,not machines’
};
~~~
###使用带构造器的参数化类型
为了在使用构造器时详细说明一个或多个类型，将类型放入类名后的三角括号（<...>）中，举个例子：

~~~
var names = new List<String>();
names.addAll([‘Seth’, ‘Kathy’ , ‘Lars’]);
var nameSet = new Set<String>.from(names);
~~~
下列代码创建了一个含有整型的键以及值为View的map：

~~~
var views = new Map<int,view>();
~~~

###泛型集合及其包含的类型
Dart泛型类型是被具体化的，意思就是它们在整个运行时间中都携带着类型信息。举个例子，你可以测试一个集合中的类型甚至是在生产模式中：

~~~
var names = new List<String>();
names.addAll([‘Seth’, ‘Kathy’, ‘Lars’]);
print(names is List<String>); // true
~~~
然而，上述表达式检查的仅仅是集合中的类型--并不是其中的对象。在生产模式下，一个List`<String>`中可能含有一些非字符项，解决方法可以是逐项检查其类型或者在异常处理程序中加入数据项操作代码(查看[异常信息](https://www.dartlang.org/docs/dart-up-and-running/ch02.html#exceptions))。  

**提示**：相反的，在Java中泛型使用erasure，意思就是泛型类型的参数在运行中将会被抹除。在Java中你可以测试一个对象是否是一个表，但是你不能测试它是否是一个List`<String>`.

更多关于泛型的信息，请见[**Optional Types in Dart**](https://www.dartlang.org/articles/optional-types/)

