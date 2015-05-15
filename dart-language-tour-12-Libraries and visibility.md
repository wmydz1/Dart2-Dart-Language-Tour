##库和可见性
import,part,library指令可以帮助创建一个模块化的，可共享的代码库。库不仅提供了API，还提供隐私单元：以下划线（_）开头的标识符只对内部库可见。每个Dartapp就是一个库，即使它不使用库指令。

库可以分布式使用包。见[Pub Package and Asset Manager]()中有关pub(SDK中的一个包管理器）。

###使用库

使用 import 来指定如何从一个库命名空间用于其他库的范围。

例如，Dart Web应用一般采用这个库[dart:html](http://api.dartlang.org/html.html)，可以这样导入：
```dart
import 'dart:html';
```
唯一需要 import 的参数是一个指向库的 URI。对于内置库，URI中具有特殊dart:scheme。对于其他库，你可以使用文件系统路径或package:scheme。包 *package*：scheme specifies libraries ，如pub工具提供的软件包管理器库。例如：
```dart
import 'dart:io';
import 'package:mylib/mylib.dart';
import 'package:utils/utils.dart';

```
	
    注：URI代表统一资源标识符。网址（统一资源定位器）是一种常见的URI的。

#### 指定库前缀

如果导入两个库是有冲突的标识符，那么你可以指定一个或两个库的前缀。例如，如果 library1 和 library2 都有一个元素类，那么你可能有这样的代码：
```dart
import 'package:lib1/lib1.dart';
import 'package:lib2/lib2.dart' as lib2;
// ...
var element1 = new Element(); // 使用lib1里的元素
var element2 =
    new lib2.Element();       // 使用lib2里的元素
```

#### 导入部分库

如果想使用的库一部分，你可以选择性导入库。例如：

```dart
// 只导入foo库
import 'package:lib1/lib1.dart' show foo;

//导入所有除了foo
import 'package:lib2/lib2.dart' hide foo;
```

#### 延迟加载库

延迟(deferred)加载（也称为延迟(lazy)加载）允许应用程序按需加载库。下面是当你可能会使用延迟加载某些情况：

+ 为了减少应用程序的初始启动时间；
+ 执行A / B测试-尝试的算法的替代实施方式中；
+ 加载很少使用的功能，例如可选的屏幕和对话框。
	
    
    警告：延迟加载是先在1.6实现的新功能。如果你使用它，你发现任何执行问题，[请让我们知道](http://dartbug.com/)。

为了延迟加载一个库，你必须使用 deferred as 先导入它。

```dart
import 'package:deferred/hello.dart' deferred as hello;
```

当需要库时，使用该库的调用标识符调用 LoadLibrary（）。
```dart
greet() async {
  await hello.loadLibrary();
  hello.printGreeting();
}
```
在前面的代码，在库加载好之前，await关键字都是暂停执行的。有关 async 和 await 见 asynchrony support 的更多信息。

您可以在一个库调用 LoadLibrary（） 多次都没有问题。该库也只被加载一次。

当您使用延迟加载，请记住以下内容：

+ 延迟库的常量在其作为导入文件时不是常量。记住，这些常量不存在，直到迟库被加载完成。
+ 你不能在导入文件中使用延迟库常量的类型。相反，考虑将接口类型移到同时由延迟库和导入文件导入的库。
+ Dart隐含调用LoadLibrary（）插入到定义deferred as namespace。在调用LoadLibrary（）函数返回一个Future。

#### 库的实现
用 library 来来命名库，用part来指定库中的其他文件。
	注意：不必在应用程序中（具有顶级main（）函数的文件）使用library，但这样做可以让你在多个文件中执行应用程序。

#####声明库
利用library identifier（库标识符）指定当前库的名称：

```dart
// 声明库，名ballgame
library ballgame;

// 导入html库
import 'dart:html';

// ...代码从这里开始...
```

#####关联文件与库

添加实现文件，把part fileUri放在有库的文件，其中fileURI是实现文件的路径。然后在实现文件中，添加部分标识符（part of identifier），其中标识符是库的名称。下面的示例使用的一部分，在三个文件来实现部分库。

第一个文件，ballgame.dart，声明球赛库，导入其他需要的库，并指定ball.dart和util.dart是此库的部分：


```dart
library ballgame;

import 'dart:html';
// ...其他导入在这里...

part 'ball.dart';
part 'util.dart';

// ...代码从这里开始...
```

第二个文件ball.dart，实现了球赛库的一部分：

```dart
part of ballgame;

// ...代码从这里开始...
```
第三个文件，util.dart，实现了球赛库的其余部分：

```dart
part of ballgame;

// ...Code goes here...
```

#####再导出库(Re-exporting libraries)

可以通过再导出部分库或者全部库来组合或重新打包库。例如，你可能有实现为一组较小的库集成为一个较大库。或者你可以创建一个库，提供了从另一个库方法的子集。
```dart
// In french.dart:
library french;

hello() => print('Bonjour!');
goodbye() => print('Au Revoir!');

// In togo.dart:
library togo;

import 'french.dart';
export 'french.dart' show hello;

// In another .dart file:
import 'togo.dart';

void main() {
  hello();   //print bonjour
  goodbye(); //FAIL
}
```