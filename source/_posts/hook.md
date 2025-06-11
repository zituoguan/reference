---
title: Hook 语言
date: 2024-03-13 18:20:00
icon: icon-style
background: bg-[#1131e2]
tags:
  - 脚本
  - 解释
categories:
  - 编程
intro: |
  [Hook](https://github.com/hook-lang/hook/) 速查表是 Hook 编程语言的单页参考表。
plugins:
  - copyCode
---

## 入门指南

### 简介

- [GitHub](https://github.com/hook-lang/hook)
- [演练场](https://hook-lang.github.io/hook-playground)
- [示例](https://github.com/hook-lang/hook/tree/main/examples)
- [VSCode 扩展](https://marketplace.visualstudio.com/items?itemName=fabiosvm.hook)

### Hook 代码示例

```rs
fn factorial(n) {
  if (n == 0)
    return 1;
  return n * factorial(n - 1);
}
```

Hook 采用类似于 `C` 语言的现代语法。

### Hello, world!

```js
println("Hello, World!");
// Hello, World!
```

Hook 语言的 `Hello, World!` 程序。

### 使用 Homebrew 安装

```text
brew tap hook-lang/hook
brew install hook
hook --help
```

解释器可通过 [`Homebrew`](https://brew.sh) 获取。

### 在 Windows 上安装 {.col-span-2}

```text
cd %tmp%
curl -sSLO https://raw.githubusercontent.com/hook-lang/hook/main/scripts/install.bat
install
```

这是在 `Windows` 上安装的方法。

## 类型和值

### 基本类型

|          |           |
| -------- | :-------- |
| `Nil`    | `Bool`    |
| `Number` | `String`  |
| `Range`  | `Array`   |
| `Record` | `Closure` |

基本类型列表。

### 布尔型 (Bool)

```js
let x = true;
let y = false;
```

布尔型是一种布尔类型。因此，它可以是 `true` 或 `false`。

### 数字 (Numbers)

```js
let x = 0;
let degree = 45; // 整数
let pi = 3.14; // 浮点数
```

数字可以是整数或浮点数。

### 字符串 (Strings)

```js
let empty = "";

let name = "John";

let message = 'Hello, "John"!';
```

字符串可以用单引号或双引号。

### 范围 (Ranges)

```js
let range = 1..5;

println(range);
// 1..5
```

范围是整数序列。

### 数组 (Arrays)

```js
let fruits = ["apple", "banana", "cherry"];

println(fruits);
// ["apple", "banana", "cherry"]
```

数组是元素的序列。

### 记录 (Records)

```js
let p = { x: 5, y: 10 };

println(p);
// {x: 5, y: 10}
```

记录将字段映射到值。

### **nil** 值

```swift
let x = nil;
var y;
```

```js
println(x); // nil
println(y); // nil
```

`nil` 表示值的缺失。

### 假值 (Falsy values)

```swift
if (nil) "true" else "false";   // false
if (false) "true" else "false"; // false
if (true) "true" else "false";  // true
if (0) "true" else "false";     // true
if (1) "true" else "false";     // true
if ("") "true" else "false";    // true
if ([]) "true" else "false";    // true
if ({}) "true" else "false";    // true
```

只有 `nil` 和 `false` 是假值。

## 语法

### 注释

```js
// 这是单行注释。

// 这也是
// 一个多行
// 注释。 ;)
```

Hook 只支持单行注释。抱歉！

### 分号 {.col-span-2}

<!-- prettier-ignore -->
```js
println(1) ; println(2) ; println(3) ;
println(4) ; println(5)
; println(6) ;
;                                      // 错误：意外的标记 ';'
```

分号是必需的，且不允许空语句。

### 代码块

```js
{
  println("Hello");
  {
    println("World");
  }
}
```

代码块用于定义作用域。

### 保留字

|         |          |            |         |
| ------- | :------- | :--------- | :------ |
| `as`    | `break`  | `continue` | `do`    |
| `else`  | `false`  | `fn`       | `for`   |
| `from`  | `if`     | `import`   | `in`    |
| `inout` | `let`    | `loop`     | `match` |
| `nil`   | `return` | `struct`   | `trait` |
| `true`  | `var`    | `while`    |         |

保留字很少。

### 标识符

```php
var lowercase;
var CAPS_LOCK;
var camelCase;
var PascalCase;
var snake_case;
var _123;
```

标识符区分大小写。

## 变量

### 变量

```js
var x; // x 包含 nil
x = 5; // 现在，x 包含一个数字
x = "foo"; // 一个字符串

println(x);
```

值有类型，但变量没有。

### 不可变变量 {.col-span-2}

```js
let x = 5;

x = 10; // 错误：无法分配给不可变变量 `x`

let y; // 错误：意外的标记 ';'
```

不可变变量在声明时必须初始化。

### 作用域 {.col-span-2}

```js
let x = 5;
{
  let y = 15;
  println(x); // 5 (此处原文为10，根据上下文应为5，或者外部x被修改，但代码未显示)
  println(y); // 15
}
println(x); // 5
println(y); // 错误：变量 `y` 已使用但未定义
```

当堆分配的变量超出作用域时，它会自动释放。

### 遮蔽 (Shadowing)

```js
let x = 5;
{
  let x = 10; // 遮蔽了外部的 `x`
  println(x); // 10
}
println(x); // 5
```

变量可以被遮蔽。

## 运算符和表达式

### 算术运算符

```js
println(5 + 10); // 15
println(5 - 10); // -5
println(5 * 10); // 50
println(5 / 10); // 0.5
println(5 % 10); // 5
println(-5); // -5
```

基本的算术运算符。

### 比较运算符

```js
println(5 == 10); // false
println(5 != 10); // true
println(5 < 10); // true
println(5 > 10); // false
println(5 <= 10); // true
println(5 >= 10); // false
```

比较运算符。

### 逻辑运算符

```js
println(true && false); // false
println(true || false); // true
println(!true); // false
```

逻辑运算符。

### 位运算符和移位运算符

```js
println(5 & 10); // 0
println(5 | 10); // 15
println(5 ^ 10); // 15
println(~5); // -6
println(5 << 1); // 10
println(5 >> 1); // 2
```

位运算符和移位运算符。

### 赋值运算符

```js
var x = 5; // 5
x += 10; // 15
x -= 10; // 5
x *= 10; // 50
x /= 10; // 5
x %= 10; // 5
x &= 10; // 0
x |= 10; // 10
x ^= 5; // 15
x <<= 5; // 480
x >>= 5; // 15
x++; // 16
x--; // 15
```

赋值运算符。

### 三元运算符

```js
let x = 5;
let y = if (x > 5) 10 else 20;

println(y);
// 20
```

在 Hook 中，三元运算符是 `if else`。

## 分支

### If 语句

```js
let x = 10;

if (x > 5) {
  println("x is greater than 5");
}
// x is greater than 5 (x 大于 5)
```

`if` 语句。

### If else 语句

```js
let x = 11;

if (x == 5) {
  println("x is 5");
} else if (x == 10) {
  println("x is 10");
} else {
  println("x is neither 5 nor 10");
}
// x is neither 5 nor 10 (x既不是5也不是10)
```

`if else` 语句。

### Match 语句

```rs
let x = 5;

match (x) {
  1 => println("one");
  2 => println("two");
  3 => println("three");
  _ => println("other");
}
// other (其他)
```

`match` 语句。

## 循环

### While 循环

```js
var x = 0;

while (x < 5) {
  print(x);
  x += 1;
}
// 01234
```

`while` 循环。

### Do while 循环

```js
var x = 0;

do {
  print(x);
  x += 1;
} while (x < 5);
// 01234
```

`do while` 循环。

### For 循环

```js
for (var i = 0; i < 5; i++) {
  print(i);
}
// 01234
```

经典的 `for` 循环。

### Loop 循环

```rs
loop {
  println("Press Ctrl+C to stop"); // 按 Ctrl+C 停止
}
```

无条件 `loop` 循环。

### Break

```js
var i = 0;
```

```rs
loop {
  if (i == 5) break;

  print(i);
  i += 1;
}
// 01234
```

使用 `break` 退出循环。

### Continue

```js
var i = 0;
```

```rs
loop {
  i += 1;
  if (i % 2 == 0) continue;

  print(i);

if (i == 5) break;
}
// 135
```

使用 `continue` 跳过循环体的其余部分。

## 字符串

### 字符串索引

```js
let s = "Hello";

println(s[0]); // H
println(s[1]); // e
println(s[4]); // o
```

字符串索引返回一个单字符字符串。

### 字符串切片

```js
let s = "Hello, World!";

println(s[0..5]);        // Hello
println(s[7..12]);       // World
```

传递一个范围来对字符串进行切片。

### 连接字符串

```js
let greeting = "Hi" + " there!";

println(greeting);
// Hi there!
```

使用 `+` 运算符连接字符串。

## 数组

### 数组索引

```js
let a = [1, 2, 3];

println(a[0]); // 1
println(a[1]); // 2
println(a[2]); // 3
```

数组索引返回一个元素。

### 数组切片

```js
let a = [1, 2, 3, 4];

println(a[0..2]);            // [1, 2, 3] (原文注释有误，应为 [1, 2])
println(a[1..3]);            // [2, 3, 4] (原文注释有误，应为 [2, 3])
println(a[2 .. len(a) - 1]); // [3, 4]
```

数组是零索引的。

### 追加元素

```js
var a = [1, 2];

a[] = 3;

println(a);
// [1, 2, 3]
```

数组是可变的。使用 `[]` 追加元素。

### 元素赋值

```js
var a = [1, 2, 3];

a[0] = 4;

println(a);
// [4, 2, 3]
```

更新数组中的元素。

### 连接数组

```js
let a = [1, 2];
let b = [3];
let c = a + b;

println(c);
// [1, 2, 3]
```

使用 `+` 运算符连接数组。

### 数组相减

```js
let a = [1, 2, 2, 3];
let b = [2];
let c = a - b;

println(c);
// [1, 3]
```

获取两个数组之间的差集。

## 函数和闭包

### 函数声明

```rs
fn sum(a, b) {
  return a + b;
}

println(sum(5, 10));
// 15
```

函数是一等公民。

### 函数调用

```rs
fn greet(name) {
  println("Hi, " + name + "!");
}

greet("John", "Doe");
// Hi, John!
```

参数数量会进行调整。

### 匿名函数

```js
let sum = |a, b| {
  return a + b;
};

println(sum(5, 10));
// 15
```

也支持匿名函数。

### 闭包

```js
let pi = 3.14;
```

```rs
fn area(r) {
  return pi * r * r;
}

println(area(5));
// 78.5
```

Hook 中的闭包仅捕获值。

### 高阶函数

```rs
fn apply(f, x) {
  return f(x);
}

fn double(x) {
  return x * 2;
}

println(apply(double, 5));
// 10
```

函数可以作为参数传递或返回。

### 函数的语法糖

```rs
fn factorial(n) =>
  if (n == 0) 1
  else n * factorial(n - 1);

println(factorial(5));
// 120
```

当函数体是单个表达式时，使用 `=>`。

### 递归

```rs
fn fib(n) {
  if (n < 2)
    return n;
  return fib(n - 1) + fib(n - 2);
}

println(fib(10));
// 55
```

支持递归。

### 内置函数

```js
println(type(5));
// number (数字)
println("1" + to_string(2));
// 12
println(len("foo"));
// 3
```

有许多内置函数。

### 更多内置函数

|             |           |             |
| ----------- | :-------- | :---------- |
| `print`     | `println` | `type`      |
| `is_nil`    | `is_bool` | `to_number` |
| `to_string` | `hex`     | `len`       |
| `exit`      | `assert`  | `panic`     |

参见：[内置函数](https://github.com/hook-lang/hook/blob/main/docs/built-in.md)

## 结构体 (Structs)

### 结构体

```rs
struct Point {
  x, y
}
```

```js
let p = Point { 5, 10 };

println(p);
// {x: 5, y: 10}
```

结构体是记录的原型。

### 访问字段

```js
println(p.x); // 5
println(p.y); // 10
```

使用 `.` 访问记录中的字段。

### 字段赋值

```js
p.x = 10;
p.y = 20;

println(p);
// {x: 10, y: 20}
```

更新记录中字段的值。

## 解构 (Destructuring)

### 解构数组

```js
let a = [1, 2];
let [x, y] = a;

println(x); // 1
println(y); // 2
```

变量被声明和赋值。

### 解构记录

```js
let p = { x: 5, y: 10 };
let { x } = p;

println(x);
// 5
```

使用 `{}` 解构记录。

### 占位符

```js
let a = [1, 2];
let [x] = a;
let [_, y] = a;

println(x); // 1
println(y); // 2
```

使用 `_` 跳过开头或中间的元素。

## 模块化 (Modularity)

### 导入模块

```js
import math;
```

```js
println(math.sqrt(25));
// 5
```

使用 `import` 将模块引入作用域。

### 导出符号

```rs
// my_module.hk
fn useful_fn() {
  return "Nothing";
}

return { useful: useful_fn };
```

返回一个包含要导出符号的记录。

### 导入本地模块

```python
import "./my_module.hk" as my;
```

```js
println(my.useful());
// Nothing (无内容)
```

指定本地模块的路径。

### 选择性导入

```js
import { pow, sqrt } from math;

let [ b, c ] = [ 4, 3 ];
let a = sqrt(pow(b, 2) + pow(c, 2));

println(a);
// 5
```

使用 `{}` 导入特定符号。

### 核心模块

|            |          |        |           |
| ---------- | :------- | :----- | :-------- |
| `math`     | `os`     | `io`   | `numbers` |
| `strings`  | `arrays` | `utf8` | `hashing` |
| `encoding` | `socket` | `json` | `lists`   |

参见：[核心模块](https://github.com/hook-lang/hook/blob/main/docs/core-modules.md)

### 扩展模块

|           |           |         |           |
| --------- | :-------- | :------ | :-------- |
| `bigint`  | `crypto`  | `curl`  | `fastcgi` |
| `geohash` | `leveldb` | `mysql` | `redis`   |
| `regex`   | `sqlite`  | `uuid`  | `zeromq`  |

这是扩展模块的列表。

### **io** 模块

```js
import { stderr, writeln } from io;

writeln(stderr, "Something went wrong");
// Something went wrong (出错了)
```

使用 `io` 模块打印到 `stderr`。

### **hashing** 模块

```python
import hashing as h;
```

```js
let d = h.sha256("Hello, world!");

println(hex(d));
// 315f5bdb76d078c43b8ac0064e4a...
```

`hashing` 模块提供哈希函数。

### **json** 模块

```js
import json;
```

```js
let j = '{"x": 1, "y": 2}';
let p = json.decode(j);

println(p.x); // 1

let k = json.encode(p);
println(type(k)); // string (字符串)
```

使用 `json` 模块处理 JSON。

## 错误处理

### 错误 {.col-span-2}

```js
println(to_int("foo"));

// 运行时错误：类型错误：参数 #1 不是可转换的字符串
//   在 to_int() (位于 <native>)
//   在 main() (位于 example.hk:1)
```

Hook 使用恐慌模式进行错误处理。当发生错误时，解释器停止。

### 语法错误

```js
println("Hello, World!");

// 语法错误：意外的文件结尾
//   在 main() (位于 example.hk:1,25)
```

Hook 具有严格的语法。

### 恐慌 (Panic)

```js
panic("Something went wrong");

// 恐慌：Something went wrong (出错了)
//   在 main() (位于 example.hk:1)
```

使用 `panic` 内置函数引发错误。

### 断言 (Assert) {.col-span-2}

```js
assert(5 > 10, "5 is not greater than 10");

// 断言：5 is not greater than 10 (5 不大于 10)
//   在 main() (位于 example.hk:1)
```

使用 `assert` 内置函数检查条件。

### 返回错误 {.col-span-2}

```rs
fn divide(a, b) {
  if (b == 0)
    return [nil, "division by zero"]; // 除零错误
  return a / b;
}

if (let [ok, err] = divide(5, 0); ok) {
  println(ok);
} else {
  println(err);
}
// division by zero (除零错误)
```

使用一个对组返回一个值和一个错误。

### 传递错误

```rs
if (let [ok, err] = divide(5, 0); err) {
  return [nil, err];
}
```

不处理错误而直接传递它。
