---
title: C++
date: 2021-06-01 11:51:44
background: bg-[#6d94c7]
tags:
categories:
  - 编程
intro: |
  C++ 快速参考备忘单，提供基本语法和方法。
plugins:
  - copyCode
  - runCode
---

## 入门

### hello.cpp

```cpp
#include <iostream>

int main() {
    std::cout << "你好，备忘单\n"; // "Hello CheatSheets" -> "你好，备忘单"
    return 0;
}
```

编译和运行

```shell script
$ g++ hello.cpp -o hello
$ ./hello
你好，备忘单
```

### 变量

```cpp
int number = 5;       // 整数
float f = 0.95;       // 浮点数
double PI = 3.14159;  // 浮点数
char yes = 'Y';       // 字符
std::string s = "ME"; // 字符串 (文本)
bool isRight = true;  // 布尔值

// 常量
const float RATE = 0.8;
```

---

```cpp
int age {25};         // C++11 起
std::cout << age;     // 打印 25
```

### 基本数据类型

| 数据类型  | 大小           | 范围                |
| --------- | -------------- | ------------------- |
| `int`     | 4 字节        | -2^31^ ^到^ 2^31^-1 |
| `float`   | 4 字节        | _N/A_               |
| `double`  | 8 字节        | _N/A_               |
| `char`    | 1 字节         | -128 ^到^ 127       |
| `bool`    | 1 字节         | true / false        |
| `void`    | _N/A_          | _N/A_               |
| `wchar_t` | 2 ^或^ 4 字节 | 1 宽字符    |

{.show-header}

### 用户输入

```cpp
int num;

std::cout << "输入一个数字: "; // "Type a number: " -> "输入一个数字: "
std::cin >> num;

std::cout << "你输入了 " << num; // "You entered " -> "你输入了 "
```

### 交换

```cpp
int a = 5, b = 10;
std::swap(a, b);

// 输出: a=10, b=5
std::cout << "a=" << a << ", b=" << b;
```

### 注释

```cpp
// C++ 中的单行注释

/* 这是 C++ 中的
   多行注释 */
```

### If 语句

```cpp
if (a == 10) {
    // 执行某些操作
}
```

参见: [条件语句](#c-conditionals)

### 循环

```cpp
for (int i = 0; i < 10; i++) {
    std::cout << i << "\n";
}
```

参见: [循环](#c-loops)

### 函数

```cpp
#include <iostream>

void hello(); // 声明

int main() {  // main 函数
    hello();    // 调用
}

void hello() { // 定义
    std::cout << "你好，备忘单!\n"; // "Hello CheatSheets!" -> "你好，备忘单!"
}
```

参见: [函数](#c-functions)

### 引用

```cpp
int i = 1;
int& ri = i; // ri 是 i 的引用

ri = 2; // i 现在变为 2
std::cout << "i=" << i;

i = 3;   // i 现在变为 3
std::cout << "ri=" << ri;
```

`ri` 和 `i` 指向相同的内存位置。

### 命名空间

```cpp
#include <iostream>
namespace ns1 {int val(){return 5;}}
int main()
{
    std::cout << ns1::val();
}
```

---

```cpp
#include <iostream>
namespace ns1 {int val(){return 5;}}
using namespace ns1;
using namespace std;
int main()
{
    cout << val();
}
```

命名空间允许在名称下使用全局标识符

## C++ 数组

### 声明

```cpp
std::array<int, 3> marks; // 定义
marks[0] = 92;
marks[1] = 97;
marks[2] = 98;

// 定义并初始化
std::array<int, 3> = {92, 97, 98};

// 带有空成员
std::array<int, 3> marks = {92, 97};
std::cout << marks[2]; // 输出: 0
```

### 操作

```cpp
┌─────┬─────┬─────┬─────┬─────┬─────┐
| 92  | 97  | 98  | 99  | 98  | 94  |
└─────┴─────┴─────┴─────┴─────┴─────┘
   0     1     2     3     4     5
```

---

```cpp
std::array<int, 6> marks = {92, 97, 98, 99, 98, 94};

// 打印第一个元素
std::cout << marks[0];

// 将第二个元素更改为 99
marks[1] = 99;

// 从用户处获取输入
std::cin >> marks[2];
```

### 显示

```cpp
char ref[5] = {'R', 'e', 'f'};

// 基于范围的 for 循环
for (const int &n : ref) {
    std::cout << std::string(1, n);
}

// 传统的 for 循环
for (int i = 0; i < sizeof(ref); ++i) {
    std::cout << ref[i];
}
```

### 多维数组

```cpp
     j0   j1   j2   j3   j4   j5
   ┌────┬────┬────┬────┬────┬────┐
i0 | 1  | 2  | 3  | 4  | 5  | 6  |
   ├────┼────┼────┼────┼────┼────┤
i1 | 6  | 5  | 4  | 3  | 2  | 1  |
   └────┴────┴────┴────┴────┴────┘
```

---

```cpp
int x[2][6] = {
    {1,2,3,4,5,6}, {6,5,4,3,2,1}
};
for (int i = 0; i < 2; ++i) {
    for (int j = 0; j < 6; ++j) {
        std::cout << x[i][j] << " ";
    }
}
// 输出: 1 2 3 4 5 6 6 5 4 3 2 1
```

## C++ 条件语句

### If 子句

```cpp
if (a == 10) {
    // 执行某些操作
}
```

---

```cpp
int number = 16;

if (number % 2 == 0)
{
    std::cout << "偶数"; // "even" -> "偶数"
}
else
{
    std::cout << "奇数"; // "odd" -> "奇数"
}

// 输出: 偶数
```

### Else if 语句

```cpp
int score = 99;
if (score == 100) {
    std::cout << "棒极了"; // "Superb" -> "棒极了"
}
else if (score >= 90) {
    std::cout << "优秀"; // "Excellent" -> "优秀"
}
else if (score >= 80) {
    std::cout << "非常好"; // "Very Good" -> "非常好"
}
else if (score >= 70) {
    std::cout << "良好"; // "Good" -> "良好"
}
else if (score >= 60)
    std::cout << "及格"; // "OK" -> "及格"
else
    std::cout << "什么?"; // "What?" -> "什么?"
```

### 运算符 {.row-span-2}

#### 关系运算符

|          |                              |
| -------- | ---------------------------- |
| `a == b` | a 等于 b              |
| `a != b` | a 不等于 b          |
| `a < b`  | a 小于 b             |
| `a > b`  | a 大于 b               |
| `a <= b` | a 小于或等于 b |
| `a >= b` | a 大于或等于 b   |

#### 赋值运算符

| 示例  | 等同于    |
| -------- | ---------------- |
| `a += b` | _即_ a = a + b  |
| `a -= b` | _即_ a = a - b  |
| `a *= b` | _即_ a = a \* b |
| `a /= b` | _即_ a = a / b  |
| `a %= b` | _即_ a = a % b  |

#### 逻辑运算符

| 示例                     | 含义                |
| --------------------------- | ---------------------- |
| `exp1 && exp2`              | 两者都为真 _(与)_  |
| <code>exp1 \|\| exp2</code> | 任一为真 _(或)_  |
| `!exp`                      | `exp` 为假 _(非)_ |

#### 位运算符

| 运算符            | 描述             |
| ------------------- | ----------------------- |
| `a & b`             | 按位与              |
| <code>a \| b</code> | 按位或               |
| `a ^ b`             | 按位异或              |
| `~ a`               | 按位取反 |
| `a << b`            | 按位左移      |
| `a >> b`            | 按位右移      |

### 三元运算符

```
           ┌── 真 ──┐
结果 = 条件 ? 表达式1 : 表达式2;
           └───── 假 ─────┘
```

---

```cpp
int x = 3, y = 5, max;
max = (x > y) ? x : y;

// 输出: 5
std::cout << max << std::endl;
```

---

```cpp
int x = 3, y = 5, max;
if (x > y) {
    max = x;
} else {
    max = y;
}
// 输出: 5
std::cout << max << std::endl;
```

### Switch 语句

```cpp
int num = 2;
switch (num) {
    case 0:
        std::cout << "零"; // "Zero" -> "零"
        break;
    case 1:
        std::cout << "一"; // "One" -> "一"
        break;
    case 2:
        std::cout << "二"; // "Two" -> "二"
        break;
    case 3:
        std::cout << "三"; // "Three" -> "三"
        break;
    default:
        std::cout << "什么?"; // "What?" -> "什么?"
        break;
}
```

## C++ 循环

### While

```cpp
int i = 0;
while (i < 6) {
    std::cout << i++;
}

// 输出: 012345
```

### Do-while

```cpp
int i = 1;
do {
    std::cout << i++;
} while (i <= 5);

// 输出: 12345
```

### Continue 语句

```cpp
for (int i = 0; i < 10; i++) {
    if (i % 2 == 0) {
        continue;
    }
    std::cout << i;
} // 输出: 13579
```

### 无限循环

```cpp
while (true) { // true 或 1
    std::cout << "无限循环"; // "infinite loop" -> "无限循环"
}
```

---

```cpp
for (;;) {
    std::cout << "无限循环";
}
```

---

```cpp
for(int i = 1; i > 0; i++) {
    std::cout << "无限循环";
}
```

### for_each (C++11 起)

```cpp
#include <iostream>
#include <array>

int main()
{
    auto print = [](int num) { std::cout << num << std::endl; };

    std::array<int, 4> arr = {1, 2, 3, 4};
    std::for_each(arr.begin(), arr.end(), print);
    return 0;
}
```

### 基于范围的循环 (C++11 起)

```cpp
for (int n : {1, 2, 3, 4, 5}) {
    std::cout << n << " ";
}
// 输出: 1 2 3 4 5
```

---

```cpp
std::string hello = "r3f.cn";
for (char c: hello)
{
    std::cout << c << " ";
}
// 输出: Q u i c k R e f . M E (保持原样，因为这是字符串内容)
```

### Break 语句

```cpp
int password, times = 0;
while (password != 1234) {
    if (times++ >= 3) {
        std::cout << "已锁定!\n"; // "Locked!" -> "已锁定!"
        break;
    }
    std::cout << "密码: "; // "Password: " -> "密码: "
    std::cin >> password; // 输入
}
```

### 几种变体

```cpp
for (int i = 0, j = 2; i < 3; i++, j--){
    std::cout << "i=" << i << ",";
    std::cout << "j=" << j << ";";
}
// 输出: i=0,j=2;i=1,j=1;i=2,j=0;
```

## C++ 函数

### 参数和返回值

```cpp
#include <iostream>

int add(int a, int b) {
    return a + b;
}

int main() {
    std::cout << add(10, 20);
}
```

`add` 是一个接受 2 个 int 类型参数并返回 int 类型的函数

### 重载

```cpp
void fun(string a, string b) {
    std::cout << a + " " + b;
}
void fun(string a) {
    std::cout << a;
}
void fun(int a) {
    std::cout << a;
}
```

### 内置函数

```cpp
#include <iostream>
#include <cmath> // 导入库

int main() {
    // sqrt() 来自 cmath
    std::cout << sqrt(9);
}
```

## C++ 类和对象 {.cols-2}

### 定义类

```cpp
class MyClass {
  public:             // 访问修饰符
    int myNum;        // 属性 (int 变量)
    string myString;  // 属性 (string 变量)
};

```

### 创建对象

```cpp
MyClass myObj;  // 创建 MyClass 的对象

myObj.myNum = 15;          // 将 myNum 的值设置为 15
myObj.myString = "你好";  // 将 myString 的值设置为 "你好" ( "Hello" -> "你好")

cout << myObj.myNum << endl;         // 输出 15
cout << myObj.myString << endl;      // 输出 "你好"

```

### 构造函数

```cpp
class MyClass {
  public:
    int myNum;
    string myString;
    MyClass() {  // 构造函数
      myNum = 0;
      myString = "";
    }
};

MyClass myObj;  // 创建 MyClass 的对象

cout << myObj.myNum << endl;         // 输出 0
cout << myObj.myString << endl;      // 输出 ""

```

### 析构函数

```cpp
class MyClass {
  public:
    int myNum;
    string myString;
    MyClass() {  // 构造函数
      myNum = 0;
      myString = "";
    }
    ~MyClass() {  // 析构函数
      cout << "对象已销毁。" << endl; // "Object destroyed." -> "对象已销毁。"
    }
};

MyClass myObj;  // 创建 MyClass 的对象

// 此处代码...

// 当程序退出作用域时，对象会自动销毁


```

### 类方法

```cpp
class MyClass {
  public:
    int myNum;
    string myString;
    void myMethod() {  // 在类内部定义的方法/函数
      cout << "世界你好!" << endl; // "Hello World!" -> "世界你好!"
    }
};

MyClass myObj;  // 创建 MyClass 的对象
myObj.myMethod();  // 调用方法
```

### 访问修饰符

```cpp
class MyClass {
  public:     // 公共访问修饰符
    int x;    // 公共属性
  private:    // 私有访问修饰符
    int y;    // 私有属性
  protected:  // 受保护访问修饰符
    int z;    // 受保护属性
};

MyClass myObj;
myObj.x = 25;  // 允许 (公共)
myObj.y = 50;  // 不允许 (私有)
myObj.z = 75;  // 不允许 (受保护)

```

### Getters 和 Setters

```cpp
class MyClass {
  private:
    int myNum;
  public:
    void setMyNum(int num) {  // Setter
      myNum = num;
    }
    int getMyNum() {  // Getter
      return myNum;
    }
};

MyClass myObj;
myObj.setMyNum(15);  // 将 myNum 的值设置为 15
cout << myObj.getMyNum() << endl;  // 输出 15

```

### 继承

```cpp
class Vehicle {
  public:
    string brand = "福特"; // "Ford" -> "福特"
    void honk() {
      cout << "嘟嘟，嘟嘟!" << endl; // "Tuut, tuut!" -> "嘟嘟，嘟嘟!"
    }
};

class Car : public Vehicle {
  public:
    string model = "野马"; // "Mustang" -> "野马"
};

Car myCar;
myCar.honk();  // 输出 "嘟嘟，嘟嘟!"
cout << myCar.brand + " " + myCar.model << endl;  // 输出 "福特 野马"
```

## C++ 预处理器

### 预处理器 {.row-span-3}

- [if](https://en.cppreference.com/w/cpp/preprocessor/conditional)
- [elif](https://en.cppreference.com/w/cpp/preprocessor/conditional)
- [else](https://en.cppreference.com/w/cpp/preprocessor/conditional)
- [endif](https://en.cppreference.com/w/cpp/preprocessor/conditional)
- [ifdef](https://en.cppreference.com/w/cpp/preprocessor/conditional)
- [ifndef](https://en.cppreference.com/w/cpp/preprocessor/conditional)
- [define](https://en.cppreference.com/w/cpp/preprocessor/replace)
- [undef](https://en.cppreference.com/w/cpp/preprocessor/replace)
- [include](https://en.cppreference.com/w/cpp/preprocessor/include)
- [line](https://en.cppreference.com/w/cpp/preprocessor/line)
- [error](https://en.cppreference.com/w/cpp/preprocessor/error)
- [pragma](https://en.cppreference.com/w/cpp/preprocessor/impl)
- [defined](https://en.cppreference.com/w/cpp/preprocessor/conditional)
- [\_\_has_include](https://en.cppreference.com/w/cpp/feature_test)
- [\_\_has_cpp_attribute](https://en.cppreference.com/w/cpp/feature_test)
- [export](https://en.cppreference.com/w/cpp/keyword/export)
- [import](https://en.cppreference.com/mwiki/index.php?title=cpp/keyword/import&action=edit&redlink=1)
- [module](https://en.cppreference.com/mwiki/index.php?title=cpp/keyword/module&action=edit&redlink=1)

{.marker-none .cols-2}

### Includes (包含)

```cpp
#include "iostream"
#include <iostream>
```

### Defines (定义)

```cpp
#define FOO
#define FOO "你好" // "hello" -> "你好"

#undef FOO
```

### If {.row-span-2}

```cpp
#ifdef DEBUG
  console.log('嗨'); // 'hi' -> '嗨'
#elif defined VERBOSE
  ...
#else
  ...
#endif
```

### Error (错误)

```cpp
#if VERSION == 2.0
  #error 不支持 // "Unsupported" -> "不支持"
  #warning 并非真正支持 // "Not really supported" -> "并非真正支持"
#endif
```

### Macro (宏)

```cpp
#define DEG(x) ((x) * 57.29)
```

### Token concat (标记连接)

```cpp
#define DST(name) name##_s name##_t
DST(object);   #=> object_s object_t;
```

### Stringification (字符串化)

```cpp
#define STR(name) #name
char * a = STR(object);   #=> char * a = "object";
```

### file and line (文件和行号)

```cpp
#define LOG(msg) console.log(__FILE__, __LINE__, msg)
#=> console.log("file.txt", 3, "嘿") // "hey" -> "嘿"
```

## 其他

### 转义序列

| 转义序列 | 字符            |
| ---------------- | --------------------- |
| `\b`             | 退格             |
| `\f`             | 换页             |
| `\n`             | 换行               |
| `\r`             | 回车                |
| `\t`             | 水平制表符        |
| `\v`             | 垂直制表符        |
| `\\`             | 反斜杠             |
| `\'`             | 单引号 |
| `\"`             | 双引号 |
| `\?`             | 问号         |
| `\0`             | 空字符        |

### 关键字 {.col-span-2 .row-span-2}

- [alignas](https://en.cppreference.com/w/cpp/keyword/alignas)
- [alignof](https://en.cppreference.com/w/cpp/keyword/alignof)
- [and](https://en.cppreference.com/w/cpp/keyword/and)
- [and_eq](https://en.cppreference.com/w/cpp/keyword/and_eq)
- [asm](https://en.cppreference.com/w/cpp/keyword/asm)
- [atomic_cancel](https://en.cppreference.com/w/cpp/keyword/atomic_cancel)
- [atomic_commit](https://en.cppreference.com/w/cpp/keyword/atomic_commit)
- [atomic_noexcept](https://en.cppreference.com/w/cpp/keyword/atomic_noexcept)
- [auto](https://en.cppreference.com/w/cpp/keyword/auto)
- [bitand](https://en.cppreference.com/w/cpp/keyword/bitand)
- [bitor](https://en.cppreference.com/w/cpp/keyword/bitor)
- [bool](https://en.cppreference.com/w/cpp/keyword/bool)
- [break](https://en.cppreference.com/w/cpp/keyword/break)
- [case](https://en.cppreference.com/w/cpp/keyword/case)
- [catch](https://en.cppreference.com/w/cpp/keyword/catch)
- [char](https://en.cppreference.com/w/cpp/keyword/char)
- [char8_t](https://en.cppreference.com/w/cpp/keyword/char8_t)
- [char16_t](https://en.cppreference.com/w/cpp/keyword/char16_t)
- [char32_t](https://en.cppreference.com/w/cpp/keyword/char32_t)
- [class](https://en.cppreference.com/w/cpp/keyword/class)
- [compl](https://en.cppreference.com/w/cpp/keyword/compl)
- [concept](https://en.cppreference.com/w/cpp/keyword/concept)
- [const](https://en.cppreference.com/w/cpp/keyword/const)
- [consteval](https://en.cppreference.com/w/cpp/keyword/consteval)
- [constexpr](https://en.cppreference.com/w/cpp/keyword/constexpr)
- [constinit](https://en.cppreference.com/w/cpp/keyword/constinit)
- [const_cast](https://en.cppreference.com/w/cpp/keyword/const_cast)
- [continue](https://en.cppreference.com/w/cpp/keyword/continue)
- [co_await](https://en.cppreference.com/w/cpp/keyword/co_await)
- [co_return](https://en.cppreference.com/w/cpp/keyword/co_return)
- [co_yield](https://en.cppreference.com/w/cpp/keyword/co_yield)
- [decltype](https://en.cppreference.com/w/cpp/keyword/decltype)
- [default](https://en.cppreference.com/w/cpp/keyword/default)
- [delete](https://en.cppreference.com/w/cpp/keyword/delete)
- [do](https://en.cppreference.com/w/cpp/keyword/do)
- [double](https://en.cppreference.com/w/cpp/keyword/double)
- [dynamic_cast](https://en.cppreference.com/w/cpp/keyword/dynamic_cast)
- [else](https://en.cppreference.com/w/cpp/keyword/else)
- [enum](https://en.cppreference.com/w/cpp/keyword/enum)
- [explicit](https://en.cppreference.com/w/cpp/keyword/explicit)
- [export](https://en.cppreference.com/w/cpp/keyword/export)
- [extern](https://en.cppreference.com/w/cpp/keyword/extern)
- [false](https://en.cppreference.com/w/cpp/keyword/false)
- [float](https://en.cppreference.com/w/cpp/keyword/float)
- [for](https://en.cppreference.com/w/cpp/keyword/for)
- [friend](https://en.cppreference.com/w/cpp/keyword/friend)
- [goto](https://en.cppreference.com/w/cpp/keyword/goto)
- [if](https://en.cppreference.com/w/cpp/keyword/if)
- [inline](https://en.cppreference.com/w/cpp/keyword/inline)
- [int](https://en.cppreference.com/w/cpp/keyword/int)
- [long](https://en.cppreference.com/w/cpp/keyword/long)
- [mutable](https://en.cppreference.com/w/cpp/keyword/mutable)
- [namespace](https://en.cppreference.com/w/cpp/keyword/namespace)
- [new](https://en.cppreference.com/w/cpp/keyword/new)
- [noexcept](https://en.cppreference.com/w/cpp/keyword/noexcept)
- [not](https://en.cppreference.com/w/cpp/keyword/not)
- [not_eq](https://en.cppreference.com/w/cpp/keyword/not_eq)
- [nullptr](https://en.cppreference.com/w/cpp/keyword/nullptr)
- [operator](https://en.cppreference.com/w/cpp/keyword/operator)
- [or](https://en.cppreference.com/w/cpp/keyword/or)
- [or_eq](https://en.cppreference.com/w/cpp/keyword/or_eq)
- [private](https://en.cppreference.com/w/cpp/keyword/private)
- [protected](https://en.cppreference.com/w/cpp/keyword/protected)
- [public](https://en.cppreference.com/w/cpp/keyword/public)
- [reflexpr](https://en.cppreference.com/w/cpp/keyword/reflexpr)
- [register](https://en.cppreference.com/w/cpp/keyword/register)
- [reinterpret_cast](https://en.cppreference.com/w/cpp/keyword/reinterpret_cast)
- [requires](https://en.cppreference.com/w/cpp/keyword/requires)
- [return](https://en.cppreference.com/w/cpp/language/return)
- [short](https://en.cppreference.com/w/cpp/keyword/short)
- [signed](https://en.cppreference.com/w/cpp/keyword/signed)
- [sizeof](https://en.cppreference.com/w/cpp/keyword/sizeof)
- [static](https://en.cppreference.com/w/cpp/keyword/static)
- [static_assert](https://en.cppreference.com/w/cpp/keyword/static_assert)
- [static_cast](https://en.cppreference.com/w/cpp/keyword/static_cast)
- [struct](https://en.cppreference.com/w/cpp/keyword/struct)
- [switch](https://en.cppreference.com/w/cpp/keyword/switch)
- [synchronized](https://en.cppreference.com/w/cpp/keyword/synchronized)
- [template](https://en.cppreference.com/w/cpp/keyword/template)
- [this](https://en.cppreference.com/w/cpp/keyword/this)
- [thread_local](https://en.cppreference.com/w/cpp/keyword/thread_local)
- [throw](https://en.cppreference.com/w/cpp/keyword/throw)
- [true](https://en.cppreference.com/w/cpp/keyword/true)
- [try](https://en.cppreference.com/w/cpp/keyword/try)
- [typedef](https://en.cppreference.com/w/cpp/keyword/typedef)
- [typeid](https://en.cppreference.com/w/cpp/keyword/typeid)
- [typename](https://en.cppreference.com/w/cpp/keyword/typename)
- [union](https://en.cppreference.com/w/cpp/keyword/union)
- [unsigned](https://en.cppreference.com/w/cpp/keyword/unsigned)
- [using](https://en.cppreference.com/w/cpp/keyword/using)
- [virtual](https://en.cppreference.com/w/cpp/keyword/virtual)
- [void](https://en.cppreference.com/w/cpp/keyword/void)
- [volatile](https://en.cppreference.com/w/cpp/keyword/volatile)
- [wchar_t](https://en.cppreference.com/w/cpp/keyword/wchar_t)
- [while](https://en.cppreference.com/w/cpp/keyword/while)
- [xor](https://en.cppreference.com/w/cpp/keyword/xor)
- [xor_eq](https://en.cppreference.com/w/cpp/keyword/xor_eq)
- [final](https://en.cppreference.com/w/cpp/language/final)
- [override](https://en.cppreference.com/w/cpp/language/override)
- [transaction_safe](https://en.cppreference.com/w/cpp/language/transactional_memory)
- [transaction_safe_dynamic](https://en.cppreference.com/w/cpp/language/transactional_memory) {.marker-none .cols-5}

### 预处理器

- [if](https://en.cppreference.com/w/cpp/preprocessor/conditional)
- [elif](https://en.cppreference.com/w/cpp/preprocessor/conditional)
- [else](https://en.cppreference.com/w/cpp/preprocessor/conditional)
- [endif](https://en.cppreference.com/w/cpp/preprocessor/conditional)
- [ifdef](https://en.cppreference.com/w/cpp/preprocessor/conditional)
- [ifndef](https://en.cppreference.com/w/cpp/preprocessor/conditional)
- [define](https://en.cppreference.com/w/cpp/preprocessor/replace)
- [undef](https://en.cppreference.com/w/cpp/preprocessor/replace)
- [include](https://en.cppreference.com/w/cpp/preprocessor/include)
- [line](https://en.cppreference.com/w/cpp/preprocessor/line)
- [error](https://en.cppreference.com/w/cpp/preprocessor/error)
- [pragma](https://en.cppreference.com/w/cpp/preprocessor/impl)
- [defined](https://en.cppreference.com/w/cpp/preprocessor/conditional)
- [\_\_has_include](https://en.cppreference.com/w/cpp/feature_test)
- [\_\_has_cpp_attribute](https://en.cppreference.com/w/cpp/feature_test)
- [export](https://en.cppreference.com/w/cpp/keyword/export)
- [import](https://en.cppreference.com/mwiki/index.php?title=cpp/keyword/import&action=edit&redlink=1)
- [module](https://en.cppreference.com/mwiki/index.php?title=cpp/keyword/module&action=edit&redlink=1) {.marker-none
  .cols-2}

## 另请参阅

- [C++ 信息图表和备忘单](https://hackingcpp.com/cpp/cheat_sheets.html) _(hackingcpp.com)_

- [C++ 参考](https://en.cppreference.com/w/) _(cppreference.com)_
- [C++ 语言教程](http://www.cplusplus.com/doc/tutorial/) _(cplusplus.com)_

