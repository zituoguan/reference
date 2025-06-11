---
title: Rust 语言
date: 2022-01-01 11:51:44
background: bg-black
tags:
categories:
  - 编程
intro: |
  Rust 快速参考备忘单，旨在帮助编写基本语法和方法。
plugins:
  - copyCode
---

## 入门指南

### Hello_World.rs

```rust
fn main() {
    println!("Hello, World!");
}
```

#### 编译和运行

```shell
$ rustc Hello_World.rs
$ ./Hello_World
Hello, World!
```

### 基本类型

|                           |                                 |
| ------------------------- | :------------------------------ |
| `bool`                    | 布尔值 (`true` _/_ `false`)    |
| `char`                    | 字符                       |
| `f32`, `f64`              | 32位, 64位浮点数         |
| `i64`, `i32`, `i16`, `i8` | 有符号 16位 ... 整数         |
| `u64`, `u32`, `u16`, `u8` | 无符号 16位 ... 整数  |
| `isize`                   | 指针大小的有符号整数   |
| `usize`                   | 指针大小的无符号整数 |

参见: [Rust 类型](#rust-types)

### 格式化输出 {.row-span-2}

```rust {.wrap}
// 单个占位符
println!("{}", 1);

// 多个占位符
println!("{} {}", 1, 3);

// 位置参数
println!(
    "{0} is {1} {2}, also {0} is a {3} programming language",
    "Rust", "cool", "language", "safe"
);

// 命名参数
println!(
    "{country} is a diverse nation with unity.",
    country = "India"
);

// 占位符特性 :b 代表二进制, :0x 代表十六进制, :o 代表八进制
println!("Let us print 76 is binary which is {:b} , and hex equivalent is {:0x} and octal equivalent is {:o}", 76, 76, 76);

// Debug 特性
println!(
    "Print whatever we want to here using debug trait {:?}",
    (76, 'A', 90)
);

// 1.58 版本中的新格式化字符串
let x = "world";
println!("Hello {x}!");
```

### 打印样式

```rust
// 打印输出
print!("Hello World\n");

// 打印后追加新行
println!("Appending a new line");

// 作为错误打印
eprint!("This is an error\n");

// 作为错误打印并换行
eprintln!("This is an error with new line");
```

### 变量

```rust
// 初始化并声明变量
let some_variable = "This_is_a_variable";

// 使变量可变
let mut mutable_variable = "Mutable";

// 赋多个值给变量
let (name, age) = ("ElementalX", 20);

// (全局) 常量
const SCREAMING_SNAKE_CASE: i64 = 9;
```

### 注释

```rust
// 行注释
/*.............块注释 */
/// 外部文档注释
//! 内部文档注释
```

参见: [注释](https://doc.rust-lang.org/reference/comments.html)

### 函数

```rust
fn test() {
    println!("This is a function!"); // 这是一个函数！
}

fn main() {
    test();
}
```

参见: [Rust 函数](#rust-functions)

## Rust 类型

### 整数

```rust
let mut a: u32 = 8;
let b: u64 = 877;
let c: i64 = 8999;
let d = -90;
```

### 浮点数

```rust
let mut sixty_bit_float: f64 = 89.90;
let thirty_two_bit_float: f32 = 7.90;
let just_a_float = 69.69;
```

### 布尔型

```rust {.wrap}
let true_val: bool = true;
let false_val: bool = false;
let just_a_bool = true;
let is_true = 8 < 5; // => false
```

### 字符

```rust
let first_letter_of_alphabet = 'a';
let explicit_char: char = 'F';
let implicit_char = '8';
let emoji = "\u{1f600}"; // => 😀
```

### 字符串字面量

```rust {.wrap}
let community_name = "AXIAL";
let no_of_members: &str = "ten";

// 社区名称是 AXIAL，它有 ten 个成员
println!("The name of the community is {community_name} and it has {no_of_members} members");
```

参见: [字符串](#rust-strings)

### 数组

```rust
┌─────┬─────┬─────┬─────┬─────┬─────┐
| 92  | 97  | 98  | 99  | 98  | 94  |
└─────┴─────┴─────┴─────┴─────┴─────┘
   0     1     2     3     4     5
```

---

```rust
let array: [i64; 6] = [92, 97, 98, 99, 98, 94];
```

### 多维数组 {.row-span-2}

```rust
     j0   j1   j2   j3   j4   j5
   ┌────┬────┬────┬────┬────┬────┐
i0 | 1  | 2  | 3  | 4  | 5  | 6  |
   ├────┼────┼────┼────┼────┼────┤
i1 | 6  | 5  | 4  | 3  | 2  | 1  |
   └────┴────┴────┴────┴────┴────┘
```

---

```rust
let array: [[i64; 6]; 2] = [
    [1, 2, 3, 4, 5, 6],
    [6, 5, 4, 3, 2, 1]
];
```

### 可变数组

```rust
let mut array: [i32; 3] = [2, 6, 10];

array[1] = 4;
array[2] = 6;
```

使用 `mut` 关键字使其可变。

### 切片

```rust
let mut array: [i64; 4] = [1, 2, 3, 4];
// 低位边界包含在内，高位边界不包含在内
let mut slices: &[i64] = &array[0..3];

// 切片的元素是 : [1, 2, 3]
println!("The elements of the slices are : {slices:?}");
```

### Vector (动态数组)

```rust
let some_vector = vec![1, 2, 3, 4, 5];
```

Vector 使用 `vec!` 宏声明。

### 元组

```rust
let tuple = (1, 'A', "Cool", 78, true);
```

## Rust 字符串

### 字符串字面量

```rust
let cs: &str = "cheat sheet";

// => 为开发者分享 cheat sheet
println!("Share {cs} for developers");
```

### String 对象

```rust
// 创建一个空的 String 对象
let my_string = String::new();

// 转换为 String 对象 (假设 a_string 是一个 &str)
// let S_string = a_string.to_string();

// 创建一个初始化的 String 对象
let lang = String::from("Rust");
// 第一门语言是 Rust
println!("First language is {lang}");
```

### .capacity()

```rust
let rand = String::from("Random String");
rand.capacity() // => 13
```

计算字符串的容量（字节数）。

### .contains()

```rust
let name = String::from("ElementalX");
name.contains("Element") // => true
```

检查子字符串是否包含在原始字符串中。

### 推入单个字符

```rust
let mut half_text = String::from("Hal");
half_text.push('f'); // => Half
```

### 推入整个字符串

```rust
let mut hi = String::from("Hey there...");
hi.push_str("How are you doing??");

// => Hey there...How are you doing??
println!("{hi}");
```

## Rust 运算符

### 比较运算符

|          |                                  |
| -------- | :------------------------------- |
| `e == f` | `e` 等于 `f`              |
| `e != f` | `e` 不等于 `f`          |
| `e < f`  | `e` 小于 `f`             |
| `e > f`  | `e` 大于 `f`               |
| `e <= f` | `e` 小于或等于 `f` |
| `e >= f` | `e` 大于或等于 `f`   |

---

```rust
let (e, f) = (1, 100);

let greater = f > e;        // => true
let less = f < e;           // => false
let greater_equal = f >= e; // => true
let less_equal = e <= f;    // => true
let equal_to = e == f;      // => false
let not_equal_to = e != f;  // => true
```

### 算术运算符

|          |                                            |
| -------- | :----------------------------------------- |
| `a +  b` | `a` 加上 `b`                        |
| `a -  b` | `a` 减去 `b`                 |
| `a /  b` | `a` 除以 `b`                      |
| `a % b`  | `a` 除以 `b` 的余数 |
| `a * b`  | `a` 乘以 `b`                 |

---

```rust {.wrap}
let (a, b) = (4, 5);

let sum: i32 = a + b;            // => 9
let subtractions: i32 = a - b;   // => -1
let multiplication: i32 = a * b; // => 20
let division: i32 = a / b;       // => 0
let modulus: i32 = a % b;        // => 4
```

### 位运算符

| Operator            | Description             |
| ------------------- | ----------------------- |
| `g & h`             | 按位与              |
| `g \| h`            | 按位或               |
| `g ^ h`             | 按位异或              |
| `!g`                | 按位取反 (一的补码) |
| `g << h`            | 按位左移       |
| `g >> h`            | 按位右移      |

---

```rust {.wrap}
let (g, h) = (0x1, 0x2);

let bitwise_and = g & h;  // => 0
let bitwise_or = g | h;   // => 3
let bitwise_xor = g ^ h;  // => 3
let right_shift = g >> 2; // => 0
let left_shift = h << 4;  // => 32
```

### 逻辑运算符

| Example               | Meaning               |
| --------------------- | --------------------- |
| `c && d`              | 两者都为真 _(与)_ |
| `c \|\| d`            | 任一为真 _(或)_ |
| `!c`                  | `c` 为假 _(非)_  |

---

```rust
let (c, d) = (true, false);

let and = c && d;  // => false
let or = c || d;   // => true
let not = !c;      // => false
```

### 复合赋值运算符

```rust
let mut k = 9;
let mut l = k;
```

---

| Operator             | Description                             |
| -------------------- | --------------------------------------- |
| `k += l`             | 加一个值并赋值，然后 k=9        |
| `k -= l`             | 减去一个值并赋值，然后 k=18 |
| `k /= l`             | 除以一个值并赋值，然后 k=9     |
| `k *= l`             | 乘以一个值并赋值，然后 k=81  |
| `k \|= l`            | 按位或并赋值，然后 k=89        |

## Rust 流程控制

### If 表达式

```rust
let case1: i32 = 81;
let case2: i32 = 82;

if case1 < case2 {
  println!("case1 大于 case2"); // 注意：原文消息与条件逻辑不符，此处按原文消息翻译
}
```

### If...Else 表达式

```rust
let case3 = 8;
let case4 = 9;

if case3 >= case4 {
    println!("case3 优于 case4");
} else {
    println!("case4 大于 case3");
}
```

### If...Else...if...Else 表达式

```rust
let foo = 12;
let bar = 13;

if foo == bar {
    println!("foo 等于 bar");
} else if foo < bar {
    println!("foo 小于 bar");
} else if foo != bar {
    println!("foo 不等于 bar");
} else {
    println!("无");
}
```

### If...Let 表达式 {.row-span-3}

```rust
let mut arr1: [i64; 3] = [1, 2, 3];
if let [1, 2, _] = arr1 {
    println!("适用于数组");
}

let mut arr2: [&str; 2] = ["one", "two"];
if let ["Apple", _] = arr2 {
    println!("也适用于字符串数组");
}
```

---

```rust
let tuple_1 = ("India", 7, 90, 90.432);
if let (_, 7, 9, 78.99) = tuple_1 {
    println!("也适用于元组");
}

let tuple_2 = (9, 7, 89, 12, "Okay");
if let (9, 7, 89, 12, blank) = tuple_2 {
    println!("一切都 {blank} 吗？");
}

let tuple_3 = (89, 90, "Yes");
if let (9, 89, "Yes") = tuple_3 {
    println!("模式匹配成功");
} else {
    println!("模式不匹配");
}
```

### Match 表达式 {.row-span-3}

```rust
let day_of_week = 2;
match day_of_week {
    1 => {
        println!("今天是星期一");
    }
    2 => {
        println!("今天是星期二");
    }
    3 => {
        println!("今天是星期三");
    }
    4 => {
        println!("今天是星期四");
    }
    5 => {
        println!("今天是星期五");
    }
    6 => {
        println!("今天是星期六");
    }
    7 => {
        println!("今天是星期日");
    }
    _ => {
        println!("默认！")
    }
};
```

### 嵌套 If 表达式

```rust
let nested_conditions = 89;
if nested_conditions == 89 {
    let just_a_value = 98;
    if just_a_value >= 97 {
        println!("大于 97");
    }
}
```

### For 循环

```rust
for mut i in 0..15 {
    i -= 1;
    println!("i 的值是 : {i}");
}
```

### While 循环

```rust
let mut check = 0;
while check < 11 {
    println!("Check 是 : {check}");
    check += 1;
    println!("递增后: {check}");

    if check == 10 {
        break; // 停止 while 循环
    }
}
```

### Loop 关键字

```rust
loop {
    println!("永远的 hello world！");
}
```

表示无限循环。

### Break 语句

```rust
let mut i = 1;
loop {
    println!("i 是 {i}");
    if i > 100 {
        break;
    }
    i *= 2;
}
```

### Continue 语句

```rust
for (v, c) in (0..10 + 1).enumerate() {
    println!("第 {c} 次循环");
    if v == 9 {
        println!("这里要 continue 吗？");
        continue;
    }
    println! {"v 的值是 : {v}"};
}
```

## Rust 函数

### 基本函数

```rust
fn print_message() {
    println!("你好，r3f.cn！");
}

fn main() {
    // 在 Rust 中调用函数。
    print_message();
}
```

### 按值传递

```rust
fn main() {
    let x: u32 = 10;
    let y: u32 = 20;

    // => 200
    println!("计算结果: {}", cal_rect(x, y));
}

fn cal_rect(x: u32, y: u32) -> u32 {
    x * y
}
```

### 按引用传递

```rust
fn main() {
    let mut by_ref = 3; // => 3
    power_of_three(&mut by_ref);
    println!("{by_ref}"); // => 9
}

fn power_of_three(by_ref: &mut i32) {
    // 解引用很重要
    *by_ref = *by_ref * *by_ref;
    println!("{by_ref}"); // => 9
}
```

### 返回值

```rust {.wrap}
fn main() {
    let (mut radius, mut pi) = (3.0, 3.14);
    let (area, _perimeter) = calculate(
        &mut radius,
        &mut pi
    );
    println!("圆的面积和周长是: {area} & {_perimeter}");
}

fn calculate(radius: &mut f64, pi: &mut f64) -> (f64, f64) {
    let perimeter = 2.0 * *pi * *radius;
    let area = *pi * *radius * *radius;
    return (area, perimeter);
}
```

### 数组作为参数

```rust
fn main() {
    let mut array: [i32; 5] = [1, 2, 3, 4, 6];
    print_arrays(array);
    println!("元素: {array:?}");
}

fn print_arrays(mut array: [i32; 5]) {
    array[0] = 89;
    array[1] = 90;
    array[2] = 91;
    array[3] = 92;
    array[4] = 93;
    println!("元素: {array:?}");
}
```

### 返回数组

```rust
fn main() {
    let mut arr: [i32; 5] = [2, 4, 6, 8, 10];
    multiply(arr);
    println!("数组是 : {:?}", multiply(arr));
}

fn multiply(mut arr: [i32; 5]) -> [i32; 5] {
    arr[2] = 90;
    for mut i in 0..5 {
        arr[i] = arr[i] * arr[2];
    }
    return arr;
}
```

## 其他

### 类型转换

```rust
let a_int = 90; // 整数
// 整数转浮点数
let mut type_cast = (a_int as f64);
```

---

```rust
let original: char = 'I';
// 字符转整数 => 73
let type_casted: i64 = original as i64;
```

在 Rust 中执行类型转换必须使用 `as` 关键字。

### 借用

```rust
let mut foo = 4;
let mut borrowed_foo = &foo;
println!("{borrowed_foo}");
```

---

```rust
let mut bar = 3;
let mut mutable_borrowed_bar = &mut bar;
println!("{mutable_borrowed_bar}");
```

这里，借用值使用 `&` 运算符从原值借用。

### 解引用

```rust
let mut borrow = 10;
let deref = &mut borrow;

println!("{}", *deref);
```

在 Rust 中可以使用 `*` 运算符进行解引用。

### 变量作用域

```rust
{
    // 作用域限定在此花括号内
    let a_number = 1;
}
// println!("{a_number}"); // 此行会报错，因为 a_number 超出作用域
```

这会产生错误，因为变量 `a_number` 的作用域在花括号处结束。

## 另请参阅

- [Rust 文档](https://doc.rust-lang.org/book/ch00-00-introduction.html) _(doc.rust-lang.org)_
- [Rust 参考](https://doc.rust-lang.org/reference/introduction.html) _(doc.rust-lang.org)_
- [Rust 备忘单](https://phaiax.github.io/rust-cheatsheet/) _(phaiax.github.io)_
