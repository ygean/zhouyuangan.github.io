# Annotating Your Code with Types

## 强类型 or 弱类型

python是一门更倾向于强类型的语言，但又不能完全划定界限到强类型语言之内。在一些操作符场景下，不同python类型变量不能相互操作。

```python
>>>[] + {}
TypeError: can only concatenate list (not "dict") to list
```
python的列表和字典显然不支持+操作，python解释器在执行代码后，抛出TypeWrror来警告开发者。


## Dynamic typing

由于python变量在运行中，可以随意改变类型，这给写出健壮python代码带来了麻烦，但这也是python语言能带来的开发体验上的便利。

```python

>>> a = 5
>>> a = "string"
>>> a
"string"
>>> a = tuple()
>>> a
()

```

注意：如果通过类型标注（type annotation）来约束变量，也不会起作用。

```python
>>> a: int = 5
>>> a = "string"
>>> a
"string"
```

此时，`a`尽管通过int标识，但是依然可以在运行时，对`a`进行赋值，并改变了类型；

## Duck Typing

什么是鸭子类型？这个如果通过例子来解释，我想接下来的例子是个人认为最佳的。

```python
from typing import Iterable

def print_items(items: Iterable):
    for item in items:
    print(item)

print_items([1,2,3])
print_items({4, 5, 6})
print_items({"A": 1, "B": 2, "C": 3})

```
无论传入参数是list，还是dict，`print_items`依然可以完成其预设功能，这是因为在这传入的不同类型的变量，都实现了`__iter__`接口函数，这使得`for`依然可以对其进行遍历。

由此可见，鸭子类型应该是描述了，在编程语言中任何一个对象和实体实现了统一（同一）的接口的编程思想；让不同的对象（类型）具备了相同的接口，可以完成相同的功能，并能发挥不同对象（类型）的特性；

