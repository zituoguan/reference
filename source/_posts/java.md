---
title: Java
date: 2021-03-10 19:50:01
background: bg-[#d33731]
tags:
  - 面向对象
  - 类
categories:
  - 编程
intro: |
  本速查表是为 Java初学者准备的速成课程，有助于回顾 Java 语言的基本语法。
plugins:
  - tooltip
  - copyCode
---

## 入门

### Hello.java {.row-span-2}

```java
public class Hello {
  // main 方法
  public static void main(String[] args)
  {
    // 输出: Hello, world!
    System.out.println("Hello, world!");
  }
}
```

编译和运行

```bash
$ javac Hello.java
$ java Hello
Hello, world!
```

### 变量

```java
int num = 5;
float floatNum = 5.99f;
char letter = 'D';
boolean bool = true;
String site = "r3f.cn";
```

### 基本数据类型 {.row-span-2}

| 数据类型  | 大小   | 默认值  | 范围                |
| --------- | ------ | ------- | :------------------ |
| `byte`    | 1 字节 | 0       | -128 到 127         |
| `short`   | 2 字节 | 0       | -2^15^ 到 2^15^-1   |
| `int`     | 4 字节 | 0       | -2^31^ 到 2^31^-1   |
| `long`    | 8 字节 | 0       | -2^63^ 到 2^63^-1   |
| `float`   | 4 字节 | 0.0f    | _N/A_               |
| `double`  | 8 字节 | 0.0d    | _N/A_               |
| `char`    | 2 字节 | \\u0000 | 0 到 65535          |
| `boolean` | _N/A_  | false   | true / false        |

{.show-header}

### 字符串

```java
String first = "John";
String last = "Doe";
String name = first + " " + last;
System.out.println(name);
```

参见: [字符串](#java-strings)

### 循环

```java
String word = "CheatSheets";
for (char c: word.toCharArray()) {
  System.out.print(c + "-");
}
// 输出: C-h-e-a-t-S-h-e-e-t-s-
```

参见: [循环](#java-loops)

### 数组

```java
char[] chars = new char[10];
chars[0] = 'a'
chars[1] = 'b'

String[] letters = {"A", "B", "C"};
int[] mylist = {100, 200};
boolean[] answers = {true, false};
```

参见: [数组](#java-arrays)

### 交换

```java
int a = 1;
int b = 2;
System.out.println(a + " " + b); // 1 2

int temp = a;
a = b;
b = temp;
System.out.println(a + " " + b); // 2 1
```

### 类型转换

```java
// 拓宽转换
// byte<short<int<long<float<double
int i = 10;
long l = i;               // 10

// 窄化转换
double d = 10.02;
long l = (long)d;         // 10

String.valueOf(10);       // "10"
Integer.parseInt("10");   // 10
Double.parseDouble("10"); // 10.0
```

### 条件语句

```java
int j = 10;

if (j == 10) {
  System.out.println("我会打印");
} else if (j > 10) {
  System.out.println("我不会");
} else {
  System.out.println("我也不会");
}
```

参见: [条件语句](#java-conditionals)

### 用户输入

```java
Scanner in = new Scanner(System.in);
String str = in.nextLine();
System.out.println(str);

int num = in.nextInt();
System.out.println(num);
```

## Java 字符串

### 基本操作

```java
String str1 = "value";
String str2 = new String("value");
String str3 = String.valueOf(123);
```

### 连接

```java
String s = 3 + "str" + 3;     // 3str3
String s = 3 + 3 + "str";     // 6str
String s = "3" + 3 + "str";   // 33str
String s = "3" + "3" + "23";  // 3323
String s = "" + 3 + 3 + "23"; // 3323
String s = 3 + 3 + 23;        // 类型不兼容
```

### StringBuilder {.row-span-3}

`StringBuilder sb = new StringBuilder(10);`

```java
┌───┬───┬───┬───┬───┬───┬───┬───┬───┐
|   |   |   |   |   |   |   |   |   |
└───┴───┴───┴───┴───┴───┴───┴───┴───┘
0   1   2   3   4   5   6   7   8   9
```

`sb.append("QuickRef");`

```java
┌───┬───┬───┬───┬───┬───┬───┬───┬───┐
| Q | u | i | c | k | R | e | f |   |
└───┴───┴───┴───┴───┴───┴───┴───┴───┘
0   1   2   3   4   5   6   7   8   9
```

`sb.delete(5, 9);`

```java
┌───┬───┬───┬───┬───┬───┬───┬───┬───┐
| Q | u | i | c | k |   |   |   |   |
└───┴───┴───┴───┴───┴───┴───┴───┴───┘
0   1   2   3   4   5   6   7   8   9
```

`sb.insert(0, "My ");`

```java
┌───┬───┬───┬───┬───┬───┬───┬───┬───┐
| M | y |   | Q | u | i | c | k |   |
└───┴───┴───┴───┴───┴───┴───┴───┴───┘
0   1   2   3   4   5   6   7   8   9
```

`sb.append("!");`

```java
┌───┬───┬───┬───┬───┬───┬───┬───┬───┐
| M | y |   | Q | u | i | c | k | ! |
└───┴───┴───┴───┴───┴───┴───┴───┴───┘
0   1   2   3   4   5   6   7   8   9
```

### 比较

```java
String s1 = new String("r3f.cn");
String s2 = new String("r3f.cn");

s1 == s2          // false
s1.equals(s2)     // true

"AB".equalsIgnoreCase("ab")  // true
```

### 操作

```java
String str = "Abcd";

str.toUpperCase();     // ABCD
str.toLowerCase();     // abcd
str.concat("#");       // Abcd#
str.replace("b", "-"); // A-cd

"  abc ".trim();       // abc
"ab".toCharArray();    // {'a', 'b'}
```

### 信息

```java
String str = "abcd";

str.charAt(2);       // c
str.indexOf("a")     // 0
str.indexOf("z")     // -1
str.length();        // 4
str.toString();      // abcd
str.substring(2);    // cd
str.substring(2,3);  // c
str.contains("c");   // true
str.endsWith("d");   // true
str.startsWith("a"); // true
str.isEmpty();       // false
```

### 不可变性

```java
String str = "hello";
str.concat("world");

// 输出: hello
System.out.println(str);
```

---

```java
String str = "hello";
String concat = str.concat("world");

// 输出: helloworld
System.out.println(concat);
```

一旦创建就不能修改，任何修改都会创建一个新的字符串

## Java 数组

### 声明

```java
int[] a1;
int[] a2 = {1, 2, 3};
int[] a3 = new int[]{1, 2, 3};

int[] a4 = new int[3];
a4[0] = 1;
a4[2] = 2;
a4[3] = 3;
```

### 修改

```java
int[] a = {1, 2, 3};
System.out.println(a[0]); // 1

a[0] = 9;
System.out.println(a[0]); // 9

System.out.println(a.length); // 3
```

### 循环 (读写)

```java
int[] arr = {1, 2, 3};
for (int i=0; i < arr.length; i++) {
    arr[i] = arr[i] * 2;
    System.out.print(arr[i] + " ");
}
// 输出: 2 4 6
```

### 循环 (只读)

```java
String[] arr = {"a", "b", "c"};
for (String a: arr) {
    System.out.print(a + " ");
}
// 输出: a b c
```

### 多维数组

```java
int[][] matrix = { {1, 2, 3}, {4, 5} };

int x = matrix[1][0];  // 4
// [[1, 2, 3], [4, 5]]
Arrays.deepToString(matrix);

int[][] a = matrix;
for (int i = 0; i < a.length; ++i) {
  for(int j = 0; j < a[i].length; ++j) {
    System.out.println(a[i][j]);
  }
}
// 输出: 1 2 3 4 5 6 7
```

### 排序

```java
char[] chars = {'b', 'a', 'c'};
Arrays.sort(chars);

// [a, b, c]
Arrays.toString(chars);
```

## Java 条件语句

### 运算符 {.row-span-2}

- <a data-tooltip="加法运算符 (也用于字符串连接)">+</a>
- <a data-tooltip="减法运算符">-</a>
- <a data-tooltip="乘法运算符">\*</a>
- <a data-tooltip="除法运算符">/</a>
- <a data-tooltip="取余运算符">%</a>
- <a data-tooltip="简单赋值运算符">=</a>
- <a data-tooltip="自增运算符；将值加 1">++</a>
- <a data-tooltip="自减运算符；将值减 1">--</a>
- <a data-tooltip="逻辑非运算符；反转布尔值">!</a>

{.marker-none .cols-4}

---

- <a data-tooltip="等于">==</a>
- <a data-tooltip="不等于">!=</a>
- <a data-tooltip="大于">></a>
- <a data-tooltip="大于或等于">>=</a>
- <a data-tooltip="小于"><</a>
- <a data-tooltip="小于或等于"><=</a>

{.marker-none .cols-4}

---

- <a data-tooltip="条件与">&&</a>
- <a data-tooltip="条件或">||</a>
- [?:](#ternary-operator){data-tooltip="三元运算符 (if-then-else 语句的简写)"}

{.marker-none .cols-4}

---

- <a data-tooltip="比较对象是否为指定类型">instanceof</a>

{.marker-none}

---

- <a data-tooltip="按位取反">~</a>
- <a data-tooltip="有符号左移"><<</a>
- <a data-tooltip="有符号右移">>></a>
- <a data-tooltip="无符号右移">>>></a>
- <a data-tooltip="按位与">&</a>
- <a data-tooltip="按位异或">^</a>
- <a data-tooltip="按位或">|</a>

{.marker-none .cols-4}

### If else

```java
int k = 15;
if (k > 20) {
  System.out.println(1);
} else if (k > 10) {
  System.out.println(2);
} else {
  System.out.println(3);
}
```

### Switch {.row-span-2}

```java
int month = 3;
String str;
switch (month) {
  case 1:
    str = "一月";
    break;
  case 2:
    str = "二月";
    break;
  case 3:
    str = "三月";
    break;
  default:
    str = "其他月份";
    break;
}

// 输出: 结果 三月
System.out.println("结果 " + str);
```

### 三元运算符

```java
int a = 10;
int b = 20;
int max = (a > b) ? a : b;

// 输出: 20
System.out.println(max);
```

## Java 循环

### For 循环

```java
for (int i = 0; i < 10; i++) {
  System.out.print(i);
}
// 输出: 0123456789
```

---

```java
for (int i = 0,j = 0; i < 3; i++,j--) {
  System.out.print(j + "|" + i + " ");
}
// 输出: 0|0 -1|1 -2|2
```

### 增强型 For 循环

```java
int[] numbers = {1,2,3,4,5};

for (int number: numbers) {
  System.out.print(number);
}
// 输出: 12345
```

用于遍历数组或列表

### While 循环

```java
int count = 0;

while (count < 5) {
  System.out.print(count);
  count++;
}
// 输出: 01234
```

### Do While 循环

```java
int count = 0;

do {
  System.out.print(count);
  count++;
} while (count < 5);
// 输出: 01234
```

### Continue 语句

```java
for (int i = 0; i < 5; i++) {
  if (i == 3) {
    continue;
  }
  System.out.print(i);
}
// 输出: 0124
```

### Break 语句

```java
for (int i = 0; i < 5; i++) {
  System.out.print(i);
  if (i == 3) {
    break;
  }
}
// 输出: 0123
```

## Java 集合框架

### Java 集合 {.col-span-2}

| 集合                                                                                                               | 接口        | 有序 | 排序 | 线程安全 | 重复 | 可空               |
| ------------------------------------------------------------------------------------------------------------------ | ----------- | ---- | ---- | -------- | ---- | ------------------ |
| [ArrayList](https://docs.oracle.com/javase/8/docs/api/java/util/ArrayList.html)                                    | List        | 是   | 否   | 否       | 是   | 是                 |
| [Vector](https://docs.oracle.com/javase/8/docs/api/java/util/Vector.html)                                          | List        | 是   | 否   | 是       | 是   | 是                 |
| [LinkedList](https://docs.oracle.com/javase/8/docs/api/java/util/LinkedList.html)                                  | List, Deque | 是   | 否   | 否       | 是   | 是                 |
| [CopyOnWriteArrayList](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/CopyOnWriteArrayList.html)   | List        | 是   | 否   | 是       | 是   | 是                 |
| [HashSet](https://docs.oracle.com/javase/8/docs/api/java/util/HashSet.html)                                        | Set         | 否   | 否   | 否       | 否   | 一个 `null`        |
| [LinkedHashSet](https://docs.oracle.com/javase/8/docs/api/java/util/LinkedHashSet.html)                            | Set         | 是   | 否   | 否       | 否   | 一个 `null`        |
| [TreeSet](https://docs.oracle.com/javase/8/docs/api/java/util/TreeSet.html)                                        | Set         | 是   | 是   | 否       | 否   | 否                 |
| [CopyOnWriteArraySet](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/CopyOnWriteArraySet.html)     | Set         | 是   | 否   | 是       | 否   | 一个 `null`        |
| [ConcurrentSkipListSet](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ConcurrentSkipListSet.html) | Set         | 是   | 是   | 是       | 否   | 否                 |
| [HashMap](https://docs.oracle.com/javase/8/docs/api/java/util/HashMap.html)                                        | Map         | 否   | 否   | 否       | 否 (键) | 一个 `null` (键)   |
| [HashTable](https://docs.oracle.com/javase/8/docs/api/java/util/Hashtable.html)                                    | Map         | 否   | 否   | 是       | 否 (键) | 否 (键)            |
| [LinkedHashMap](https://docs.oracle.com/javase/8/docs/api/java/util/LinkedHashMap.html)                            | Map         | 是   | 否   | 否       | 否 (键) | 一个 `null` (键)   |
| [TreeMap](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html)                                        | Map         | 是   | 是   | 否       | 否 (键) | 否 (键)            |
| [ConcurrentHashMap](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ConcurrentHashMap.html)         | Map         | 否   | 否   | 是       | 否 (键) | 否                 |
| [ConcurrentSkipListMap](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ConcurrentSkipListMap.html) | Map         | 是   | 是   | 是       | 否 (键) | 否                 |
| [ArrayDeque](https://docs.oracle.com/javase/8/docs/api/java/util/ArrayDeque.html)                                  | Deque       | 是   | 否   | 否       | 是   | 否                 |
| [PriorityQueue](https://docs.oracle.com/javase/8/docs/api/java/util/PriorityQueue.html)                            | Queue       | 是   | 否   | 否       | 是   | 否                 |
| [ConcurrentLinkedQueue](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ConcurrentLinkedQueue.html) | Queue       | 是   | 否   | 是       | 是   | 否                 |
| [ConcurrentLinkedDeque](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ConcurrentLinkedDeque.html) | Deque       | 是   | 否   | 是       | 是   | 否                 |
| [ArrayBlockingQueue](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ArrayBlockingQueue.html)       | Queue       | 是   | 否   | 是       | 是   | 否                 |
| [LinkedBlockingDeque](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/LinkedBlockingDeque.html)     | Deque       | 是   | 否   | 是       | 是   | 否                 |
| [PriorityBlockingQueue](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/PriorityBlockingQueue.html) | Queue       | 是   | 否   | 是       | 是   | 否                 |

{.show-header .left-text}

### ArrayList

```java
List<Integer> nums = new ArrayList<>();

// 添加
nums.add(2);
nums.add(5);
nums.add(8);

// 获取
System.out.println(nums.get(0));

// 索引 for 循环迭代
for (int i = 0; i < nums.size(); i++) {
    System.out.println(nums.get(i));
}

nums.remove(nums.size() - 1);
nums.remove(0); // 非常慢

for (Integer value : nums) {
    System.out.println(value);
}
```

### HashMap

```java
Map<Integer, String> m = new HashMap<>();
m.put(5, "Five");
m.put(8, "Eight");
m.put(6, "Six");
m.put(4, "Four");
m.put(2, "Two");

// 获取
System.out.println(m.get(6));

// Lambda forEach
m.forEach((key, value) -> {
    String msg = key + ": " + value;
    System.out.println(msg);
});
```

### HashSet

```java
Set<String> set = new HashSet<>();
if (set.isEmpty()) {
    System.out.println("空!");
}

set.add("dog");
set.add("cat");
set.add("mouse");
set.add("snake");
set.add("bear");

if (set.contains("cat")) {
    System.out.println("包含 cat");
}

set.remove("cat");
for (String element : set) {
    System.out.println(element);
}
```

### ArrayDeque

```java
Deque<String> a = new ArrayDeque<>();

// 使用 add()
a.add("Dog");

// 使用 addFirst()
a.addFirst("Cat");

// 使用 addLast()
a.addLast("Horse");

// [Cat, Dog, Horse]
System.out.println(a);

// 访问元素
System.out.println(a.peek());

// 移除元素
System.out.println(a.pop());
```

## 其他

### 访问修饰符 {.col-span-2}

| 修饰符    | 类   | 包   | 子类 | 全局 |
| ----------- | ---- | ---- | ---- | ---- |
| public      | 是   | 是   | 是   | 是   |
| protected   | 是   | 是   | 是   | 否   |
| 无修饰符  | 是   | 是   | 否   | 否   |
| private     | 是   | 否   | 否   | 否   |

{.show-header .left-text}

### 正则表达式

```java
String text = "I am learning Java";
// 移除所有空格
text.replaceAll("\\s+", "");

// 分割字符串
text.split("\\|");
text.split(Pattern.quote("|"));
```

参见: [Java 中的正则表达式](/regex#regex-in-java)

### 注释

```java
// 我是单行注释!

/*
我是
多行注释!
*/

/**
 * 这是
 * 文档
 * 注释
 */
```

### 关键字 {.col-span-2}

- `abstract`
- `continue`
- `for`
- `new`
- `switch`
- `assert`
- `default`
- `goto`
- `package`
- `synchronized`
- `boolean`
- `do`
- `if`
- `private`
- `this`
- `break`
- `double`
- `implements`
- `protected`
- `throw`
- `byte`
- `else`
- `import`
- `public`
- `throws`
- `case`
- `enum`
- `instanceof`
- `return`
- `transient`
- `catch`
- `extends`
- `int`
- `short`
- `try`
- `char`
- `final`
- `interface`
- `static`
- `void`
- `class`
- `finally`
- `long`
- `strictfp`
- `volatile`
- `const`
- `float`
- `native`
- `super`
- `while`

{.marker-none .cols-6}

### Math 方法

| 方法                  | 描述               |
| --------------------- | :----------------- |
| `Math.max(a,b)`       | a 和 b 的最大值    |
| `Math.min(a,b)`       | a 和 b 的最小值    |
| `Math.abs(a)`         | a 的绝对值         |
| `Math.sqrt(a)`        | a 的平方根         |
| `Math.pow(a,b)`       | a 的 b 次幂        |
| `Math.round(a)`       | 最接近的整数       |
| `Math.sin(ang)`       | ang 的正弦值       |
| `Math.cos(ang)`       | ang 的余弦值       |
| `Math.tan(ang)`       | ang 的正切值       |
| `Math.asin(ang)`      | ang 的反正弦值     |
| `Math.log(a)`         | a 的自然对数       |
| `Math.toDegrees(rad)` | 角度 rad 转换为度数 |
| `Math.toRadians(deg)` | 角度 deg 转换为弧度 |

### Try/Catch/Finally

```java
try {
  // 一些操作
} catch (Exception e) {
  e.printStackTrace();
} finally {
  System.out.println("总是会打印");
}
```

