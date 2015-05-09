#Typedefs

在 Dart 中，方法是对象，就像字符串和数字是对象。typedef ,或者函数类型别名，给函数类型一个你可以声明字段和返回类型的名字。当一个函数类型分配给一个变量的时候，typedef 保留类型信息 。  

思考下面的代码，哪一个没有是用 typedef。

```
class SortedCollection {
  Function compare;

  SortedCollection(int f(Object a, Object b)) {
    compare = f;
  }
}

 // Initial, broken implementation.
 int sort(Object a, Object b) => 0;

main() {
  SortedCollection coll = new SortedCollection(sort);

  // All we know is that compare is a function,
  // but what type of function?
  assert(coll.compare is Function);
}

```

类型信息丢失了，当  `f` 分配到 `compare` 的时候。类型 `f` `(Object, Object)` → `int`(→ 意味着返回的)，然而`compare` 的类型是方法。如果我们更改代码使用显式的名字并保留类型信息，开发者和工具都可以使用这些信息。

```
typedef int Compare(Object a, Object b);

class SortedCollection {
  Compare compare;

  SortedCollection(this.compare);
}

 // Initial, broken implementation.
 int sort(Object a, Object b) => 0;

main() {
  SortedCollection coll = new SortedCollection(sort);
  assert(coll.compare is Function);
  assert(coll.compare is Compare);
}

```  

**请注意** 目前 typedefs 仅限于方法类型，我们希望这个能改变。

因为 typedefs 是简单的别名，它提供一种方式检查任何方法的类型。比如： 

```
typedef int Compare(int a, int b);

int sort(int a, int b) => a - b;

main() {
  assert(sort is Compare); // True!
}
```