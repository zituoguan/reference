---
title: Nim
date: 2024-05-15 8:03:44
background: bg-[#eed547]
tags:
categories:
  - 编程
intro: |
  Nim 快速参考备忘单，旨在帮助编写基本语法和方法。
plugins:
  - copyCode
---

## 入门

### Helloworld.nim

```nim
echo "Hello World!"
#---------------------------#
# 这是一个注释
echo "What's your name? "
var name: string = readLine(stdin)
echo "Hi, ", name, "!"
```

#### 编译和运行

```shell
$ nim c helloworld.nim
# 如果操作系统是 windows
$ helloworld.exe
# 如果操作系统是 linux
$ ./Hello_World
# 输出
Hello, World!

# 也可以使用一个命令
# 同时编译和运行
# 程序。
# 我们需要输入：
$ nim c -r helloworld.nim

```

### 注释

```nim
# 这是一个注释


#[
  这是一个多行注释。
  在 Nim 中，多行注释可以嵌套，以 #[ 开头
  ... 并以 ]# 结尾
]#

```

### 变量声明

```nim

var
  letter: char = 'n'
  lang = "N" & "im"
  nLength: int = len(lang)
  boat: float
  truth: bool = false
  b = 7
  c = -11
  d = "Hello"
  e = '!'
```

### Let

```nim
# 使用 let 声明和绑定变量
let
  legs = 400
 #legs 是不可变的。
  arms = 2_000
  # _ 会被忽略，对于长数字很有用。
  aboutPi = 3.15
  let input = readLine(stdin)  # 可行
```

### Const

```nim
# 常量在编译时计算
const
  debug = true
   # 性能，并且在编译时表达式中很有用。
  compileBadCode = false
```

基本数据类型

---

### 整数

```nim
let
  a = 11
  b = 4

echo "a + b = ", a + b
echo "a - b = ", a - b
echo "a * b = ", a * b
echo "a / b = ", a / b
echo "a div b = ", a div b
echo "a mod b = ", a mod b
#输出
#a + b = 15
#a - b = 7
#a * b = 44
#a / b = 2.75
#a div b = 2
#a mod b = 3
```

### 浮点数

```nim
let
  c = 6.75
  d = 2.25

echo "c + d = ", c + d
echo "c - d = ", c - d
echo "c * d = ", c * d
echo "c / d = ", c / d
#输出
#c + d = 9.0
#c - d = 4.5
#c * d = 15.1875
#c / d = 3.0
```

### 字符串

```nim
#字符串可以描述
#为一系列字符。
#其内容写在两个双引号 (") 之间。
let
  m = "word"
  n = "A sentence with interpunction."
  o = ""
  p = "32"
  q = "!"
```

### 字符

```nim
#字符是单个
#字符。它们
#写在两个单引号 (') 之间。
let
  h = 'z'
  i = '+'
  j = '2'
  k = '35' # 错误
  l = 'xy' # 错误
```

### 特殊字符

```nim
#\n 是换行符
#\t 是制表符
#\\ 是反斜杠 (因为一个 \ 用作转义字符)

echo "some\nim\tips"
echo "some\\nim\\tips"
echo r"some\nim\tips"
#输出
#some
#im	ips
#some\nim\tips
#some\nim\tips
```

### 布尔值

```nim
#布尔 (或简称 bool)
# 数据类型只能有
#两个值：true 或 false。
let isEmpty = true
let isFull = false
```

### 转换浮点数和整数

```nim
let
  e = 5
  f = 23.987
echo e + f   # 错误
echo float(e)
echo int(f)

echo float(e) + f
echo e + int(f)
#输出
#5.0
#23
#28.987
#28
```

### 字符串连接

```nim
var
  p = "abc"
  q = "xy"
  r = 'z'

p.add("def")
echo "p is now: ", p

q.add(r)
echo "q is now: ", q

echo "concat: ", p & q

echo "p is still: ", p
echo "q is still: ", q
#输出
#p is now: abcdef
#q is now: xyz
#concat: abcdefxyz
#p is still: abcdef
#q is still: xyz
```

## 运算符

### 关系运算符

```nim
let
  g = 31
  h = 99

echo "g is greater than h: ", g > h
echo "g is smaller than h: ", g < h
echo "g is equal to h: ", g == h
echo "g is not equal to h: ", g != h
echo "g is greater or equal to h: ", g >= h
echo "g is smaller or equal to h: ", g <= h
#输出
g is greater than h: false
g is smaller than h: true
g is equal to h: false
g is not equal to h: true
g is greater or equal to h: false
g is smaller or equal to h: true

#示例
let
  i = 'a'
  j = 'd'
  k = 'Z'

echo i < j
echo i < k

let
  m = "axyb"
  n = "axyz"
  o = "ba"
  p = "ba "

echo m < n
echo n < o
echo o < p
#输出
#false
#true
#true
#true
#true
```

### 逻辑运算符

```nim
echo "T and T: ", true and true
echo "T and F: ", true and false
echo "F and F: ", false and false
echo "---"
echo "T or T: ", true or true
echo "T or F: ", true or false
echo "F or F: ", false or false
echo "---"
echo "T xor T: ", true xor true
echo "T xor F: ", true xor false
echo "F xor F: ", false xor false
echo "---"
echo "not T: ", not true
echo "not F: ", not false
#输出
#T and T: true
#T and F: false
#F and F: false
---
#T or T: true
#T or F: true
#F or F: false
---
#T xor T: false
#T xor F: true
#F xor F: false
---
#not T: false
#not F: true
```

## 控制流

### If 语句

```nim
let
  a = 11
  b = 22
  c = 999

if a < b:
  echo "a is smaller than b"
  if 10*a < b:
    echo "not only that, a is *much* smaller than b"

if b < c:
  echo "b is smaller than c"
  if 10*b < c:
    echo "not only that, b is *much* smaller than c"

if a+b > c:
  echo "a and b are larger than c"
  if 1 < 100 and 321 > 123:
    echo "did you know that 1 is smaller than 100?"
    echo "and 321 is larger than 123! wow!"
#输出
#a is smaller than b
#b is smaller than c
#not only that, b is *much* smaller than c
```

### Case 语句

```nim
let name = readLine(stdin)
case name
of "":
  echo "Poor soul, you lost your name?"
of "name":
  echo "Very funny, your name is name."
of "Dave", "Frank":
  echo "Cool name!"
else:
  echo "Hi, ", name, "!"

```

### While 语句

```nim
echo "What's your name? "
var name = readLine(stdin)
while name == "":
  echo "Please tell me your name: "
  name = readLine(stdin) # 没有 `var`，因为我们这里没有声明新变量
```

### For 语句

```nim
echo "Counting to ten: "
for i in countup(1, 10):
  echo i
# --> 在不同行上输出 1 2 3 4 5 6 7 8 9 10
```

### 作用域和块语句

```nim
while false:
  var x = "hi"
echo x # 不起作用
#-----------------------#
block myblock:
  var x = "hi"
echo x # 同样不起作用
```

### Break 语句

```nim
block myblock:
  echo "entering block"
  while true:
    echo "looping"
    break # 离开循环，但不离开块
  echo "still in block"
echo "outside the block"

```

### Continue 语句

```nim
for i in 1 .. 5:
  if i <= 3: continue
  echo i # 只会打印 4 和 5
```

### When 语句

```nim
  when system.hostOS == "windows":
  echo "running on Windows!"
elif system.hostOS == "linux":
  echo "running on Linux!"
elif system.hostOS == "macosx":
  echo "running on Mac OS X!"
else:
  echo "unknown operating system"
```

### 语句和缩进

```nim
# 单一赋值语句不需要缩进：
if x: x = false

# 嵌套 if 语句需要缩进：
if x:
  if y:
    y = false
  else:
    y = true

# 需要缩进，因为条件后有两个语句：
if x:
  x = false
  y = false
```

### 过程

```nim
proc yes(question: string): bool =
  echo question, " (y/n)"
  while true:
    case readLine(stdin)
    of "y", "Y", "yes", "Yes": return true
    of "n", "N", "no", "No": return false
    else: echo "Please be clear: yes or no"

if yes("Should I delete all your important files?"):
  echo "I'm sorry Dave, I'm afraid I can't do that."
else:
  echo "I think you know what the problem is just as well as I do."
```

### Result 变量

```nim
proc sumTillNegative(x: varargs[int]): int =
  for i in x:
    if i < 0:
      return
    result = result + i

echo sumTillNegative() # echoes 0
echo sumTillNegative(3, 4, 5) # echoes 12
echo sumTillNegative(3, 4 , -1 , 6) # echoes 7
```

### 参数

```nim
proc printSeq(s: seq, nprinted: int = -1) =
  var nprinted = if nprinted == -1: s.len else: min(nprinted, s.len)
  for i in 0 ..< nprinted:
    echo s[i]
#------------------- #
proc divmod(a, b: int; res, remainder: var int) =
  res = a div b        # 整数除法
  remainder = a mod b  # 整数取模运算

var
  x, y: int
divmod(8, 5, x, y) # 修改 x 和 y
echo x
echo y
```

### Discard 语句

```nim
discard yes("May I ask a pointless question?")

proc p(x, y: int): int {.discardable.} =
  return x + y

p(3, 4) # 现在有效
```

### 命名参数

```nim
proc createWindow(x, y, width, height: int; title: string;  show: bool): Window = ...

var w = createWindow(show = true, title = "My Application", x = 0, y = 0, height = 600, width = 800)

var w = createWindow(0, 0, title = "My Application",
                     height = 600, width = 800, true)
```

### 默认值

```nim
proc createWindow(x = 0, y = 0, width = 500, height = 700,
                  title = "unknown",
                  show = true): Window =


var w = createWindow(title = "My Application", height = 600, width = 800)
```

### 重载过程

```nim
proc toString(x: int): string =
  result =
    if x < 0: "negative"
    elif x > 0: "positive"
    else: "zero"

proc toString(x: bool): string =
  result =
    if x: "yep"
    else: "nope"

assert toString(13) == "positive"
 # 调用 toString(x: int) 过程
assert toString(true) == "yep"
 # 调用 toString(x: bool) 过程
```

### 前向声明

```nim
proc odd(n: int): bool =
  assert(n >= 0) # 确保我们不会陷入负递归
  if n == 0: false
  else:
    n == 1 or even(n-1)

proc even(n: int): bool =
  assert(n >= 0) # 确保我们不会陷入负递归
  if n == 1: false
  else:
    n == 0 or odd(n-1)
```

### 迭代器

```nim
echo "Counting to ten: "
for i in countup(1, 10):
  echo i

proc countup(a, b: int): int =
  var res = a
  while res <= b:
    return res
    inc(res)

iterator countup(a, b: int): int =
  var res = a
  while res <= b:
    yield res
    inc(res)
```

### 类型转换

```nim
var
  x: int32 = 1.int32   # 等同于调用 int32(1)
  y: int8  = int8('a') # 'a' == 97'i8
  z: float = 2.5       # int(2.5) 向下取整为 2
  sum: int = int(x) + int(y) + int(z) # sum == 100
```

### 内部类型表示

```nim
var
  myBool = true
  myCharacter = 'n'
  myString = "nim"
  myInteger = 42
  myFloat = 3.14
echo myBool, ":", repr(myBool)
# --> true:true
echo myCharacter, ":", repr(myCharacter)
# --> n:'n'
echo myString, ":", repr(myString)
# --> nim:0x10fa8c050"nim"
echo myInteger, ":", repr(myInteger)
# --> 42:42
echo myFloat, ":", repr(myFloat)
# --> 3.14:3.14
```

### 枚举

```nim
type
  Direction = enum
    north, east, south, west

var x = south
# `x` 的类型是 `Direction`；其值为 `south`
#打印 "south"
echo x
```

### 序数类型

| 操作       |                            注释                            |
| :--------- | :-----------------------------------------------------------: |
| ord(x)     | 返回用于表示 x 值的整数值                                     |
| inc(x)     |                      将 x 增加 1                      |
| inc(x, n)  |              将 x 增加 n；n 是一个整数               |
| dec(x)     |                      将 x 减少 1                      |
| dec(x, n)  |              将 x 减少 n；n 是一个整数               |
| succ(x)    |                  返回 x 的后继者                   |
| succ(x, n) |                返回 x 的第 n 个后继者                |
| pred(x)    |                 返回 x 的前驱者                  |
| pred(x, n) |               返回 x 的第 n 个前驱者               |

### 子范围

```nim
type
  MySubrange = range[0..5]
```

### 集合

```nim
  var s: set[int64]
  # 错误：集合太大；对于超过 2^16 个元素的序数类型，请使用 `std/sets`
 type
  CharSet = set[char]
var
  x: CharSet
x = {'a'..'z', '0'..'9'}
 # 这会构造一个包含从 'a' 到 'z' 的字母和从 '0' 到 '9' 的数字的集合
```

### 位域

```nim
type
 MyFlag* {.size: sizeof(cint).} = enum
   A
   B
   C
   D
 MyFlags = set[MyFlag]

proc toNum(f: MyFlags): int = cast[cint](f)
proc toFlags(v: int): MyFlags = cast[MyFlags](v)

assert toNum({}) == 0
assert toNum({A}) == 1
assert toNum({D}) == 8
assert toNum({A, C}) == 5
assert toFlags(0) == {}
assert toFlags(7) == {A, B, C}
```

### 数组

```nim
type
  IntArray = array[0..5, int] # 一个用 0..5 索引的数组
var
  x: IntArray
x = [1, 2, 3, 4, 5, 6]
for i in low(x) .. high(x):
  echo x[i]
```

### 序列

```nim
  var
  x: seq[int] # 对整数序列的引用
x = @[1, 2, 3, 4, 5, 6] # @ 将数组转换为在堆上分配的序列
for value in @[3, 4, 5]:
  echo value
# --> 3
# --> 4
# --> 5

for i, value in @[3, 4, 5]:
  echo "index: ", $i, ", value:", $value
# --> index: 0, value:3
# --> index: 1, value:4
# --> index: 2, value:5
```

### 开放数组

```nim
var
  fruits:   seq[string]
 # 对使用 '@[]' 初始化的字符串序列的引用
  capitals: array[3, string]

 # 固定大小的字符串数组

capitals = ["New York", "London", "Berlin"]
 # 数组 'capitals' 只允许分配三个元素
fruits.add("Banana")
 # 序列 'fruits' 在运行时可动态扩展
fruits.add("Mango")

proc openArraySize(oa: openArray[string]): int =
  oa.len

assert openArraySize(fruits) == 2
  # 过程接受序列作为参数
assert openArraySize(capitals) == 3
  # 也接受数组类型
```

### 可变参数

```nim
proc myWriteln(f: File, a: varargs[string]) =
  for s in items(a):
    write(f, s)
  write(f, "\n")

myWriteln(stdout, "abc", "def", "xyz")
# 被编译器转换为：
myWriteln(stdout, ["abc", "def", "xyz"])
```

### 切片

```nim
var
  a = "Nim is a programming language"
  b = "Slices are useless."

echo a[7 .. 12] # --> 'a prog'
b[11 .. ^2] = "useful"
echo b # --> 'Slices are useful.'
```

### 对象

```nim
type
  Person = object
    name: string
    age: int

var person1 = Person(name: "Peter", age: 30)

echo person1.name # "Peter"
echo person1.age  # 30

var person2 = person1 # person 1 的副本

person2.age += 14

echo person1.age # 30
echo person2.age # 44


# 顺序可以更改
let person3 = Person(age: 12, name: "Quentin")

# 不需要指定每个成员
let person4 = Person(age: 3)
# 未指定的成员将使用其默认值进行初始化。在这种情况下，它是空字符串。
doAssert person4.name == ""
```

### 元组

```nim
type
  Person = tuple
    name: string
    age: int

  PersonX = tuple[name: string, age: int]

  PersonY = (string, int)

var
  person: Person
  personX: PersonX
  personY: PersonY

person = (name: "Peter", age: 30)
# Person 和 PersonX 等效
personX = person

# 创建具有匿名宇段的元组：
personY = ("Peter", 30)

person = personY
personY = person

person = ("Peter", 30)

echo person.name # "Peter"
echo person.age  # 30

echo person[0] # "Peter"
echo person[1] # 30

var building: tuple[street: string, number: int]
building = ("Rue del Percebe", 13)
echo building.street

```

### 引用和指针类型

```nim
type
  Node = ref object
    le, ri: Node
    data: int

var n = Node(data: 9)
echo n.data
# 不需要写 n[].data；实际上，强烈不建议使用 n[].data！
```

### 过程类型

```nim
proc greet(name: string): string =
  "Hello, " & name & "!"

proc bye(name: string): string =
  "Goodbye, " & name & "."

proc communicate(greeting: proc (x: string): string, name: string) =
  echo greeting(name)

communicate(greet, "John")
communicate(bye, "Mary")
```

### 模块

```nim
# 模块 A
var
  x*, y: int

proc `*` *(a, b: seq[int]): seq[int] =
  # 分配一个新序列：
  newSeq(result, len(a))
  # 乘以两个整数序列：
  for i in 0 ..< len(a): result[i] = a[i] * b[i]

when isMainModule:
  # 测试序列的新 `*` 运算符：
  assert(@[1, 2, 3] * @[1, 2, 3] == @[1, 4, 9])


```

### 排除符号

```nim
import mymodule except y

# From 语句
from mymodule import x, y, z
from mymodule import x, y, z

x()
  # 不带任何限定地使用 x

#Include 语句
include fileA, fileB, fileC

```

### 继承

```nim
type
  Person = ref object of RootObj
    name*: string  # * 表示 `name` 可从其他模块访问
    age: int       # 没有 * 表示该字段对其他模块隐藏

  Student = ref object of Person # Student 继承自 Person
    id: int                      # 带有一个 id 字段

var
  student: Student
  person: Person
assert(student of Student) # 为真
# 对象构造：
student = Student(name: "Anton", age: 5, id: 2)
echo student[]
```

### 相互递归类型

```nim
type
  Node = ref object
 # 对具有以下字段的对象的引用：
    le, ri: Node
   # 左右子树
    sym: ref Sym
  # 叶子节点包含对 Sym 的引用

  Sym = object
    # 一个符号
    name: string
     # 符号的名称
    line: int
   # 符号声明所在的行
    code: Node
    # 符号的抽象语法树
```

### 对象变体

```nim
# 这是一个如何在 Nim 中建模抽象语法树的示例
type
  NodeKind = enum  # 不同的节点类型
    nkInt,          # 带有整数值的叶节点
    nkFloat,        # 带有浮点值的叶节点
    nkString,       # 带有字符串值的叶节点
    nkAdd,          # 加法
    nkSub,          # 减法
    nkIf            # if 语句
  Node = ref object
    case kind: NodeKind  # `kind` 字段是鉴别器
    of nkInt: intVal: int
    of nkFloat: floatVal: float
    of nkString: strVal: string
    of nkAdd, nkSub:
      leftOp, rightOp: Node
    of nkIf:
      condition, thenPart, elsePart: Node

var n = Node(kind: nkFloat, floatVal: 1.0)
# 以下语句会引发 `FieldDefect` 异常，因为
# n.kind 的值不匹配：
n.strVal = ""
```

### 方法调用语法

```nim
import std/strutils

echo "abc".len # 与 echo len("abc") 相同
echo "abc".toUpperAscii()
echo({'a', 'b', 'c'}.card)
stdout.writeLine("Hallo") # 与 writeLine(stdout, "Hallo") 相同
##############################
import std/[strutils, sequtils]

stdout.writeLine("Give a list of numbers (separated by spaces): ")
stdout.write(stdin.readLine.splitWhitespace.map(parseInt).max.`$`)
stdout.writeLine(" is the maximum!")
```

### 属性

```nim
type
  Socket* = ref object of RootObj
    h: int # 由于缺少星号，无法从模块外部访问

proc `host=`*(s: var Socket, value: int) {.inline.} =
  ## 主机地址的设置器
  s.h = value

proc host*(s: Socket): int {.inline.} =
  ## 主机地址的获取器
  s.h

var s: Socket
new s
s.host = 34  # 与 `host=`(s, 34) 相同

type
  Vector* = object
    x, y, z: float

proc `[]=`* (v: var Vector, i: int, value: float) =
  # 设置器
  case i
  of 0: v.x = value
  of 1: v.y = value
  of 2: v.z = value
  else: assert(false)

proc `[]`* (v: Vector, i: int): float =
  # 获取器
  case i
  of 0: result = v.x
  of 1: result = v.y
  of 2: result = v.z
  else: assert(false)
```

### 动态调度

```nim
type
  Expression = ref object of RootObj ## 表达式的抽象基类
  Literal = ref object of Expression
    x: int
  PlusExpr = ref object of Expression
    a, b: Expression

# 注意：'eval' 依赖于动态绑定
method eval(e: Expression): int {.base.} =
  # 重写此基方法
  quit "需要重写！"

method eval(e: Literal): int = e.x
method eval(e: PlusExpr): int = eval(e.a) + eval(e.b)

proc newLit(x: int): Literal = Literal(x: x)
proc newPlus(a, b: Expression): PlusExpr = PlusExpr(a: a, b: b)

echo eval(newPlus(newPlus(newLit(1), newLit(2)), newLit(4)))
```

### Raise 语句

```nim
var
  e: ref OSError
new(e)
e.msg = "the request to the OS failed"
raise e

raise newException(OSError, "the request to the OS failed")
```

### Try 语句

```nim
from std/strutils import parseInt

# 读取文本文件的前两行，这两行应包含数字
# 并尝试将它们相加
var
  f: File
if open(f, "numbers.txt"):
  try:
    let a = readLine(f)
    let b = readLine(f)
    echo "sum: ", parseInt(a) + parseInt(b)
  except OverflowDefect:
    echo "overflow!"
  except ValueError:
    echo "could not convert string to integer"
  except IOError:
    echo "IO error!"
  except CatchableError:
    echo "Unknown exception!"
    # 重新引发未知异常：
    raise
  finally:
    close(f)
```

### 使用引发的异常注释过程

```nim
proc complexProc() {.raises: [IOError, ArithmeticDefect].} =


proc simpleProc() {.raises: [].} =
  ...
```

### 泛型

```nim
 type
  BinaryTree*[T] = ref object # BinaryTree 是一个泛型类型，带有
                              # 泛型参数 `T`
    le, ri: BinaryTree[T]     # 左右子树；可以为 nil
    data: T                   # 存储在节点中的数据

proc newNode*[T](data: T): BinaryTree[T] =
  # 节点的构造函数
  new(result)
  result.data = data

proc add*[T](root: var BinaryTree[T], n: BinaryTree[T]) =
  # 将节点插入树中
  if root == nil:
    root = n
  else:
    var it = root
    while it != nil:
      # 比较数据项；使用适用于任何具有 `==` 和 `<` 运算符
      # 的类型的泛型 `cmp` 过程
      var c = cmp(it.data, n.data)
      if c < 0:
        if it.le == nil:
          it.le = n
          return
        it = it.le
      else:
        if it.ri == nil:
          it.ri = n
          return
        it = it.ri

proc add*[T](root: var BinaryTree[T], data: T) =
  # 便捷过程：
  add(root, newNode(data))

iterator preorder*[T](root: BinaryTree[T]): T =
  # 二叉树的前序遍历。
  # 这使用显式堆栈 (比递归迭代器工厂更有效)。
  var stack: seq[BinaryTree[T]] = @[root]
  while stack.len > 0:
    var n = stack.pop()
    while n != nil:
      yield n.data
      add(stack, n.ri)  # 将右子树推入堆栈
      n = n.le          # 并跟随左指针

var
  root: BinaryTree[string] # 使用 `string` 实例化 BinaryTree
add(root, newNode("hello")) # 实例化 `newNode` 和 `add`
add(root, "world")          # 实例化第二个 `add` 过程
for str in preorder(root):
  stdout.writeLine(str)
```

### 模板

```nim
template `!=` (a, b: untyped): untyped =
  # 此定义存在于 System 模块中
  not (a == b)

assert(5 != 6) # 编译器将其重写为：assert(not (5 == 6))
#############################################
const
  debug = true

proc log(msg: string) {.inline.} =
  if debug: stdout.writeLine(msg)

var
  x = 4
log("x has the value: " & $x)
####################################
template withFile(f: untyped, filename: string, mode: FileMode,
                  body: untyped) =
  let fn = filename
  var f: File
  if open(f, fn, mode):
    try:
      body
    finally:
      close(f)
  else:
    quit("cannot open: " & fn)

withFile(txt, "ttempl3.txt", fmWrite):
  txt.writeLine("line 1")
  txt.writeLine("line 2")

```

### 静态参数

```nim
import std/macros

macro myMacro(arg: static[int]): untyped =
  echo arg # 只是一个整数 (7)，而不是 `NimNode`

myMacro(1 + 2 * 3)
```

### 作为参数的代码块

```nim
echo "Hello ":
  let a = "Wor"
  let b = "ld!"
  a & b
```

### 语法树

```nim
dumpTree:
  var mt: MyType = MyType(a:123.456, b:"abcdef")

# 输出：
#   StmtList
#     VarSection
#       IdentDefs
#         Ident "mt"
#         Ident "MyType"
#         ObjConstr
#           Ident "MyType"
#           ExprColonExpr
#             Ident "a"
#             FloatLit 123.456
#           ExprColonExpr
#             Ident "b"
#             StrLit "abcdef"
```

### 自定义语义检查

```nim
macro myAssert(arg: untyped): untyped =
  arg.expectKind nnkInfix
```

### 生成代码

```nim
import std/macros

type
MyType = object
  a: float
  b: string

macro myMacro(arg: untyped): untyped =
var mt: MyType = MyType(a:123.456, b:"abcdef")

#

let mtLit = newLit(mt)

result = quote do:
  echo `arg`
  echo `mtLit`

myMacro("Hallo")
```

### 构建你的第一个宏

```nim
import std/macros

macro myAssert(arg: untyped): untyped =
  # 所有节点类型标识符都以 "nnk" 为前缀
  arg.expectKind nnkInfix
  arg.expectLen 3
  # 运算符作为字符串字面量
  let op  = newLit(" " & arg[0].repr & " ")
  let lhs = arg[1]
  let rhs = arg[2]

  result = quote do:
    if not `arg`:
      raise newException(AssertionDefect,$`lhs` & `op` & $`rhs`)

let a = 1
let b = 2

myAssert(a != b)
myAssert(a == b)

```

## 另请参阅

- [Nim 备忘单](https://narimiran.github.io/nim-basics/) _(https://narimiran.github.io)_
