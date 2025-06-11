---
title: Python
date: 2020-12-23 18:41:20
background: bg-[#436b97]
tags:
  - 脚本
  - 解释型
categories:
  - 编程
intro: |
  [Python](https://www.python.org/) 速查表是 Python 3 编程语言的单页参考表。
plugins:
  - copyCode
  - runCode
---

## 入门

### 简介

- [Python](https://www.python.org/) _(python.org)_
- [Python 文档](https://docs.python.org/3/index.html) _(docs.python.org)_
- [X分钟学习Python](https://learnxinyminutes.com/docs/python/) _(learnxinyminutes.com)_
- [Python中的正则表达式](/regex#regex-in-python) _(r3f.cn)_

### Hello World

```python
>>> print("Hello, World!")
Hello, World!
```

Python 中著名的 "Hello World" 程序

### 变量

```python
age = 18      # age is of type int
name = "John" # name is now of type str
print(name)
```

Python 不能在没有赋值的情况下声明变量。

### 数据类型 {.row-span-2}

|                                    |          |
| ---------------------------------- | -------- |
| `str`                              | 文本     |
| `int`, `float`, `complex`          | 数字     |
| `list`, `tuple`, `range`           | 序列     |
| `dict`                             | 映射     |
| `set`, `frozenset`                 | 集合     |
| `bool`                             | 布尔     |
| `bytes`, `bytearray`, `memoryview` | 二进制   |

参见: [数据类型](#python-built-in-data-types)

### 字符串切片

```python
>>> msg = "Hello, World!"
>>> print(msg[2:5])
llo
```

参见: [字符串](#python-strings)

### 列表

```python
mylist = []
mylist.append(1)
mylist.append(2)
for item in mylist:
    print(item) # prints out 1,2
```

参见: [列表](#python-lists)

### If Else

```python
num = 200
if num > 0:
    print("num is greater than 0")
else:
    print("num is not greater than 0")
```

参见: [流程控制](#python-flow-control)

### 循环

```python
for item in range(6):
    if item == 3: break
    print(item)
else:
    print("Finally finished!")
```

参见: [循环](#python-loops)

### 函数

```python
>>> def my_function():
...     print("Hello from a function")
...
>>> my_function()
Hello from a function
```

参见: [函数](#python-functions)

### 文件处理 {.col-span-2}

```python
with open("myfile.txt", "r", encoding='utf8') as file:
    for line in file:
        print(line)
```

参见: [文件处理](#python-file-handling)

### 算术运算

```python
result = 10 + 30 # => 40
result = 40 - 10 # => 30
result = 50 * 5  # => 250
result = 16 / 4  # => 4.0 (Float Division)
result = 16 // 4 # => 4 (Integer Division)
result = 25 % 2  # => 1
result = 5 ** 3  # => 125
```

`/` 表示 x 和 y 的商，`//` 表示 x 和 y 的向下取整除法，另请参阅
[StackOverflow](https://stackoverflow.com/a/183870/13192320)

### 加等于

```python
counter = 0
counter += 10           # => 10
counter = 0
counter = counter + 10  # => 10

message = "Part 1."

# => Part 1.Part 2.
message += "Part 2."
```

### f-字符串 (Python 3.6+)

```python
>>> website = 'r3f.cn'
>>> f"Hello, {website}"
"Hello, r3f.cn"

>>> num = 10
>>> f'{num} + 10 = {num + 10}'
'10 + 10 = 20'
```

参见: [Python F-字符串](#python-f-strings-since-python-3-6)

## Python 内置数据类型

### 字符串

```python
hello = "Hello World"
hello = 'Hello World'

multi_string = """Multiline Strings
Lorem ipsum dolor sit amet,
consectetur adipiscing elit """
```

参见: [字符串](#python-strings)

### 数字

```python
x = 1    # int
y = 2.8  # float
z = 1j   # complex

>>> print(type(x))
<class 'int'>
```

### 布尔值

```python
my_bool = True
my_bool = False

bool(0)     # => False
bool(1)     # => True
```

### 列表

```python
list1 = ["apple", "banana", "cherry"]
list2 = [True, False, False]
list3 = [1, 5, 7, 9, 3]
list4 = list((1, 5, 7, 9, 3))
```

参见: [列表](#python-lists)

### 元组

```python
my_tuple = (1, 2, 3)
my_tuple = tuple((1, 2, 3))

tupla = (1, 2, 3, 'python')

print(tupla[0])       # Output: 1
print(tupla.count(1)) # 计算出现次数
print(tupla.index(2)) # 查找索引

tupla1 = (1, 2, 3)
tupla2 = ('a', 'b')

len(tuple) → 返回元素数量。
in → 检查元素是否存在于元组中。
Concatenation (+) → 合并两个元组。
Repetition (*) → 重复一个元组。
Slicing (tuple[start:end]) → 提取子元组。

print(len(tupla1))       # Output: 3
print(2 in tupla1)       # Output: True
print(tupla1 + tupla2)   # Output: (1, 2, 3, 'a', 'b')
print(tupla1[1:])        # Output: (2, 3)

# unpacking
a, b, c, d = tupla   # 每个值赋给一个变量

```

与列表类似，但不可变

### 集合

```python
set1 = {"a", "b", "c"}
set2 = set(("a", "b", "c"))
```

唯一项目/对象的集合

### 字典

```python {.wrap}
>>> empty_dict = {}
>>> a = {"one": 1, "two": 2, "three": 3}
>>> a["one"]
1
>>> a.keys()
dict_keys(['one', 'two', 'three'])
>>> a.values()
dict_values([1, 2, 3])
>>> a.update({"four": 4})
>>> a.keys()
dict_keys(['one', 'two', 'three', 'four'])
>>> a['four']
4
```

键值对，类似 JSON 的对象

### 类型转换

#### 整数

```python
x = int(1)   # x will be 1
y = int(2.8) # y will be 2
z = int("3") # z will be 3
```

#### 浮点数

```python
x = float(1)     # x will be 1.0
y = float(2.8)   # y will be 2.8
z = float("3")   # z will be 3.0
w = float("4.2") # w will be 4.2
```

#### 字符串

```python
x = str("s1") # x will be 's1'
y = str(2)    # y will be '2'
z = str(3.0)  # z will be '3.0'
```

## Python 高级数据类型

### 堆 {.col-span-2 .row-span-3}

```python
import heapq

myList = [9, 5, 4, 1, 3, 2]
heapq.heapify(myList) # 将 myList 转换为最小堆
print(myList)    # => [1, 3, 2, 5, 9, 4]
print(myList[0]) # 堆中的第一个值始终是最小的

heapq.heappush(myList, 10) # 插入 10
x = heapq.heappop(myList)  # 弹出并返回最小项
print(x)                   # => 1
```

#### 取反所有值以将最小堆用作最大堆

```python
myList = [9, 5, 4, 1, 3, 2]
myList = [-val for val in myList] # 乘以 -1 取反
heapq.heapify(myList)

x = heapq.heappop(myList)
print(-x) # => 9 (确保再次乘以 -1)
```

堆是二叉树，其中每个父节点的值都小于或等于其任何子节点的值。用于快速访问最小值/最大值。时间复杂度：heapify 为 O(n)，push 和 pop 为 O(log n)。参见：
[Heapq](https://docs.python.org/3/library/heapq.html)

### 栈和队列 {.row-span-3}

```python
from collections import deque

q = deque()          # 空
q = deque([1, 2, 3]) # 带值

q.append(4)     # 追加到右侧
q.appendleft(0) # 追加到左侧
print(q)    # => deque([0, 1, 2, 3, 4])

x = q.pop() # 从右侧移除并返回
y = q.popleft() # 从左侧移除并返回
print(x)    # => 4
print(y)    # => 0
print(q)    # => deque([1, 2, 3])

q.rotate(1) # 向右旋转1步
print(q)    # => deque([3, 1, 2])
```

Deque 是一个双端队列，两端追加/弹出操作的时间复杂度为 O(1)。用作栈和队列。参见：
[Deque](https://docs.python.org/3/library/collections.html#collections.deque)

## Python 字符串

### 类数组

```python
>>> hello = "Hello, World"
>>> print(hello[1])
e
>>> print(hello[-1])
d
```

获取位置 1 或最后一个字符

### 循环

```python
>>> for char in "foo":
...     print(char)
f
o
o
```

遍历单词 "foo" 中的字母

### 字符串切片 {.row-span-4}

```java
 ┌───┬───┬───┬───┬───┬───┬───┐
 | m | y | b | a | c | o | n |
 └───┴───┴───┴───┴───┴───┴───┘
 0   1   2   3   4   5   6   7
-7  -6  -5  -4  -3  -2  -1
```

---

```python
>>> s = 'mybacon'
>>> s[2:5]
'bac'
>>> s[0:2]
'my'
```

```python
>>> s = 'mybacon'
>>> s[:2]
'my'
>>> s[2:]
'bacon'
>>> s[:2] + s[2:]
'mybacon'
>>> s[:]
'mybacon'
```

```python
>>> s = 'mybacon'
>>> s[-5:-1]
'baco'
>>> s[2:6]
'baco'
```

#### 带步长

```python
>>> s = '12345' * 5
>>> s
'1234512345123451234512345'
>>> s[::5]
'11111'
>>> s[4::5]
'55555'
>>> s[::-5]
'55555'
>>> s[::-1]
'5432154321543215432154321'
```

### 字符串长度

```python
>>> hello = "Hello, World!"
>>> print(len(hello))
13
```

len() 函数返回字符串的长度

### 多份拷贝

```python
>>> s = '===+'
>>> n = 8
>>> s * n
'===+===+===+===+===+===+===+===+'
```

### 检查字符串

```python
>>> s = 'spam'
>>> s in 'I saw spamalot!'
True
>>> s not in 'I saw The Holy Grail!'
True

```

### 连接

```python
>>> s = 'spam'
>>> t = 'egg'
>>> s + t
'spamegg'
>>> 'spam' 'egg'
'spamegg'
```

### 格式化 {.col-span-2}

```python
name = "John"
print("Hello, %s!" % name)
```

```python
name = "John"
age = 23
print("%s is %d years old." % (name, age))
```

#### format() 方法

```python
txt1 = "My name is {fname}, I'm {age}".format(fname="John", age=36)
txt2 = "My name is {0}, I'm {1}".format("John", 36)
txt3 = "My name is {}, I'm {}".format("John", 36)
```

### 输入

```python
>>> name = input("Enter your name: ")
Enter your name: Tom
>>> name
'Tom'
```

从控制台获取输入数据

### 连接 (Join)

```python
>>> "#".join(["John", "Peter", "Vicky"])
'John#Peter#Vicky'
```

### Endswith

```python
>>> "Hello, world!".endswith("!")
True
```

## Python F-字符串 (Python 3.6+ 起)

### f-字符串用法

```python
>>> website = 'r3f.cn'
>>> f"Hello, {website}"
"Hello, r3f.cn"

>>> num = 10
>>> f'{num} + 10 = {num + 10}'
'10 + 10 = 20'

>>> f"""He said {"I'm John"}"""
"He said I'm John"

>>> f'5 {"{stars}"}'
'5 {stars}'
>>> f'{{5}} {"stars"}'
'{5} stars'

>>> name = 'Eric'
>>> age = 27
>>> f"""Hello!
...     I'm {name}.
...     I'm {age}."""
"Hello!\n    I'm Eric.\n    I'm 27."
```

自 Python 3.6 起可用，另请参阅：
[格式化字符串字面值](https://docs.python.org/3/reference/lexical_analysis.html#f-strings)

### f-字符串填充对齐

```python
>>> f'{"text":10}'     # [宽度]
'text      '
>>> f'{"test":*>10}'   # 左填充
'******test'
>>> f'{"test":*<10}'   # 右填充
'test******'
>>> f'{"test":*^10}'   # 居中填充
'***test***'
>>> f'{12345:0>10}'    # 用数字填充
'0000012345'
```

### f-字符串类型

```python
>>> f'{10:b}'        # 二进制类型
'1010'
>>> f'{10:o}'        # 八进制类型
'12'
>>> f'{200:x}'       # 十六进制类型
'c8'
>>> f'{200:X}'
'C8'
>>> f'{345600000000:e}' # 科学计数法
'3.456000e+11'
>>> f'{65:c}'       # 字符类型
'A'
>>> f'{10:#b}'      # [类型] 带表示法 (基数)
'0b1010'
>>> f'{10:#o}'
'0o12'
>>> f'{10:#x}'
'0xa'
```

### F-字符串其他

```python
>>> f'{-12345:0=10}'  # 负数
'-000012345'
>>> f'{12345:010}'    # [0] 快捷方式 (无对齐)
'0000012345'
>>> f'{-12345:010}'
'-000012345'
>>> import math       # [.精度]
>>> math.pi
3.141592653589793
>>> f'{math.pi:.2f}'
'3.14'
>>> f'{1000000:,.2f}' # [分组选项]
'1,000,000.00'
>>> f'{1000000:_.2f}'
'1_000_000.00'
>>> f'{0.25:0%}'      # 百分比
'25.000000%'
>>> f'{0.25:.0%}'
'25%'
```

### F-字符串符号

```python
>>> f'{12345:+}'      # [符号] (+/-)
'+12345'
>>> f'{-12345:+}'
'-12345'
>>> f'{-12345:+10}'
'    -12345'
>>> f'{-12345:+010}'
'-000012345'
```

## Python 列表

### 定义

```python
>>> li1 = []
>>> li1
[]
>>> li2 = [4, 5, 6]
>>> li2
[4, 5, 6]
>>> li3 = list((1, 2, 3))
>>> li3
[1, 2, 3]
>>> li4 = list(range(1, 11))
>>> li4
[1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```

### 生成 {.col-span-2}

```python
>>> list(filter(lambda x : x % 2 == 1, range(1, 20)))
[1, 3, 5, 7, 9, 11, 13, 15, 17, 19]

>>> [x ** 2 for x in range (1, 11) if  x % 2 == 1]
[1, 9, 25, 49, 81]

>>> [x for x in [3, 4, 5, 6, 7] if x > 5]
[6, 7]

>>> list(filter(lambda x: x > 5, [3, 4, 5, 6, 7]))
[6, 7]
```

### 追加

```python
>>> li = []
>>> li.append(1)
>>> li
[1]
>>> li.append(2)
>>> li
[1, 2]
>>> li.append(4)
>>> li
[1, 2, 4]
>>> li.append(3)
>>> li
[1, 2, 4, 3]
```

### 列表切片 {.col-span-2 .row-span-3}

列表切片语法：

```python
a_list[start:end]
a_list[start:end:step]
```

#### 切片

```python
>>> a = ['spam', 'egg', 'bacon', 'tomato', 'ham', 'lobster']
>>> a[2:5]
['bacon', 'tomato', 'ham']
>>> a[-5:-2]
['egg', 'bacon', 'tomato']
>>> a[1:4]
['egg', 'bacon', 'tomato']
```

#### 省略索引

```python
>>> a[:4]
['spam', 'egg', 'bacon', 'tomato']
>>> a[0:4]
['spam', 'egg', 'bacon', 'tomato']
>>> a[2:]
['bacon', 'tomato', 'ham', 'lobster']
>>> a[2:len(a)]
['bacon', 'tomato', 'ham', 'lobster']
>>> a
['spam', 'egg', 'bacon', 'tomato', 'ham', 'lobster']
>>> a[:]
['spam', 'egg', 'bacon', 'tomato', 'ham', 'lobster']
```

#### 带步长

```python
['spam', 'egg', 'bacon', 'tomato', 'ham', 'lobster']
>>> a[0:6:2]
['spam', 'bacon', 'ham']
>>> a[1:6:2]
['egg', 'tomato', 'lobster']
>>> a[6:0:-2]
['lobster', 'tomato', 'egg']
>>> a
['spam', 'egg', 'bacon', 'tomato', 'ham', 'lobster']
>>> a[::-1]
['lobster', 'ham', 'tomato', 'bacon', 'egg', 'spam']
```

### 移除

```python
>>> li = ['bread', 'butter', 'milk']
>>> li.pop()
'milk'
>>> li
['bread', 'butter']
>>> del li[0]
>>> li
['butter']
```

### 访问

```python
>>> li = ['a', 'b', 'c', 'd']
>>> li[0]
'a'
>>> li[-1]
'd'
>>> li[4]
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
IndexError: list index out of range
```

### 连接 {.row-span-2}

```python
>>> odd = [1, 3, 5]
>>> odd.extend([9, 11, 13])
>>> odd
[1, 3, 5, 9, 11, 13]
>>> odd = [1, 3, 5]
>>> odd + [9, 11, 13]
[1, 3, 5, 9, 11, 13]
```

### 排序和反转 {.row-span-2}

```python
>>> li = [3, 1, 3, 2, 5]
>>> li.sort()
>>> li
[1, 2, 3, 3, 5]
>>> li.reverse()
>>> li
[5, 3, 3, 2, 1]
```

### 计数

```python
>>> li = [3, 1, 3, 2, 5]
>>> li.count(3)
2
```

### 重复

```python
>>> li = ["re"] * 3
>>> li
['re', 're', 're']
```

## Python 流程控制

### 基本

```python
num = 5
if num > 10:
    print("num is totally bigger than 10.")
elif num < 10:
    print("num is smaller than 10.")
else:
    print("num is indeed 10.")
```

### 单行 (三元运算符)

```python
>>> a = 330
>>> b = 200
>>> r = "a" if a > b else "b"
>>> print(r)
a
```

### else if

```python
value = True
if not value:
    print("Value is False")
elif value is None:
    print("Value is None")
else:
    print("Value is True")
```

### match case

```python
x = 1
match x:
  case 0:
    print("zero")
  case 1:
    print("one")
  case _:
    print("multiple")
```

## Python 循环

### 基本

```python
primes = [2, 3, 5, 7]
for prime in primes:
    print(prime)
```

打印: 2 3 5 7

### 带索引

```python
animals = ["dog", "cat", "mouse"]
# enumerate() 为可迭代对象添加计数器
for i, value in enumerate(animals):
    print(i, value)
```

打印: 0 dog 1 cat 2 mouse

### While

```python
x = 0
while x < 4:
    print(x)
    x += 1  # x = x + 1 的简写
```

打印: 0 1 2 3

### Break

```python
x = 0
for index in range(10):
    x = index * 10
    if index == 5:
      break
    print(x)
```

打印: 0 10 20 30 40

### Continue

```python
for index in range(3, 8):
    x = index * 10
    if index == 5:
      continue
    print(x)
```

打印: 30 40 60 70

### Range

```python
for i in range(4):
    print(i) # 打印: 0 1 2 3

for i in range(4, 8):
    print(i) # 打印: 4 5 6 7

for i in range(4, 10, 2):
    print(i) # 打印: 4 6 8
```

### 使用 zip()

```python
words = ['Mon', 'Tue', 'Wed']
nums = [1, 2, 3]
# 使用 zip 打包成元组列表
for w, n in zip(words, nums):
    print('%d:%s, ' %(n, w))
```

打印: 1:Mon, 2:Tue, 3:Wed,

### for/else

```python
nums = [60, 70, 30, 110, 90]
for n in nums:
    if n > 100:
        print("%d is bigger than 100" %n)
        break
else:
    print("Not found!")
```

另请参阅: [Python 技巧](https://book.pythontips.com/en/latest/for_-_else.html)

## Python 函数

### 基本

```python
def hello_world():
    print('Hello, World!')
```

### 返回

```python
def add(x, y):
    print("x is %s, y is %s" %(x, y))
    return x + y

add(5, 6)    # => 11
```

### 位置参数

```python
def varargs(*args):
    return args

varargs(1, 2, 3)  # => (1, 2, 3)
```

"args" 的类型是元组。

### 关键字参数

```python
def keyword_args(**kwargs):
    return kwargs

# => {"big": "foot", "loch": "ness"}
keyword_args(big="foot", loch="ness")
```

"kwargs" 的类型是字典。

### 返回多个值

```python
def swap(x, y):
    return y, x

x = 1
y = 2
x, y = swap(x, y)  # => x = 2, y = 1
```

### 默认值

```python
def add(x, y=10):
    return x + y

add(5)      # => 15
add(5, 20)  # => 25
```

### 匿名函数

```python
# => True
(lambda x: x > 2)(3)

# => 5
(lambda x, y: x ** 2 + y ** 2)(2, 1)
```

## Python 模块

### 导入模块

```python
import math
print(math.sqrt(16))  # => 4.0
```

### 从模块导入

```python
from math import ceil, floor
print(ceil(3.7))   # => 4.0
print(floor(3.7))  # => 3.0
```

### 导入所有

```python
from math import *
```

### 缩短模块名

```python
import math as m

# => True
math.sqrt(16) == m.sqrt(16)
```

### 函数和属性

```python
import math
dir(math)
```

## Python 文件处理

### 读取文件

#### 逐行读取

```python
with open("myfile.txt") as file:
    for line in file:
        print(line)
```

#### 带行号

```python
file = open('myfile.txt', 'r')
for i, line in enumerate(file, start=1):
    print("Number %s: %s" % (i, line))
```

### 字符串

#### 写入字符串

```python
contents = {"aa": 12, "bb": 21}
with open("myfile1.txt", "w+") as file:
    file.write(str(contents))
```

#### 读取字符串

```python
with open('myfile1.txt', "r+") as file:
    contents = file.read()
print(contents)
```

### 对象

#### 写入对象

```python
contents = {"aa": 12, "bb": 21}
with open("myfile2.txt", "w+") as file:
    file.write(json.dumps(contents))
```

#### 读取对象

```python
with open('myfile2.txt', "r+") as file:
    contents = json.load(file)
print(contents)
```

### 删除文件

```python
import os
os.remove("myfile.txt")
```

### 检查并删除

```python
import os
if os.path.exists("myfile.txt"):
    os.remove("myfile.txt")
else:
    print("The file does not exist")
```

### 删除文件夹

```python
import os
os.rmdir("myfolder")
```

## Python 类和继承

### 定义

```python
class MyNewClass:
    pass

# 类实例化
my = MyNewClass()
```

### 构造函数

```python
class Animal:
    def __init__(self, voice):
        self.voice = voice

cat = Animal('Meow')
print(cat.voice)    # => Meow

dog = Animal('Woof')
print(dog.voice)    # => Woof
```

### 方法

```python
class Dog:

    # 类的方法
    def bark(self):
        print("Ham-Ham")

charlie = Dog()
charlie.bark()   # => "Ham-Ham"
```

### 类变量 {.row-span-2}

```python
class MyClass:
    class_variable = "A class variable!"

# => A class variable!
print(MyClass.class_variable)

x = MyClass()

# => A class variable!
print(x.class_variable)
```

### Super() 函数 {.row-span-2}

```python
class ParentClass:
    def print_test(self):
        print("Parent Method")

class ChildClass(ParentClass):
    def print_test(self):
        print("Child Method")
        # 调用父类的 print_test()
        super().print_test()
```

---

```python
>>> child_instance = ChildClass()
>>> child_instance.print_test()
Child Method
Parent Method
```

### repr() 方法

```python
class Employee:
    def __init__(self, name):
        self.name = name

    def __repr__(self):
        return self.name

john = Employee('John')
print(john)  # => John
```

### 用户定义异常

```python
class CustomError(Exception):
    pass
```

### 多态

```python
class ParentClass:
    def print_self(self):
        print('A')

class ChildClass(ParentClass):
    def print_self(self):
        print('B')

obj_A = ParentClass()
obj_B = ChildClass()

obj_A.print_self() # => A
obj_B.print_self() # => B
```

### 重写

```python
class ParentClass:
    def print_self(self):
        print("Parent")

class ChildClass(ParentClass):
    def print_self(self):
        print("Child")

child_instance = ChildClass()
child_instance.print_self() # => Child
```

### 继承

```python
class Animal:
    def __init__(self, name, legs):
        self.name = name
        self.legs = legs

class Dog(Animal):
    def sound(self):
        print("Woof!")

Yoki = Dog("Yoki", 4)
print(Yoki.name) # => YOKI
print(Yoki.legs) # => 4
Yoki.sound()     # => Woof!
```

## Python 类型提示 (Python 3.5 起)

### 变量和参数

```python
string: str = "ha"
times: int = 3


# 错误的提示，但能正确运行
result: str = 1 + 2
print(result)  # => 3


def say(name: str, start: str = "Hi"):
    return start + ", " + name

print(say("Python"))  # => Hi, Python
```

### 内置数据类型

```python
from typing import Dict, Tuple, List

bill: Dict[str, float] = {
    "apple": 3.14,
    "watermelon": 15.92,
    "pineapple": 6.53,
}
completed: Tuple[str] = ("DONE",)
succeeded: Tuple[int, str] = (1, "SUCCESS")
statuses: Tuple[str, ...] = (
    "DONE", "SUCCESS", "FAILED", "ERROR",
)
codes: List[int] = (0, 1, -1, -2)
```

### 内置数据类型 (3.10+)

```python
bill: dict[str, float] = {
    "apple": 3.14,
    "watermelon": 15.92,
    "pineapple": 6.53,
}
completed: tuple[str] = ("DONE",)
succeeded: tuple[int, str] = (1, "SUCCESS")
statuses: tuple[str, ...] = (
    "DONE", "SUCCESS", "FAILED", "ERROR",
)
codes: list[int] = (0, 1, -1, -2)
```

### 位置参数

```python
def calc_summary(*args: int):
    return sum(args)

print(calc_summary(3, 1, 4))  # => 8
```

表示所有参数的类型都是 int。

### 返回值

```python
def say_hello(name) -> str:
    return "Hello, " + name

var = "Python"
print(say_hello(var))  # => Hello, Python
```

### 联合类型返回值

```python
from typing import Union

def resp200(meaningful) -> Union[int, str]:
    return "OK" if meaningful else 200
```

表示返回值类型可能是 int 或 str。

### 关键字参数

```python
def calc_summary(**kwargs: int):
    return sum(kwargs.values())

print(calc_summary(a=1, b=2))  # => 3
```

表示所有参数值的类型都是 int。

### 多返回值

```python
def resp200() -> (int, str):
    return 200, "OK"

returns = resp200()
print(returns)  # => (200, 'OK')
print(type(returns))  # tuple
```

### 联合类型返回值 (3.10+)

```python
def resp200(meaningful) -> int | str:
    return "OK" if meaningful else 200
```

自 Python 3.10 起

### 属性

```python
class Employee:
    name: str
    age: int

    def __init__(self, name, age):
        self.name = name
        self.age = age
        self.graduated: bool = False
```

### Self 实例

```python
class Employee:
    name: str

    def set_name(self, name) -> "Employee":
        self.name = name
        return self

    def copy(self) -> 'Employee':
        return type(self)(self.name)
```

### Self 实例 (3.11+)

```python
from typing import Self

class Employee:
    name: str
    age: int

    def set_name(self: Self, name) -> Self:
        self.name = name
        return self
```

### 类型和泛型 {.col-span-2}

```python
from typing import TypeVar, Type

T = TypeVar("T")

# "mapper" 是一个类型，如 int、str、MyClass 等。
# "default" 是类型 T 的一个实例，如 314、"string"、MyClass() 等。
# 返回的也是类型 T 的一个实例。
def converter(raw, mapper: Type[T], default: T) -> T:
    try:
        return mapper(raw)
    except:
        return default

raw: str = input("Enter an integer: ")
result: int = converter(raw, mapper=int, default=0)
```

### 函数 {.col-span-2}

```python
from typing import TypeVar, Callable, Any

T = TypeVar("T")

def converter(raw, mapper: Callable[[Any], T], default: T) -> T:
    try:
        return mapper(raw)
    except:
        return default

# Callable[[Any], ReturnType] 表示一个函数声明如下：
# def func(arg: Any) -> ReturnType:
#     pass

# Callable[[str, int], ReturnType] 表示一个函数声明如下：
# def func(string: str, times: int) -> ReturnType:
#     pass

# Callable[..., ReturnType] 表示一个函数声明如下：
# def func(*args, **kwargs) -> ReturnType:
#     pass

def is_success(value) -> bool:
    return value in (0, "OK", True, "success")

resp = dict(code=0, message="OK", data=[])
successed: bool = converter(resp["message"], mapper=is_success, default=False)
```

## Python 运算符

### 海象运算符 {.col-span-2}

```python
values = [1, "text", True, "", 2]
i = 0

# 它将值赋给变量并在布尔表达式中进行比较
while (data := values[i]):

    print(data, end=",")
    i = i + 1

# 预期结果: 1, "text", True
```

## 其他

### 注释

```python
# 这是单行注释。
```

```python
""" 可以使用三个 " 来编写多行字符串，
    并且通常用作文档。
"""
```

```python
''' 可以使用三个 ' 来编写多行字符串，
    并且通常用作文档。
'''
```

### 生成器

```python
def double_numbers(iterable):
    for i in iterable:
        yield i + i
```

生成器帮助您编写惰性代码。

### 生成器转列表

```python
values = (-x for x in [1,2,3,4,5])
gen_to_list = list(values)

# => [-1, -2, -3, -4, -5]
print(gen_to_list)
```

### 处理异常 {.col-span-3}

```python
try:
    # 使用 "raise" 抛出错误
    raise IndexError("This is an index error")
except IndexError as e:
    pass                 # Pass 只是一个空操作。通常你会在这里进行恢复操作。
except (TypeError, NameError):
    pass                 # 如果需要，可以一起处理多个异常。
else:                    # try/except 块的可选子句。必须在所有 except 块之后
    print("All good!")   # 仅当 try 中的代码没有引发异常时运行
finally:                 # 在任何情况下都会执行
    print("We can clean up resources here")
```
