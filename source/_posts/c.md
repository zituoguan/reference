---
title: C 语言
date: 2022-12-30 09:51:44
background: bg-[#2a338a]
tags:
categories:
  - 编程
intro: |
  C 语言快速参考备忘单，提供基本语法和方法。
plugins:
  - copyCode
  - runCode
---

## 入门

### hello.c {.row-span-2}

```c
#include <stdio.h>

int main(void) {
  printf("Hello World!\n");

  return 0;
}
```

使用 `gcc` 编译 `hello.c` 文件

```bash
$ gcc -Wall -g hello.c -o hello
```

运行编译后的二进制文件 `hello`

```bash
$ ./hello
```

输出 => Hello World!

### 变量 {.row-span-2}

```c
int myNum = 15;

int myNum2; // 不赋值，然后赋值
myNum2 = 15;

int myNum3 = 15; // myNum3 是 15
myNum3 = 10;     // myNum3 现在是 10

float myFloat = 5.99; // 浮点数
char myLetter = 'D';  // 字符

int x = 5;
int y = 6;
int sum = x + y; // 将变量相加得到 sum

// 声明多个变量
int a = 5, b = 6, c = 50;
```

### 常量

```c
const int minutesPerHour = 60;
const float PI = 3.14;
```

最佳实践

```c
const int BIRTHYEAR = 1980;
```

### 注释

```c
// 这是单行注释
printf("Hello World!\n"); // 可以在文件中的任何位置注释

/* 多行注释，
   在屏幕上打印 Hello World!
   这很棒 */
```

### 打印文本

```c
printf("我正在学习 C 语言。\n");
int testInteger = 5;
printf("数字 = %d\n", testInteger);

float f = 5.99; // 浮点数
printf("值 = %f\n", f);

short a = 0b1010110; // 二进制数
int b = 02713; // 八进制数
long c = 0X1DAB83; // 十六进制数

// 以八进制形式输出
printf("a=%ho, b=%o, c=%lo\n", a, b, c);
// 输出 => a=126, b=2713, c=7325603

// 以十进制形式输出
printf("a=%hd, b=%d, c=%ld\n", a, b, c);
// 输出 => a=86, b=1483, c=1944451

// 以十六进制形式输出 (字母小写)
printf("a=%hx, b=%x, c=%lx\n", a, b, c);
// 输出 => a=56, b=5cb, c=1dab83

// 以十六进制形式输出 (字母大写)
printf("a=%hX, b=%X, c=%lX\n", a, b, c);
// 输出 => a=56, b=5CB, c=1DAB83
```

### 控制空格数量

```c
int a1 = 20, a2 = 345, a3 = 700;
int b1 = 56720, b2 = 9999, b3 = 20098;
int c1 = 233, c2 = 205, c3 = 1;
int d1 = 34, d2 = 0, d3 = 23;

printf("%-9d %-9d %-9d\n", a1, a2, a3);
printf("%-9d %-9d %-9d\n", b1, b2, b3);
printf("%-9d %-9d %-9d\n", c1, c2, c3);
printf("%-9d %-9d %-9d\n", d1, d2, d3);
```

输出结果

```bash
20        345       700
56720     9999      20098
233       205       1
34        0         23
```

在 `%-9d` 中，`d` 表示以 `10` 进制输出，`9` 表示至少占用 `9` 个字符宽度，宽度不足则用空格填充，`-` 表示左对齐。

### 字符串

```c
char greetings[] = "Hello World!";
printf("%s", greetings);
```

访问字符串

```c
char greetings[] = "Hello World!";
printf("%c", greetings[0]);
```

修改字符串

```c
char greetings[] = "Hello World!";
greetings[0] = 'J';

printf("%s", greetings);
// 打印 "Jello World!"
```

创建字符串的另一种方法

```c
char greetings[] = {'H','e','l','l','\0'};

printf("%s", greetings);
// 打印 "Hell!"
```

使用字符指针创建字符串 (字符串字面量)

```c
char *greetings = "Hello";
printf("%s", greetings);
// 打印 "Hello!"
```

**注意**: 字符串字面量可能存储在内存的只读区域。修改字符串字面量会引发未定义行为。你不能修改它！

`C` 语言**没有** String 类型，使用 `char` 类型并创建一个字符 `数组`。

### 条件 {.row-span-2}

```c
int time = 20;
if (time < 18) {
  printf("Goodbye!\n");
} else {
  printf("Good evening!\n");
}
// 输出 -> "Good evening!"
int time = 22;
if (time < 10) {
  printf("Good morning!\n");
} else if (time < 20) {
  printf("Goodbye!\n");
} else {
  printf("Good evening!\n");
}
// 输出 -> "Good evening!"
```

### 三元运算符 {.col-span-2}

```c
int age = 20;
(age > 19) ? printf("Adult\n") : printf("Teenager\n");
```

### Switch 语句

```c
int day = 4;

switch (day) {
  case 3: printf("Wednesday\n"); break;
  case 4: printf("Thursday\n"); break;
  default:
    printf("Weekend!\n");
}
// 输出 -> "Thursday" (day 4)
```

### While 循环

```c
int i = 0;

while (i < 5) {
  printf("%d\n", i);
  i++;
}
```

**注意**: 不要忘记增加条件中使用的变量，否则循环将永远不会结束并变成“无限循环”！

### Do/While 循环

```c
int i = 0;

do {
  printf("%d\n", i);
  i++;
} while (i < 5);
```

### For 循环

```c
for (int i = 0; i < 5; i++) {
  printf("%d\n", i);
}
```

### 跳出循环 Break/Continue {.row-span-2}

```c
for (int i = 0; i < 10; i++) {
  if (i == 4) {
    break;
  }
  printf("%d\n", i);
}
```

当 `i` 等于 `4` 时跳出循环。

```c
for (int i = 0; i < 10; i++) {
  if (i == 4) {
    continue;
  }
  printf("%d\n", i);
}
```

跳过值为 `4` 的示例。

### While Break 示例

```c
int i = 0;

while (i < 10) {
  if (i == 4) {
    break;
  }
  printf("%d\n", i);

  i++;
}
```

### While continue 示例

```c
int i = 0;

while (i < 10) {
  i++;

  if (i == 4) {
    continue;
  }
  printf("%d\n", i);
}
```

### 数组 {.row-span-2}

```c
int myNumbers[] = {25, 50, 75, 100};

printf("%d", myNumbers[0]);
// 输出 25
```

更改数组元素

```c
int myNumbers[] = {25, 50, 75, 100};
myNumbers[0] = 33;

printf("%d", myNumbers[0]);
```

遍历数组

```c
int myNumbers[] = {25, 50, 75, 100};
int i;

for (i = 0; i < 4; i++) {
  printf("%d\n", myNumbers[i]);
}
```

设置数组大小

```c
// 声明一个包含四个整数的数组：
int myNumbers[4];

// 添加元素
myNumbers[0] = 25;
myNumbers[1] = 50;
myNumbers[2] = 75;
myNumbers[3] = 100;
```

### 枚举 Enum {.col-span-2}

```c
enum week { Mon = 1, Tues, Wed, Thurs, Fri, Sat, Sun };
```

定义枚举变量

```c
enum week a, b, c;
enum week { Mon = 1, Tues, Wed, Thurs, Fri, Sat, Sun } a, b, c;
```

使用枚举变量，可以将列表中的值赋给它

```c
enum week { Mon = 1, Tues, Wed, Thurs, Fri, Sat, Sun };
enum week a = Mon, b = Wed, c = Sat;
// 或者
enum week{ Mon = 1, Tues, Wed, Thurs, Fri, Sat, Sun } a = Mon, b = Wed, c = Sat;
```

### 枚举示例应用

```c
enum week {Mon = 1, Tues, Wed, Thurs} day;

scanf("%d", &day);

switch(day) {
  case Mon: puts("Monday"); break;
  case Tues: puts("Tuesday"); break;
  case Wed: puts("Wednesday"); break;
  case Thurs: puts("Thursday"); break;
  default: puts("Error!");
}
```

### 用户输入

```c
// 创建一个整型变量来存储从用户那里获取的数字
int myNum;

// 要求用户输入一个数字
printf("输入一个数字: ");

// 获取并保存用户输入的数字
scanf("%d", &myNum);

// 输出用户输入的数字
printf("你输入的数字是: %d\n", myNum);
```

### 用户输入字符串

```c
// 创建一个字符串
char firstName[30];
// 要求用户输入一些文本
printf("输入你的名字: ");
// 获取并保存文本
scanf("%s", &firstName);
// 输出文本
printf("你好 %s。\n", firstName);
```

### 内存地址

创建变量时，会为其分配一个内存地址。

```c
int myAge = 43;

printf("%p", &myAge);
// 输出: 0x7ffe5367e044
```

要访问它，请使用引用运算符 (`&`)。

### 创建指针

```c
int myAge = 43; // 一个 int 变量
printf("%d\n", myAge); // 输出 myAge 的值 (43)

// 输出 myAge 的内存地址 (0x7ffe5367e044)
printf("%p\n", &myAge);
```

### 指针变量 {.col-span-2}

```c
int myAge = 43; // 一个 int 变量
int*ptr = &myAge; // 名为 ptr 的指针变量，用于存储 myAge 的地址

printf("%d\n", myAge); // 打印 myAge 的值 (43)

printf("%p\n", &myAge); // 输出 myAge 的内存地址 (0x7ffe5367e044)
printf("%p\n", ptr); // 使用指针 (0x7ffe5367e044) 输出 myAge 的内存地址
```

### 解引用

```c
int myAge = 43; // 变量声明
int*ptr = &myAge; // 指针声明

// 引用：使用指针输出 myAge 的
// 内存地址 (0x7ffe5367e044)
printf("%p\n", ptr);
// 解引用：使用指针输出 myAge 的值 (43)
printf("%d\n", *ptr);
```

## 运算符

### 算术运算符

```c
int myNum = 100 + 50;
int sum1 = 100 + 50; // 150 (100 + 50)
int sum2 = sum1 + 250; // 400 (150 + 250)
int sum3 = sum2 + sum2; // 800 (400 + 400)
```

---

| 运算符 | 名称     | 示例    |
| ------ | -------- | ------- |
| `+`    | 加       | `x + y` |
| `-`    | 减       | `x - y` |
| `*`    | 乘       | `x * y` |
| `/`    | 除       | `x / y` |
| `%`    | 取模     | `x % y` |
| `++`   | 自增     | `++x`   |
| `--`   | 自减     | `--x`   |

### 赋值运算符

| 示例                 | 等同于                    |
| -------------------- | ------------------------- |
| x `=` 5              | x `=` 5                   |
| x `+=` 3             | x `=` x `+` 3             |
| x `-=` 3             | x `=` x `-` 3             |
| x `*=` 3             | x `=` x `*` 3             |
| x `/=` 3             | x `=` x `/` 3             |
| x `%=` 3             | x `=` x `%` 3             |
| x `&=` 3             | x `=` x `&` 3             |
| x <code>\|=</code> 3 | x `=` x <code>\|</code> 3 |
| x `^=` 3             | x `=` x `^` 3             |
| x `>>=` 3            | x `=` x `>>` 3            |
| x `<<=` 3            | x `=` x `<<` 3            |

### 比较运算符

```c
int x = 5;
int y = 3;

printf("%d", x > y);
// 返回 1 (true)，因为 5 大于 3
```

---

| 符号 | 名称             | 示例     |
| ---- | ---------------- | -------- |
| `==` | 等于             | x `==` y |
| `!=` | 不等于           | x `!=` y |
| `>`  | 大于             | x `>` y  |
| `<`  | 小于             | x `<` y  |
| `>=` | 大于或等于       | x `>=` y |
| `<=` | 小于或等于       | x `<=` y |

比较运算符用于比较两个值。

### 逻辑运算符 {.col-span-2}

| 符号              | 名称     | 描述                                   | 示例                          |
| ----------------- | -------- | -------------------------------------- | ----------------------------- |
| `&&`              | 逻辑与   | 如果两个语句都为真，则返回真           | `x < 5 && x < 10`             |
| <code>\|\|</code> | 逻辑或   | 如果其中一个语句为真，则返回真         | <code>x < 5 \|\| x < 4</code> |
| `!`               | 逻辑非   | 反转结果，如果为真则返回假             | `!(x < 5 && x < 10)`          |

{.show-header}

### 运算符示例 {.row-span-2}

```c
unsigned int a = 60; /*60 = 0011 1100 */
unsigned int b = 13; /*13 = 0000 1101 */
int c = 0;

c = a & b; /*12 = 0000 1100 */
printf("第 1 行 - c 的值是 %d\n", c);

c = a | b; /*61 = 0011 1101 */
printf("第 2 行 - c 的值是 %d\n", c);
c = a ^ b; /*49 = 0011 0001 */
printf("第 3 行 - c 的值是 %d\n", c);
c = ~a; /*-61 = 1100 0011 */
printf("第 4 行 - c 的值是 %d\n", c);
c = a << 2; /*240 = 1111 0000 */
printf("第 5 行 - c 的值是 %d\n", c);
c = a >> 2; /*15 = 0000 1111 */
printf("第 6 行 - c 的值是 %d\n", c);
```

### 位运算符 {.col-span-2}

| 运算符        | 描述                                                     | 实例                                              |
| :-------------- | :------------------------------------------------------- | :---------------------------------------------------- |
| `&`             | 按位与操作，按二进制位进行“与”操作                       | `(A & B)` 将得到 `12`，即 0000 1100            |
| <code>\|</code> | 按位或运算符，按二进制位进行“或”操作                     | <code>(A \| B)</code> 将得到 `61`，即 0011 1101 |
| `^`             | 异或运算符，按二进制位进行“异或”操作                     | `(A ^ B)` 将得到 `49`，即 0011 0001            |
| `~`             | 取反运算符，按二进制位进行“取反”操作                     | `(~A)` 将得到 `-61`，即 1100 0011              |
| `<<`            | 二进制左移运算符                                         | `A << 2` 将得到 `240`，即 1111 0000            |
| `>>`            | 二进制右移运算符                                         | `A >> 2` 将得到 `15`，即 0000 1111             |

{.show-header}

## 数据类型

### 基本数据类型 {.col-span-2}

| 数据类型             | 大小             | 范围                               | 描述                         |
| -------------------- | ---------------- | ---------------------------------- | :--------------------------- |
| `char`               | 1 字节           | `−128` ~ `127`                     | 单个字符/字母数字/ASCII      |
| `signed char`        | 1 字节           | `−128` ~ `127`                     |                              |
| `unsigned char`      | 1 字节           | `0` ~ `255`                        |                              |
| `int`                | `2` 到 `4` 字节  | `−32,768` ~ `32,767`               | 存储整数                     |
| `signed int`         | 2 字节           | `−32,768` ~ `32,767`               |                              |
| `unsigned int`       | 2 字节           | `0` ~ `65,535`                     |                              |
| `short int`          | 2 字节           | `−32,768` ~ `32,767`               |                              |
| `signed short int`   | 2 字节           | `−32,768` ~ `32,767`               |                              |
| `unsigned short int` | 2 字节           | `0` ~ `65,535`                     |                              |
| `long int`           | 4 字节           | `-2,147,483,648` ~ `2,147,483,647` |                              |
| `signed long int`    | 4 字节           | `-2,147,483,648` ~ `2,147,483,647` |                              |
| `unsigned long int`  | 4 字节           | `0` ~ `4,294,967,295`              |                              |
| `float`              | 4 字节           | `3.4E-38` ~ `3.4E+38`              |                              |
| `double`             | 8 字节           | `1.7E-308` ~ `1.7E+308`            |                              |
| `long double`        | 10 字节          | `3.4E-4932` ~ `1.1E+4932`          |                              |

{.show-header}

### 数据类型

```c
// 创建变量
int myNum = 5; // 整数
float myFloatNum = 5.99; // 浮点数
char myLetter = 'D'; // 字符
// 高精度浮点数据或数字
double myDouble = 3.2325467;
// 打印输出变量
printf("%d\n", myNum);
printf("%f\n", myFloatNum);
printf("%c\n", myLetter);
printf("%lf\n", myDouble);
```

---

| 数据类型 | 描述                         |
| :------- | :--------------------------- |
| `char`   | 字符类型                     |
| `short`  | 短整型                       |
| `int`    | 整型                         |
| `long`   | 长整型                       |
| `float`  | 单精度浮点类型               |
| `double` | 双精度浮点类型               |
| `void`   | 无类型                       |

### 基本格式说明符

| 格式说明符 | 数据类型                                             |
| ---------- | :--------------------------------------------------- |
| `%d` 或 `%i` | `int` 整数                                         |
| `%f`       | `float` 单精度十进制类型                             |
| `%lf`      | `double` 高精度浮点数据或数字                        |
| `%c`       | `char` 字符                                        |
| `%s`       | 用于 `strings` 字符串                                |

{.show-header}

### 单独的进制格式说明符

| 格式      | 短整型        | 整型        | 长整型        |
| --------- | ------------- | ----------- | :------------ |
| 八进制    | `%ho`         | `%o`        | `%lo`         |
| 十进制    | `%hd`         | `%d`        | `%ld`         |
| 十六进制  | `%hx` / `%hX` | `%x` / `%X` | `%lx` / `%lX` |

{.show-header}

### 数据格式示例

```c
int myNum = 5;
float myFloatNum = 5.99; // 浮点数
char myLetter = 'D';     // 字符
// 打印输出变量
printf("%d\n", myNum);
printf("%f\n", myFloatNum);
printf("%c\n", myLetter);
```

## C 预处理器

### 预处理指令 {.row-span-2}

| 指令       | 描述                                                         |
| ---------- | :----------------------------------------------------------- |
| `#define`  | 定义一个宏                                                   |
| `#include` | 包含一个源代码文件                                           |
| `#undef`   | 取消定义宏                                                   |
| `#ifdef`   | 如果宏已定义，则返回真                                       |
| `#ifndef`  | 如果宏未定义，则返回真                                       |
| `#if`      | 如果给定条件为真，则编译以下代码                             |
| `#else`    | `#if` 的替代方案                                             |
| `#elif`    | 如果 `#if` 条件为假，且当前条件为 `真`                       |
| `#endif`   | 结束一个 `#if...#else` 条件编译块                            |
| `#error`   | 当遇到标准错误时打印错误消息                                 |
| `#pragma`  | 使用标准化方法向编译器发出特殊命令                           |

{.show-header}

```c
// 将所有 MAX_ARRAY_LENGTH 替换为 20
#define MAX_ARRAY_LENGTH 20
// 从系统库获取 stdio.h
#include <stdio.h>
// 从本地目录获取 myheader.h
#include "myheader.h"
#undef FILE_SIZE
#define FILE_SIZE 42 // 取消定义并定义为 42
```

### 预定义宏 {.row-span-2}

| 宏         | 描述                                                           |
| ---------- | :------------------------------------------------------------- |
| `__DATE__` | 当前日期，格式为 "MMM DD YYYY" 的字符常量                      |
| `__TIME__` | 当前时间，格式为 "HH:MM:SS" 的字符常量                         |
| `__FILE__` | 这将包含当前文件名，一个字符串常量                             |
| `__LINE__` | 这将包含当前行号，一个十进制常量                               |
| `__STDC__` | 当编译器针对 `ANSI` 标准进行编译时定义为 `1`                   |

{.show-header}

`ANSI C` 定义了许多您可以使用的宏，但您不能直接修改这些预定义的宏。

#### 预定义宏示例

```c
#include <stdio.h>

int main(void) {
  printf("文件: %s\n", __FILE__);
  printf("日期: %s\n", __DATE__);
  printf("时间: %s\n", __TIME__);
  printf("行号: %d\n", __LINE__);
  printf("ANSI: %d\n", __STDC__);
}
```

### 宏续行运算符 (\\)

宏通常写在一行上。

```c
#define message_for(a, b) \
    printf(#a " and " #b ": We love you!\n")
```

如果宏太长而无法放在一行上，请使用宏续行运算符 `\`。

### 字符串常量化运算符 (#)

```c
#include <stdio.h>

#define message_for(a, b) \
  printf(#a " and " #b ": We love you!\n")

int main(void) {
  message_for(Carole, Debra);

  return 0;
}
```

当上述代码编译并执行时，会产生以下结果：

```
Carole and Debra: We love you!
```

当您需要将宏参数转换为字符串常量时，请使用字符串常量化运算符 `#`。

### 标记粘贴运算符 (##)

```c
#include <stdio.h>

#define tokenpaster(n) printf ("Token " #n " = %d\n", token##n)

int main(void) {
  int token34 = 40;
  tokenpaster(34);

  return 0;
}
```

### defined() 运算符

```c
#include <stdio.h>

#if !defined (MESSAGE)
   #define MESSAGE "You wish!"
#endif

int main(void) {
  printf("Here is the message: %s\n", MESSAGE);

  return 0;
}
```

### 参数化宏

```c
int square(int x) {
  return x * x;
}
```

宏将上述代码重写如下：

```c
#define square(x) ( (x) * (x) )
```

宏名称和左括号之间不允许有空格。

```c
#include <stdio.h>
#define MAX(x,y) ( (x) > (y) ? (x) : (y) )

int main(void) {
  printf("20 和 10 之间的最大值是 %d\n", MAX(10, 20));

  return 0;
}
```

## C 函数

### 函数声明和定义 {.row-span-2}

```c
int main(void) {
  printf("Hello World!\n");

  return 0;
}
```

函数由两部分组成

```c
void myFunction() { // 声明
  // 函数体 (要执行的代码) (定义)
}
```

---

- `声明` 声明函数名称、返回类型和参数 _(如果有)_
- `定义` 函数体 _(要执行的代码)_

---

```c
// 函数声明
void myFunction();
// main 方法
int main() {
  myFunction(); // --> 调用函数

  return 0;
}

void myFunction() {// 函数定义
  printf("Good evening!\n");
}
```

### 调用函数

```c
// 创建函数
void myFunction() {
  printf("Good evening!\n");
}

int main() {
  myFunction(); // 调用函数
  myFunction(); // 可以多次调用

  return 0;
}
// 输出 -> "Good evening!"
// 输出 -> "Good evening!"
```

### 函数参数

```c
void myFunction(char name[]) {
  printf("你好 %s\n", name);
}

int main() {
  myFunction("Liam");
  myFunction("Jenny");

  return 0;
}
// 你好 Liam
// 你好 Jenny
```

### 多个参数

```c
void myFunction(char name[], int age) {
  printf("你好 %s, 你 %d 岁了。\n",name,age);
}
int main() {
  myFunction("Liam", 3);
  myFunction("Jenny", 14);

  return 0;
}
// 你好 Liam, 你 3 岁了。
// 你好 Jenny, 你 14 岁了。
```

### 返回值 {.row-span-2}

```c
int myFunction(int x) {
  return 5 + x;
}

int main() {
  printf("结果: %d\n", myFunction(3));
  return 0;
}
// 输出 8 (5 + 3)
```

两个参数

```c
int myFunction(int x, int y) {
  return x + y;
}

int main() {
  printf("结果: %d\n", myFunction(5, 3));
  // 将结果存储在变量中
  int result = myFunction(5, 3);
  printf("结果 = %d\n", result);

  return 0;
}
// 结果: 8 (5 + 3)
// 结果 = 8 (5 + 3)
```

### 递归示例

```c
int sum(int k);

int main() {
  int result = sum(10);
  printf("%d\n", result);

  return 0;
}

int sum(int k) {
  if (k > 0) {
    return k + sum(k -1);
  } else {
    return 0;
  }
}
```

### 数学函数

```c
#include <math.h>

void main(void) {
  printf("%f\n", sqrt(16)); // 平方根
  printf("%f\n", ceil(1.4)); // 向上取整 (四舍五入)
  printf("%f\n", floor(1.4)); // 向下取整 (四舍五入)
  printf("%f\n", pow(4, 3)); // x(4) 的 y(3) 次方
}
```

---

- `abs(x)` 绝对值
- `acos(x)` 反余弦值
- `asin(x)` 反正弦
- `atan(x)` 反正切
- `cbrt(x)` 立方根
- `cos(x)` 余弦
- `exp(x)` 的值 Ex
- `sin(x)` x 的正弦
- `tan(x)` 角的正切

## C 结构体

### 创建结构体

```c
struct MyStructure { // 结构体声明
  int myNum; // 成员 (int 变量)
  char myLetter; // 成员 (char 变量)
}; // 以分号结束结构体
```

创建一个名为 `s1` 的结构体变量

```c{7}
struct myStructure {
  int myNum;
  char myLetter;
};

int main() {
  struct myStructure s1;

  return 0;
}
```

### 结构体中的字符串

```c{9}
struct myStructure {
  int myNum;
  char myLetter;
  char myString[30]; // 字符串
};

int main() {
  struct myStructure s1;
  strcpy(s1. myString, "Some text");
  // 打印值
  printf("我的字符串: %s\n", s1.myString);

  return 0;
}
```

使用 `strcpy` 函数为字符串赋值。

### 访问结构体成员 {.row-span-2}

```c{11,12,16}
// 创建一个名为 myStructure 的结构体
struct myStructure {
  int myNum;
  char myLetter;
};

int main() {
  // 创建一个名为 s1 的 myStructure 结构体变量
  struct myStructure s1;
  // 为 s1 的成员赋值
  s1.myNum = 13;
  s1.myLetter = 'B';

  // 创建一个名为 s2 的 myStructure 结构体变量
  // 并为其赋值
  struct myStructure s2 = {13, 'B'};
  // 打印值
  printf("我的数字: %d\n", s1.myNum);
  printf("我的字母: %c\n", s1.myLetter);

  return 0;
}
```

创建不同的结构体变量

```c
struct myStructure s1;
struct myStructure s2;
// 为不同的结构体变量赋值
s1.myNum = 13;
s1.myLetter = 'B';

s2.myNum = 20;
s2.myLetter = 'C';
```

### 复制结构体

```c{6}
struct myStructure s1 = {
  13, 'B', "Some text"
};

struct myStructure s2;
s2 = s1;
```

在示例中，`s1` 的值被复制到 `s2`。

### 修改值

```c{6,7}
// 创建一个结构体变量并为其赋值
struct myStructure s1 = {
  13, 'B'
};
// 修改值
s1.myNum = 30;
s1.myLetter = 'C';
// 打印值
printf("%d %c",
    s1.myNum,
    s1.myLetter);
```

## 文件处理

### 文件处理函数

| 函数        | 描述                                       |
| ----------- | :----------------------------------------- |
| `fopen()`   | `打开` 一个新的或已存在的文件              |
| `fprintf()` | 将数据写入 `文件`                          |
| `fscanf()`  | 从文件中 `读取` 数据                       |
| `fputc()`   | 将一个字符写入 `文件`                      |
| `fgetc()`   | 从文件中 `读取` 一个字符                   |
| `fclose()`  | `关闭` 文件                                |
| `fseek()`   | 将文件指针设置到 `给定的位置`              |
| `fputw()`   | 将一个整数 `写入` 文件                     |
| `fgetw()`   | 从文件中 `读取` 一个整数                   |
| `ftell()`   | 返回当前 `位置`                            |
| `rewind()`  | 将文件指针设置到文件的开头                 |

{.show-header}

C 库中有许多函数用于 `打开`/`读取`/`写入`/`搜索` 和 `关闭` 文件。

### 打开模式参数

| 模式  | 描述                                                                                                 |
| ----- | :--------------------------------------------------------------------------------------------------- |
| `r`   | 以 `只读` 模式打开文本文件，允许读取文件                                                               |
| `w`   | 以 `写入` 模式打开文本文件，允许写入文件                                                               |
| `a`   | 以 `追加` 模式打开文本文件<br /><small>如果文件不存在，将创建一个新文件</small>                       |
| `r+`  | 以 `读写` 模式打开文本文件，允许读取和写入文件                                                         |
| `w+`  | 以 `读写` 模式打开文本文件，允许读取和写入文件                                                         |
| `a+`  | 以 `读写` 模式打开文本文件，允许读取和写入文件                                                         |
| `rb`  | 以 `只读` 模式打开二进制文件                                                                           |
| `wb`  | 以 `写入` 模式打开二进制文件                                                                           |
| `ab`  | 以 `追加` 模式打开二进制文件                                                                           |
| `rb+` | 以 `读写` 模式打开二进制文件                                                                           |
| `wb+` | 以 `读写` 模式打开二进制文件                                                                           |
| `ab+` | 以 `读写` 模式打开二进制文件                                                                           |

{.show-header}

### 打开文件：fopen()

```c{6}
#include <stdio.h>

void main() {
  FILE *fp;
  char ch;

  fp = fopen("file_handle.c", "r");

  while (1) {
    ch = fgetc(fp);
    if (ch == EOF)
      break;
    printf("%c", ch);
  }
  fclose(fp);
}
```

在对文件执行所有操作后，必须使用 `fclose()` 关闭文件。

### 写入文件：fprintf()

```c{7}
#include <stdio.h>

void main() {
  FILE *fp;
  fp = fopen("file.txt", "w"); // 打开文件

  // 将数据写入文件
  fprintf(fp, "Hello file for fprintf..\n");
  fclose(fp); // 关闭文件
}
```

### 读取文件：fscanf()

```c{6}
#include <stdio.h>

void main() {
  FILE *fp;

  char buff[255]; // 创建一个字符数组来存储文件数据
  fp = fopen("file.txt", "r");

  while(fscanf(fp, "%s", buff) != EOF) {
    printf("%s ", buff);
  }
  fclose(fp);
}
```

### 写入文件：fputc()

```c{6}
#include <stdio.h>

void main() {
  FILE *fp;
  fp = fopen("file1.txt", "w"); // 打开文件
  fputc('a',fp); // 将单个字符写入文件
  fclose(fp); // 关闭文件
}
```

### 读取文件：fgetc()

```c{8}
#include <stdio.h>
#include <conio.h>

void main() {
  FILE *fp;
  char c;

  clrscr();

  fp = fopen("myfile.txt", "r");

  while( (c = fgetc(fp) ) != EOF) {
    printf("%c", c);
  }
  fclose(fp);

  getch();
}
```

### 写入文件：fputs()

```c {8}
#include<stdio.h>
#include<conio.h>

void main() {
  FILE *fp;

  clrscr();

  fp = fopen("myfile2.txt","w");
  fputs("hello c programming",fp);
  fclose(fp);

  getch();
}
```

### 读取文件：fgets()

```c {10}
#include<stdio.h>
#include<conio.h>

void main() {
  FILE *fp;
  char text[300];

  clrscr();

  fp = fopen("myfile2.txt", "r");
  printf("%s", fgets(text, 200, fp));
  fclose(fp);

  getch();
}
```

### fseek()

```c{8}
#include <stdio.h>

void main(void) {
  FILE *fp;

  fp = fopen("myfile.txt","w+");
  fputs("This is Book", fp);

  // 将文件指针设置到给定位置
  fseek(fp, 7, SEEK_SET);

  fputs("Kenny Wong", fp);
  fclose(fp);
}
```

将文件指针设置到给定位置。

### rewind()

```c{11}
#include <stdio.h>
#include <conio.h>

void main() {
  FILE *fp;
  char c;

  clrscr();

  fp = fopen("file.txt", "r");

  while( (c = fgetc(fp) ) != EOF) {
    printf("%c", c);
  }

  rewind(fp); // 将文件指针移动到文件的开头

  while( (c = fgetc(fp) ) != EOF) {
    printf("%c", c);
  }
  fclose(fp);

  getch();
}
// 输出
// Hello World! Hello World!
```

### ftell()

```c{11}
#include <stdio.h>
#include <conio.h>

void main () {
   FILE *fp;
   int length;

   clrscr();

   fp = fopen("file.txt", "r");

   fseek(fp, 0, SEEK_END);
   length = ftell(fp); // 返回当前位置
   fclose(fp);

   printf("文件大小: %d 字节", length);

   getch();
}
// 输出
// 文件大小: 18 字节
```
