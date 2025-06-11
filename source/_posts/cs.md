---
title: C#
date: 2021-12-14 12:22:00
background: bg-[#8c4c8a]
tags:
  - object-oriented
  - class
categories:
  - 编程
intro: |
  C# 快速参考备忘单，提供基本语法和方法。
plugins:
  - copyCode
---

## 入门

### Hello.cs

```cs
class Hello {
  // main 方法
  static void Main(string[] args)
  {
    // 输出: Hello, world!
    Console.WriteLine("Hello, world!");
  }
}
```

为新的控制台应用程序创建项目目录

```cs
$ dotnet new console
```

列出所有应用程序模板

```cs
$ dotnet new list
```

编译和运行（确保您在项目目录中）

```shell script
$ dotnet run
Hello, world!
```

### 变量

```cs
int intNum = 9;
long longNum = 9999999;
float floatNum = 9.99F;
double doubleNum = 99.999;
decimal decimalNum = 99.9999M;
char letter = 'D';
bool @bool = true;
string site = "r3f.cn";

var num = 999;
var str = "999";
var bo = false;
```

### 基本数据类型

| 数据类型 | 大小             | 范围                      |
| -------- | ---------------- | ------------------------- |
| `int`    | 4 字节           | -2^31^ ^到^ 2^31^-1       |
| `long`   | 8 字节           | -2^63^ ^到^ 2^63^-1       |
| `float`  | 4 字节           | 6 ^到^ 7 位小数           |
| `double` | 8 字节           | 15 位小数                 |
| `decimal`| 16 字节          | 28 ^到^ 29 位小数         |
| `char`   | 2 字节           | 0 ^到^ 65535              |
| `bool`   | 1 比特           | true / false              |
| `string` | 每字符 2 字节    | _不适用_                  |

{.show-header}

### 注释

```cs
// 单行注释

/* 多行
   注释 */

// TODO: 在 Visual Studio 的任务列表中添加注释

/// 用于文档的单行注释

/** 用于文档的
    多行注释 **/

```

### 字符串

```cs
string first = "John";
string last = "Doe";

// 字符串连接
string name = first + " " + last;
Console.WriteLine(name); // => John Doe
```

另请参阅：[字符串](#c-strings)

### 用户输入

```cs
Console.WriteLine("输入数字:");
if(int.TryParse(Console.ReadLine(),out int input))
{
  // 输入已验证
  Console.WriteLine($"您输入了 {input}");
}
```

### 条件语句

```cs
int j = 10;

if (j == 10) {
  Console.WriteLine("我会打印出来");
} else if (j > 10) {
  Console.WriteLine("我不会");
} else {
  Console.WriteLine("我也不会");
}
```

### 数组

```cs
char[] chars = new char[10];
chars[0] = 'a';
chars[1] = 'b';

string[] letters = {"A", "B", "C"};
int[] mylist = {100, 200};
bool[] answers = {true, false};
```

### 循环

```cs
int[] numbers = {1, 2, 3, 4, 5};

for(int i = 0; i < numbers.Length; i++) {
  Console.WriteLine(numbers[i]);
}
```

---

```cs
foreach(int num in numbers) {
  Console.WriteLine(num);
}
```

## C# 字符串

### 字符串连接

```cs
string first = "John";
string last = "Doe";

string name = first + " " + last;
Console.WriteLine(name); // => John Doe
```

### 字符串插值

```cs
string first = "John";
string last = "Doe";

string name = $"{first} {last}";
Console.WriteLine(name); // => John Doe
```

### 字符串成员 {.row-span-2}

| 成员       | 描述                                                                                                                               |
| ---------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| Length     | 返回字符串长度的属性。                                                                                                               |
| Compare()  | 比较两个字符串的静态方法。                                                                                                           |
| Contains() | 判断字符串是否包含特定的子字符串。                                                                                                   |
| Equals()   | 判断两个字符串是否具有相同的字符数据。                                                                                               |
| Format()   | 通过 {0} 表示法并使用其他基本类型来格式化字符串。                                                                                    |
| Trim()     | 从前导和尾随字符中移除所有特定字符的实例。默认为移除前导和尾随空格。                                                                   |
| Split()    | 移除提供的字符，并根据两侧剩余的字符创建一个数组。                                                                                   |

{.show-header}

### 原义字符串

```cs {.wrap}
string longString = @"我可以在这里输入任何字符 !#@$%^&*()__+ '' \n \t 除了双引号，它们都会被按字面意思处理。它甚至可以处理多行。";
```

### 成员示例

```cs
// 使用 System.String 的属性
string lengthOfString = "多长?";
lengthOfString.Length           // => 3 (注意：此处原文为 "How long?" 长度为9，翻译后长度会变化，这里按翻译后的字面长度)

// 使用 System.String 的方法
lengthOfString.Contains("多"); // => true
```

## 其他

### 通用 .NET 术语 {.col-span-2}

| 术语                          | 定义                                                                                                                                                                                          |
| ----------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 运行时 (Runtime)              | 执行给定已编译代码单元所需的服务集合。                                                                                                                                                              |
| 公共语言运行时 (CLR)          | 主要负责定位、加载和管理 .NET 对象。CLR 还处理内存管理、应用程序托管、线程协调、执行安全检查以及其他底层细节。                                                                                        |
| 托管代码 (Managed code)       | 在 .NET 运行时上编译和运行的代码。C#/F#/VB 是示例。                                                                                                                                                 |
| 非托管代码 (Unmanaged code)   | 直接编译为机器代码且不能由 .NET 运行时直接托管的代码。不包含自动内存管理、垃圾回收等。从 C/C++ 创建的 DLL 是示例。                                                                                      |

{.show-header}

