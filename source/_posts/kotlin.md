---
title: Kotlin
date: 2023-02-26 16:24:31
background: bg-[#7954f6]
tags:
  - Cross-platform
  - Android
categories:
  - 编程
intro: |
  一份 Kotlin 快速参考备忘单，包含用法、示例等。
plugins:
  - copyCode
---

## Kotlin 简介

### main()

```kotlin
fun main() {
  println("你好，r3f.cn！")
  // 代码写在这里
}
```

`main()` 函数是每个 Kotlin 程序的起点，必须在执行前包含在代码中。

### 打印语句

```kotlin
println("你好，地球人！")
print("带我去")
print("见你们的领导。")

/*
打印：
你好，地球人！
带我去见你们的领导。
*/
```

### 注释

```kotlin
// 这是单行注释

/*
这是
多行
注释
*/
```

### 执行顺序

```kotlin
fun main() {
  println("我会第一个被打印。")
  println("我会第二个被打印。")
  println("我会第三个被打印。")
}
```

## 数据类型和变量

### 可变变量

```kotlin
var age = 25
age = 26
```

### 不可变变量

```kotlin
val goldenRatio = 1.618
```

### 类型推断

```kotlin
// 以下变量被赋予双引号内的字面值
// 因此推断类型为 String

var color = "紫色"
```

### 字符串连接

```kotlin
var streetAddress = "主街 123 号"
var cityState = "纽约州布鲁克林"

println(streetAddress + " " + cityState)
// 打印：主街 123 号 纽约州布鲁克林
```

### 字符串模板

```kotlin
var address = "主街 123 号"
println("地址是 $address")
// 打印：地址是 主街 123 号
```

### 内置属性和函数

```kotlin
var monument = "自由女神像"

println(monument.capitalize()) // 首字母大写
// 打印：自由女神像
println(monument.length)
// 打印：6 (注意：这里原文是21，对应 "the Statue of Liberty"，中文 "自由女神像" 长度是6)
// 如果要保持原文的输出，可以写 monument = "the Statue of Liberty"
// println(monument.capitalize())
// 打印: The Statue of Liberty
// println(monument.length)
// 打印: 21
```

### 字符转义 {.row-span-2}

```kotlin {.wrap}
print("\"太棒了！\" 我喊道。\"很简单，\" 他说。")

// 打印："太棒了！" 我喊道。"很简单，" 他说。
```

- `\n` 插入新行
- `\t` 插入制表符
- `\r` 插入回车符
- `\'` 插入单引号
- `\"` 插入双引号
- `\\` 插入反斜杠
- `\$` 插入美元符号

### 算术运算符

```kotlin
5 + 7  // 12
9 - 2   // 7
8 * 4   // 32
25 / 5  // 5
31 % 2 // 1
```

`+` 加法，`-` 减法，`*` 乘法，`/` 除法，`%` 取模

### 运算顺序

```kotlin
5 + 8 * 2 / 4 - 3 // 6
3 + (4 + 4) / 2 // 7
4 * 2 + 1 * 7    // 15
3 + 18 / 2 * 1   // 12
6 - 3 % 2 + 2   // 7
```

### 增强赋值运算符

```kotlin
var batteryPercentage = 80

// 长语法
batteryPercentage = batteryPercentage + 10

// 使用增强赋值运算符的短语法
batteryPercentage += 10
```

###自增和自减运算符

```kotlin
var year = 2019
year++   // 2020
year--   // 2019
```

### 数学库

```kotlin
Math.pow(2.0, 3.0) // 8.0 (2的3次方)
Math.min(6, 9)     // 6   (最小值)
Math.max(10, 12)   // 12  (最大值)
Math.round(13.7)  // 14  (四舍五入)
```

## 条件表达式

### If 表达式

```kotlin
var morning = true

if (morning) {
  println("早安，该起床了！")
}
// 打印：早安，该起床了！
```

### Else 表达式

```kotlin
var rained = false

if (rained) {
  println("今天不用浇花了。")
} else {
  println("植物需要浇水！")
}
// 打印：植物需要浇水！
```

### Else-If 表达式

```kotlin
var age = 65

if (age < 18 ) {
  println("你被认为是未成年人")
} else if (age < 60) {
  println("你被认为是成年人")
} else {
  println("你被认为是老年人")
}

// 打印：你被认为是老年人
```

### 比较运算符

```kotlin
var myAge = 19
var sisterAge = 11
var cousinAge = 11

myAge > sisterAge  // true (我的年龄大于妹妹的年龄)
myAge < cousinAge  // false (我的年龄小于表弟的年龄)
myAge >= cousinAge // true (我的年龄大于等于表弟的年龄)
myAge <= sisterAge // false (我的年龄小于等于妹妹的年龄)
```

### 逻辑运算符

```kotlin
var humid = true
var raining = true
var jacket = false // 原文 jacket = false，但 raining = true 时，jacket && raining 应该是 false
                   // 如果要让 jacket && raining 为 true, jacket 也应为 true

println(!humid)
// 打印：false (不潮湿)
println(jacket && raining) // 假设 jacket 为 true
// 打印：true (穿夹克并且下雨)
println(humid || raining)
// 打印：true (潮湿或者下雨)
```

### 与运算符：&&

```kotlin
var humid = true
var raining = true
var shorts = false
var sunny = false

// true AND true
println(humid && raining) // true (潮湿并且下雨)
// true AND false
println(humid && shorts)  // false (潮湿并且穿短裤)
// false AND true
println(sunny && raining) // false (晴天并且下雨)
// false AND false
println(shorts && sunny)  // false (穿短裤并且晴天)
```

### 或运算符：||

```kotlin
var late = true
var skipBreakfast = true
var underslept = false
var checkEmails = false

// true OR true
println(skipBreakfast || late) // true (不吃早餐或者迟到)
// true OR false
println(late || checkEmails)   // true (迟到或者检查邮件)
// false OR true
println(underslept || late)    // true (睡眠不足或者迟到)
// false OR false
println(checkEmails || underslept) // false (检查邮件或者睡眠不足)
```

### 非运算符

```kotlin
var hungry = true
var full = false

println(!hungry) // false (不饿)
println(!full)   // true (不饱)
```

### 求值顺序

```kotlin
!true && (false || true) // false
/*
(false || true) 首先求值为 true。
然后，求值 !true && true，最终结果为 false。
*/

!false && true || false // true
/*
!false 首先求值为 true。
然后 true && true 求值为 true。
接着，true || false 求值为 true，最终返回 true。
*/
```

### 嵌套条件

```kotlin
var studied = true
var wellRested = true

if (wellRested) {
  println("祝你今天好运！")
  if (studied) {
    println("你应该为考试做好准备了！")
  } else {
    println("考试前花几个小时学习吧！")
  }
}

// 打印：祝你今天好运！
// 打印：你应该为考试做好准备了！
```

### When 表达式

```kotlin
var grade = "A"

when (grade) {
  "A" -> println("干得漂亮！")
  "B" -> println("干得不错！") // 原文 "Great job!"，这里稍作区分
  "C" -> println("你通过了！")
  else -> println("差一点！下次一定要多准备！")
}
// 打印：干得漂亮！
```

### 范围运算符

```kotlin {.wrap}
var height = 46 // 英寸

if (height in 1..53) {
  println("抱歉，您必须至少 54 英寸高才能乘坐过山车")
}
// 打印：抱歉，您必须至少 54 英寸高才能乘坐过山车
```

### 相等运算符

```kotlin
var myAge = 22
var sisterAge = 21

myAge == sisterAge // false (我的年龄等于妹妹的年龄)
myAge != sisterAge // true (我的年龄不等于妹妹的年龄)
```

## 空安全

### 可空与不可空

```kotlin
var a: String = "Kotlin" // a 永远不能为 null
a = null // 编译错误
var b: String? = "Kotlin" // b 可以为 null
b = null // ok
```

### 安全调用

```kotlin
val a = "Kotlin"
val b: String? = null
println(a.length) // 可以安全调用，因为 a 永远不为 null
println(b?.length) // b?.length 返回 b 的长度，如果 b 为 null 则返回 null
println(a?.length) // 不必要的安全调用
```

### 链式安全调用

```kotlin
bob?.department?.head?.name // 如果任何属性为 null，链式调用返回 null
```

### Elvis 运算符

```kotlin
val l = b?.length ?: -1 // 如果 b 为 null，返回默认值 -1
// 等同于：
val l: Int = if (b != null) b.length else -1
```

### 非空断言运算符

```kotlin
val l = b!!.length // 如果 b 为 null，抛出 NullPointerException
```

## 集合

### 不可变列表

```kotlin {.wrap}
var programmingLanguages = listOf("C#", "Java", "Kotlin", "Ruby")
```

### 可变列表

```kotlin {.wrap}
var fruits = mutableListOf("橙子", "苹果", "香蕉", "芒果")
```

### 访问列表

```kotlin {.wrap}
var cars = listOf("宝马", "法拉利", "沃尔沃", "特斯拉")

println(cars[2]) // 打印：沃尔沃
```

### Size 属性

```kotlin {.wrap}
var worldContinents = listOf("亚洲", "非洲", "北美洲", "南美洲", "南极洲", "欧洲", "澳洲")

println(worldContinents.size) // 打印：7
```

### 列表操作 {.row-span-2}

```kotlin {.wrap}
var seas = listOf("黑海", "加勒比海", "北海")
println(seas.contains("北海")) // 打印：true

// contains() 函数对任何列表执行读取操作，并确定元素是否存在
seas.add("波罗的海") // 错误：无法写入不可变列表
// add() 函数只能在可变列表上调用，因此上面的代码会抛出错误
```

### 不可变集

```kotlin {.wrap}
var primaryColors = setOf("红色", "蓝色", "黄色")
```

### 可变集

```kotlin {.wrap}
var womenInTech = mutableSetOf("阿达·洛芙莱斯", "格蕾丝·霍珀", "拉迪亚·珀尔曼", "玛丽·肯尼思·凯勒修女")
```

### 访问集合元素 {.row-span-2}

```kotlin {.wrap}
var companies = setOf("Facebook", "Apple", "Netflix", "Google")

println(companies.elementAt(3))
// 打印：Google
println(companies.elementAt(4))
// 返回错误
println(companies.elementAtOrNull(4))
// 打印：null
```

### 不可变映射

```kotlin {.wrap}
var averageTemp = mapOf("冬天" to 35,  "春天" to 60,  "夏天" to 85, "秋天" to 55)
```

### 可变映射

```kotlin {.wrap}
var europeanDomains = mutableMapOf("德国" to "de", "斯洛伐克" to "sk", "匈牙利" to "hu", "挪威" to "no")
```

### 检索映射的键和值

```kotlin {.wrap}
var oscarWinners = mutableMapOf("寄生虫" to "奉俊昊", "绿皮书" to "吉姆·伯克", "水形物语" to "吉尔莫·德尔·托罗")

println(oscarWinners.keys)
// 打印：[寄生虫, 绿皮书, 水形物语]

println(oscarWinners.values)
// 打印：[奉俊昊, 吉姆·伯克, 吉尔莫·德尔·托罗]
println(oscarWinners["寄生虫"])
// 打印：奉俊昊
```

### 添加和删除映射条目

```kotlin {.wrap}
var worldCapitals = mutableMapOf("美国" to "华盛顿特区", "德国" to "柏林", "墨西哥" to "墨西哥城", "法国" to "巴黎")

worldCapitals.put("巴西", "巴西利亚")
println(worldCapitals)
// 打印：{美国=华盛顿特区, 德国=柏林, 墨西哥=墨西哥城, 法国=巴黎, 巴西=巴西利亚}

worldCapitals.remove("德国")
println(worldCapitals)
// 打印：{美国=华盛顿特区, 墨西哥=墨西哥城, 法国=巴黎, 巴西=巴西利亚}
```

## 函数

### 函数

```kotlin
fun greet() {
  println("你好！")
}

fun main() {
  //函数调用
  greet() //打印：你好！
}
```

### 函数参数

```kotlin {.wrap}
fun birthday(name: String, age: Int) {
   println("生日快乐，$name！你今天 $age 岁了！")
}

fun main() {
  birthday("奥斯卡", 26)
  //打印：生日快乐，奥斯卡！你今天 26 岁了！ (原文输出是25，但调用是26)
  birthday("阿玛拉", 30)
  //打印：生日快乐，阿玛拉！你今天 30 岁了！
}
```

### 默认参数

```kotlin {.wrap}
fun favoriteLanguage(name: String, language: String = "Kotlin") { // name 参数也需要类型
  println("你好，$name。你最喜欢的编程语言是 $language")
}

fun main() {
  favoriteLanguage("玛侬")
  //打印：你好，玛侬。你最喜欢的编程语言是 Kotlin

  favoriteLanguage("李", "Java")
  //打印：你好，李。你最喜欢的编程语言是 Java
}
```

### 命名参数

```kotlin {.wrap}
fun findMyAge(currentYear: Int, birthYear: Int) {
   var myAge = currentYear - birthYear
   println("我 $myAge 岁了。")
}

fun main() {
  findMyAge(currentYear = 2020, birthYear = 1995)
  //打印：我 25 岁了。
  findMyAge(birthYear = 1920, currentYear = 2020)
  //打印：我 100 岁了。
}
```

### 返回语句

```kotlin {.wrap}
//返回类型在括号外声明
fun getArea(length: Int, width: Int): Int {
  var area = length * width

  //return 语句
  return area
}

fun main() {
  var myArea = getArea(10, 8)
  println("面积是 $myArea。")
  //打印：面积是 80。
}
```

### 单表达式函数

```kotlin{.wrap}
fun fullName(firstName: String, lastName: String) = "$firstName $lastName"

fun main() {
  println(fullName("爱莉安娜", "奥尔特加"))
  //打印：爱莉安娜 奥尔特加
  println(fullName("凯", "吉滕斯"))
  //打印：凯 吉滕斯
}
```

### 函数字面量

```kotlin{.wrap}
fun main() {
  //匿名函数：
  var getProduct = fun(num1: Int, num2: Int): Int {
    return num1 * num2
  }
  println(getProduct(8, 3))
  //打印：24
  //Lambda 表达式
  var getDifference = { num1: Int, num2: Int -> num1 - num2 }
  println(getDifference(10, 3))
  //打印：7
}
```

## 类

### 类示例

```kotlin
//带有包含默认值属性的类
class Student {
  var name = "露西娅"
  var semester = "秋季"
  var gpa = 3.95
}

//不带类体的简写语法
class Student
```

### 类实例

```kotlin
// 类
class Student {
  var name = "露西娅"
  var semester = "秋季"
  var gpa = 3.95
}

fun main() {
  var student = Student()
  // 实例
  println(student.name)
  // 打印：露西娅
  println(student.semester)
  // 打印：秋季
  println(student.gpa)
  // 打印：3.95
}
```

### 主构造函数

```kotlin {.wrap}
class Student(val name: String, val gpa: Double, val semester: String, val estimatedGraduationYear: Int)

fun main() {
  var student = Student("露西娅", 3.95, "秋季", 2022)
  println(student.name)
  //打印：露西娅
  println(student.gpa)
  //打印：3.95
  println(student.semester)
  //打印：秋季
  println(student.estimatedGraduationYear)
  //打印：2022
}
```

### 初始化代码块

```kotlin {.wrap}
class Student(val name: String, val gpa: Double, val semester: String, val estimatedGraduationYear: Int) {
  init {
    println("$name 还有 ${estimatedGraduationYear - 2020} 年大学毕业。")
  }
}

fun main() {
  var student = Student("露西娅", 3.95, "秋季", 2022)
  //打印：露西娅 还有 2 年大学毕业。
}
```

### 成员函数 {.col-span-2}

```kotlin {.wrap}
class Student(val name: String, val gpa: Double, val semester: String, val estimatedGraduationYear: Int) {

  init {
    println("$name 还有 ${estimatedGraduationYear - 2020} 年大学毕业。")
  }

  //成员函数
  fun calculateLetterGrade(): String {
    return when {
      gpa >= 3.0 -> "A"
      gpa >= 2.7 -> "B"
      gpa >= 1.7 -> "C"
      gpa >= 1.0 -> "D"
      else -> "E"
    }
  }
}

//创建实例并调用函数时，将执行 when 表达式并返回字母等级
fun main() {
  var student = Student("露西娅", 3.95, "秋季", 2022)
  //打印：露西娅 还有 2 年大学毕业。
  println("${student.name} 的字母等级是 ${student.calculateLetterGrade()}。")
  //打印：露西娅 的字母等级是 A。
}
```

## 另请参阅

- [Kotlin 语言官方文档](https://kotlinlang.org/) _(kotlinlang.org)_
