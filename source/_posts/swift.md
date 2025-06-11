---
title: Swift
date: 2023-02-28 14:50:01
background: bg-[#eb4e38]
tags:
  - Apple
  - iOS
  - iPadOS
categories:
  - 编程
intro: |
  本速查表提供了 Swift 使用示例，涵盖了 Swift 基础知识、控制流等。
plugins:
  - copyCode
---

## 入门

### 变量 {.row-span-2}

```swift
var score = 0  // 变量
let pi = 3.14  // 常量

var greeting = "Hello"
var numberOfToys = 8
var isMorning = true

var numberOfToys: Int = 8
numberOfToys += 1

print(numberOfToys)
// 打印 "9"
```

### 类型注解

```swift
var greeting: String = "Hello"
var numberOfToys: Int = 8
var isMorning: Bool = true
var price: Double = 8.99
```

### 算术运算符 {.row-span-3}

- `+` 加
- `-` 减
- `*` 乘
- `/` 除
- `%` 余

{.cols-2 .marker-none}

---

```swift
var x = 0
x = 4 + 2 // x 现在是 6
x = 4 - 2 // x 现在是 2
x = 4 * 2 // x 现在是 8
x = 4 / 2 // x 现在是 2
x = 4 % 2 // x 现在是 0
```

---

- `+=` 加并赋值
- `-=` 减并赋值
- `*=` 乘并赋值
- `/=` 除并赋值
- `%=` 取余并赋值

{.marker-none}

#### 复合赋值运算符

```swift
var numberOfDogs = 100
numberOfDogs += 1
print("There are \(numberOfDogs) Dalmatians!")

// 打印: There are 101 Dalmatians!
```

### 字符串插值

```swift
var apples = 6
print("I have \(apples) apples!")

// 打印: I have 6 apples!
```

### 多行字符串

```swift
let myLongString = """
Swift?
这是我最喜欢的语言！
是的！
"""
```

### 代码注释

```swift
// 这行代表 Swift 中的注释。

/*
这全部都被注释掉了。
都不会运行！
*/
```

### 形成元组 {.col-span-2}

```swift
let player = ("Maya", 5, 150)

print(player) // ("Maya", 5, 150)
print("\(player.0): level \(player.1), \(player.2) pts") // Maya: level 5, 150 pts
```

### 分解元组

```swift
let player = (name: "Maya", level: 5)
let (currentName, curLevel) = player
print("\(currentName): level \(curLevel)")
// 打印: Maya: level 5
```

### 特殊注释语法 (MARK)

```swift
// MARK: -视图设置
```

`MARK` 可用于在列中显示注释

### 特殊注释语法 (TODO)

```swift
// TODO: 更新逻辑以适应数据更改
```

`TODO` 用于显示需要完成的事项提醒

### 特殊注释语法 (FIXME)

```swift
// FIXME: 修复对现有条目进行更改时的错误行为
```

`FIXME` 用于显示需要修复的事项提醒

## 变量

### 变量声明

变量使用 `var` 声明：

```swift
var greeting = "Hello"
var numberOfToys = 8
var isMorning = true
```

为清晰起见，变量声明可以包含类型注解：

```swift
var greeting: String = "Hello"
var numberOfToys: Int = 8
var isMorning: Bool = true
```

变量是可变的。它们的值可以更改：

```swift
var numberOfToys: Int = 8
numberOfToys += 1

print(numberOfToys)
// 打印 "9"
```

### 常量

常量使用 `let` 声明：

```swift
let greeting = "Hello"
let numberOfToys = 8
let isMorning = true
```

为清晰起见，常量声明可以包含类型注解：

```swift
let greeting: String = "Hello"
let numberOfToys: Int = 8
let isMorning: Bool = true
```

常量是不可变的。它们的值不能更改：

```swift
let numberOfToys: Int = 8
numberOfToys += 1
// 错误: numberOfToys 是不可变的
```

### 计算变量 (get 和 set) {.row-span-3}

```swift
import Foundation

let df = DateFormatter()
df.dateFormat = "d MMMM yyyy"

guard var birth = df.date(from: "5 June 1999") else {
    print("日期无效")
    return
}

var age: Int {
    Calendar.current
        .dateComponents([.year],
                        from: birth,
                        to: Date()).year!
}

print(age) // 23
guard let birth2 = df.date(from: "5 June 2002") else {
    print("日期无效")
    return
}
birth = birth2
print(age) // 20
```

在下面的示例中，`distanceInFeet` 有一个 `getter` 和一个 `setter`。由于 `setter` 的存在，`getter` 需要关键字 `get`：

```swift
var distanceInMeters: Float = 100

var distanceInFeet: Float {
  get {
    distanceInMeters *3.28
  }
  set(newDistance) {
    distanceInMeters = newDistance /3.28
  }
}

print(distanceInMeters) // 100.0
print(distanceInFeet)   // 328.0

distanceInFeet = 250
print(distanceInMeters) // 76.21951
print(distanceInFeet)   // 250.0

distanceInMeters = 800
print(distanceInMeters) // 800.0
print(distanceInFeet)   // 2624.0
```

### willSet {.row-span-2}

```swift
var distance = 5 {
  willSet {
    print("距离将被设置")
  }
}

distance = 10 // 打印: 距离将被设置
```

新值可以在 `willSet` 中访问：

```swift
var distance = 5 {
  willSet(newDistance) {
    print("距离将被设置为 \(newDistance)")
  }
}

distance = 10 // 打印: 距离将被设置为 10
```

`willSet` 可用于在设置变量值之前执行一些代码

### didSet

```swift
var distance = 5 {
  didSet {
    print("距离已设置为 \(distance)")
    print("它的旧值是: \(oldValue)")
  }
}
distance = 10 // 打印: 距离已设置为 10
              // 打印: 它的旧值是: 5
```

### willSet 和 didSet

```swift
var distance = 5 {
  willSet(newDistance) {
    print("距离将被设置为 \(newDistance)")
  }
  didSet {
    print("距离已设置为 \(distance)")
    print("它的旧值是: \(oldValue)")
  }
}
distance = 10
```

## 条件

### if 语句

```swift
var halloween = true
if halloween {
  print("不给糖就捣蛋！")
}
// 打印: 不给糖就捣蛋！
if 5 > 3 {
  print("5 大于 3")
} else {
  print("5 不大于 3")
}
// 输出: "5 大于 3"
```

### else 语句

```swift
var turbulence = false

if turbulence {
  print("请坐好。")
} else {
  print("您可以自由走动。")
}
// 打印: 您可以自由走动。
```

### else if 语句

```swift
var weather = "rainy"
if weather == "sunny" {
  print("涂点防晒霜")
} else if weather == "rainy" {
  print("带把伞")
} else if weather == "snowing" {
  print("穿上你的雪地靴")
} else {
  print("无效的天气")
}
// 打印: 带把伞
```

### 比较运算符

```swift
5 > 1      // true
6 < 10     // true
2 >= 3     // false
3 <= 5     // true
"A" == "a" // false
"B" != "b" // true
```

-`<` 小于 <br> -`>` 大于 <br> -`<=` 小于等于 <br> -`>=` 大于等于 <br> -`==` 等于 <br> -`!=` 不等于

### 范围运算符

```swift
a...b      // a 和 b 之间的数字 (包括 a 和 b)
a..<b      // a 和 b 之间的数字 (包括 a 但不包括 b)
...b      // 直到 b 的数字 (包括 b)
```

-`a...b` 闭区间 <br> -`a..<b` 半开区间 <br> -`...b` 单边区间

### 三元条件运算符

```swift
var driverLicense = true

driverLicense
    ? print("驾驶座") : print("乘客座")
// 打印: 驾驶座
```

### switch 语句

```swift
var secondaryColor = "green"

switch secondaryColor {
  case "orange":
    print("红色和黄色的混合物")
  case "purple":
    print("红色和蓝色的混合物")
  default:
    print("这可能不是二次色")
}
// 打印: 蓝色和黄色的混合物
```

### switch 语句：区间匹配

```swift
let year = 1905
var artPeriod: String

switch year {
  case 1860...1885:
    artPeriod = "印象派"
  case 1886...1910:
    artPeriod = "后印象派"
  default:
    artPeriod = "未知"
}
// 打印: 后印象派
```

### switch 语句：复合情况

```swift
let service = "Seamless"

switch service {
case "Uber", "Lyft":
    print("出行")
  case "DoorDash", "Seamless", "GrubHub":
    print("餐厅外卖")
  case "Instacart", "FreshDirect":
    print("生鲜配送")
  default:
    print("未知服务")
}
// 打印: 餐厅外卖
```

### switch 语句：where 子句

```swift
let num = 7

switch num {
  case let x where x % 2 == 0:
    print("\(num) 是偶数")
  case let x where x % 2 == 1:
    print("\(num) 是奇数")
  default:
    print("\(num) 无效")
}

// 打印: 7 是奇数
```

### 逻辑运算符

```swift
!true  // false
!false //true
```

### 逻辑运算符 &&

```swift
true && true   // true
true && false  // false
false && true  // false
false && false // false
```

### 逻辑运算符 ||

```swift
true || true   // true
true || false  // true
false || true  // true
false || false // false
```

### 组合逻辑运算符

```swift
!false && true || false // true
```

`!false && true` 首先计算并返回 `true` 然后，表达式 `true || false` 计算并返回最终结果 `true`

```swift
false || true && false // false
```

`true && false` 首先计算并返回 `false` 然后，表达式 `false || false` 计算并返回最终结果 `false`

### 控制执行顺序

```swift

// 没有括号:
true || true && false || false
//----> true

// 有括号:
(true || true) && (false || false)
//----> false

```

### 简单卫语句

```swift
func greet(name: String?) {
  guard let unwrapped = name else {
    print("你好，客人！")
    return
  }
  print("你好 \(unwrapped)！")
}
greet(name: "Asma") // 输出: 你好 Asma！
greet(name: nil)    // 输出: 你好，客人！
```

## 循环

### 范围

```swift
let zeroToThree = 0...3
//zeroToThree: 0, 1, 2, 3
```

### stride() 函数

```swift
for oddNum in stride(from: 1, to: 5, by: 2) {
  print(oddNum)
}
// 打印: 1
// 打印: 3
```

### for-in 循环

```swift
for char in "hehe" {
  print(char)
}
// 打印: h
// 打印: e
// 打印: h
// 打印: e
```

### continue 关键字

```swift
for num in 0...5 {
  if num % 2 == 0 {
    continue
  }
  print(num)
}
// 打印: 1
// 打印: 3
// 打印: 5
```

`continue` 关键字将强制循环继续下一次迭代

### break 关键字

```swift
for char in "supercalifragilistic" {
if char == "c" {
    break
  }
  print(char)
}
// 打印: s
// 打印: u
// 打印: p
// 打印: e
// 打印: r
```

### 使用下划线

```swift
for _ in 1...3 {
  print("Ole")
}
// 打印: Ole
// 打印: Ole
// 打印: Ole
```

### while 循环

```swift
var counter = 1
var stopNum = Int.random(in: 1...10)

while counter < stopNum {
  print(counter)
  counter += 1
}
// 循环打印直到满足停止条件
```

`while` 循环接受一个条件，并在提供的条件为 `true` 时继续执行其主体代码。如果条件永远不为 false，循环将一直运行，程序将陷入 `无限循环`

## 数组和集合

### 数组

```swift
var scores = [Int]()
// 数组为空: []
```

### .count 属性

```swift
var grocery = ["🥓", "🥞", "🍪", "🥛", "🍊"]
print(grocery.count)
// 打印: 5
```

### 索引 {.row-span-2}

索引指的是项目在有序列表中的位置，使用下标语法 `array[index]` 从数组中检索单个元素。

```swift
var vowels = ["a", "e", "i", "o", "u"]

print(vowels[0]) // 打印: a
print(vowels[1]) // 打印: e
print(vowels[2]) // 打印: i
print(vowels[3]) // 打印: o
print(vowels[4]) // 打印: u
```

注意：Swift 数组是零索引的，这意味着第一个元素的索引为 0。

### 使用数组字面量初始化

```swift
// 使用类型推断:
var snowfall = [2.4, 3.6, 3.4, 1.8, 0.0]
// 显式类型:
var temp: [Int] = [33, 31, 30, 38, 44]
```

### 使用默认值初始化

```swift
var teams = [Int](repeating: 0, count: 3)
print(teams) // 打印: [0, 0, 0]
// 或者使用 Array 类型
var sizes = Array<Int>(repeating: 0, count: 3)
print(sizes) // 打印: [0, 0, 0]
```

### .append() 方法和 += 运算符

```swift
var gymBadges = ["Boulder", "Cascade"]
gymBadges.append("Thunder")
gymBadges += ["Rainbow", "Soul"]
// ["Boulder", "Cascade", "Thunder",
// "Rainbow", "Soul"]
```

### .insert() 和 .remove() 方法

```swift
var moon = ["🌖", "🌗", "🌘", "🌑"]
moon.insert("🌕", at: 0)
// ["🌕", "🌖", "🌗", "🌘", "🌑"]

moon.remove(at: 4)
// ["🌕", "🌖", "🌗", "🌘"]
```

### 遍历数组

```swift
var employees = ["Peter", "Denial", "Jame"]
for person in employees {
  print(person)
}
// 打印: Peter
// 打印: Denial
// 打印: Jam
```

### 集合 (Set)

```swift
var paintingsInMOMA: Set = [
  "The Dream",
  "The Starry Night",
  "The False Mirror"
]
```

我们可以使用集合 (`Set`) 来存储相同数据类型的 `唯一` 元素

### 空集合 (Set)

```swift
var team = Set<String>()

print(team)
// 打印: []
```

### 填充集合

```swift
var vowels: Set = ["a", "e", "i", "o","u"]
```

要创建一个填充了值的集合，请在赋值运算符之前使用 `Set` 关键字。

### .insert()

```swift
var cookieJar: Set = [
  "Chocolate Chip",
  "Oatmeal Raisin"
]
// 添加一个新元素
cookieJar.insert("Peanut Butter Chip")
```

### .remove() 和 .removeAll() 方法

```swift
var oddNumbers: Set = [1, 2, 3, 5]

// 删除现有元素
oddNumbers.remove(2)
// 删除所有元素
oddNumbers.removeAll()
```

### .contains()

```swift
var names: Set = ["Rosa", "Doug", "Waldo"]
print(names.contains("Lola")) // 打印: false

if names.contains("Waldo"){
  print("Waldo 在这里！")
} else {
  print("Waldo 在哪里？")
}
// 打印: Waldo 在这里！
```

### .isEmpty 属性

```swift
var emptyList = [String]()
print(emptyList.isEmpty)     // 打印: true

var populatedList: [Int] = [1, 2, 3]
print(populatedList.isEmpty) // 打印: false
```

### 遍历集合

```swift
var recipe: Set = ["Egg", "Flour", "Sugar"]

for ingredient in recipe {
  print ("在食谱中加入 \(ingredient)")
}
```

### .isEmpty 属性

```swift
var emptySet = Set<String>()
print(emptySet.isEmpty)     // 打印: true

var populatedSet: Set = [1, 2, 3]
print(populatedSet.isEmpty) // 打印: false
```

### .count 属性

```swift
var band: Set = ["Peter", "Denial", "Jame"]

print("乐队有 \(band.count) 名队员。")
// 打印: 乐队有 4 名队员。
```

### .intersection() 交集

```swift
var setA: Set = ["A", "B", "C", "D"]
var setB: Set = ["C", "D", "E", "F"]

var setC = setA.intersection(setB)
print(setC) // 打印: ["D", "C"]
```

### .union() 并集

```swift
var setA: Set = ["A", "B", "C", "D"]
var setB: Set = ["C", "D", "E", "F"]

var setC = setA.union(setB)
print(setC)
// 打印: ["B", "A", "D", "F", "C", "E"]
```

### .symmetricDifference() 对称差集

```swift
var setA: Set = ["A", "B", "C", "D"]
var setB: Set = ["C", "D", "E", "F"]

var setC = setA.symmetricDifference(setB)
print(setC)
// 打印: ["B", "E", "F", "A"]
```

### .subtracting() 差集

```swift
var setA: Set = ["A", "B", "C", "D"]
var setB: Set = ["C", "D"]

var setC = setA.subtracting(setB)
print(setC)
// 打印: ["B", "A"]
```

## 字典

### 基本字典

```swift
var dictionaryName = [
  "Key1": "Value1",
  "Key2": "Value2",
  "Key3": "Value3"
]
```

一个 `无序` 的数据对或键值对集合

### 键

```swift
var fruitStand = [
  "Coconuts": 12,
  "Pineapples": 12,
  "Papaya": 12
]
```

每个 `键` 都是 `唯一` 的，即使它们都包含相同的 `值`

### 类型一致性

```swift
var numberOfSides = [
  "triangle": 3,
  "square": 4,
  "rectangle": 4
]
```

仅包含 `String` 键和 `Int` 值

### 初始化并填充字典

```swift
var employeeID = [
  "Hamlet": 1367,
  "Horatio": 8261,
  "Ophelia": 9318
]
```

### 初始化空字典

```swift
// 初始化器语法:
var yearlyFishPopulation = [Int: Int]()

// 空字典字面量语法:
var yearlyBirdPopulation: [Int: Int] = [:]
```

### 添加到字典

```swift
var pronunciation = [
  "library": "lai·breh·ree",
  "apple": "a·pl"
]
// 新键: "programming", 新值: "prow gra"
pronunciation["programming"] = "prow·gra"
```

### 删除键值对 {.row-span-2}

```swift
var bookShelf = [
  "Goodnight": "Margaret Wise Brown",
  "The BFG": "Roald Dahl",
  "Falling Up": "Shel Silverstein",
  "No, David!": "David Shannon"
]
// 通过将键设置为 nil 来删除值
bookShelf["The BFG"] = nil

// 使用 .removeValue() 删除值
bookShelf.removeValue(forKey: "Goodnight")

// 删除所有值
bookShelf.removeAll()
```

### 修改键值对 {.row-span-2}

```swift
var change = [
  "Quarter": 0.29,
  "Dime": 0.15,
  "Nickel": 0.05
]

// 使用下标语法更改值
change["Quarter"] = .25

// 使用 .updateValue() 更改值
change.updateValue(.10, forKey: "Dime")
```

要更改键值对的值，请使用 `.updateValue()` 方法或下标语法，方法是在字典名称后附加方括号 `[ ]` 并在其中包含现有键，然后添加赋值运算符 _(`= `)_ 后跟修改后的值

### .isEmpty 属性

```swift
var bakery = [String:Int]()

// 检查字典是否为空
print(bakery.isEmpty) // 打印 true
bakery["Cupcakes"] = 12
// 检查字典是否为空
print(bakery.isEmpty) // 打印 false
```

### .count 属性

```swift
var fruitStand = [
  "Apples": 12,
  "Oranges": 17 // 注意：这里原文可能有误，应该是 "Oranges": 17
]
print(fruitStand.count) // 打印: 2
```

### 将值赋给变量

```swift
var hex = [
  "red": "#ff0000",
  "yellow": "#ffff00",
  "blue": "#0000ff",
]

print("蓝色十六进制代码 \(hex["blue"])")
// 打印: 蓝色十六进制代码 Optional("#0000ff")

if let redHex = hex["red"] {
  print("红色十六进制代码 \(redHex)")
}
// 打印: 红色十六进制代码 #ff0000
```

将键值对的值赋给变量将返回一个可选值。要提取值，请使用可选展开

### 遍历字典

```swift
var emojiMeaning = [
  "🤔": "思考脸",
  "😪": "困倦脸",
  "😵": "眩晕脸"
]
// 遍历键和值
for (emoji, meaning) in emojiMeaning {
  print("\(emoji) 被称为 '\(meaning)Emoji'")
}
// 仅遍历键
for emoji in emojiMeaning.keys {
  print(emoji)
}
// 仅遍历值
for meaning in emojiMeaning.values {
  print(meaning)
}
```

## 函数

### 基本函数

```swift
func washCar() -> Void {
  print("肥皂")
  print("擦洗")
  print("冲洗")
  print("擦干")
}
```

### 调用函数

```swift
func greetLearner() {
 print("欢迎来到 r3f.cn！")
}
// 函数调用:
greetLearner()
// 打印: 欢迎来到 r3f.cn！
```

### 返回值

```swift
let birthYear = 1994
var currentYear = 2020

func findAge() -> Int {
  return currentYear-birthYear
}

print(findAge()) // 打印: 26
```

### 多个参数 {.col-span-2}

```swift
func convertFracToDec(numerator: Double, denominator: Double) -> Double {
  return numerator / denominator
}

let decimal = convertFracToDec(numerator: 1.0, denominator: 2.0)
print(decimal) // 打印: 0.5
```

### 省略参数标签

```swift
func findDiff(_ a: Int, b: Int) -> Int {
  return a -b
}

print(findDiff(6, b: 4)) // 打印: 2
```

### 返回多个值 {.col-span-2}

```swift
func smartphoneModel() -> (name: String, version: String, yearReleased: Int) {
  return ("iPhone", "8 Plus", 2017)
}
let phone = smartphoneModel()

print(phone.name)         // 打印: iPhone
print(phone.version)      // 打印: 8 Plus
print(phone.yearReleased) // 打印: 2017
```

### 参数和实际参数

```swift
func findSquarePerimet(side: Int) -> Int {
  return side *4
}

let perimeter = findSquarePerimet(side: 5)
print(perimeter) // 打印: 20

// 参数: side
// 实际参数: 5
```

### 隐式返回

```swift
func nextTotalSolarEclipse() -> String {
  "2024年4月8日 🌎"
}

print(nextTotalSolarEclipse())
// 打印: 2024年4月8日 🌎
```

### 默认参数

```swift
func greet(person: String = "客人") {
  print("你好 \(person)")
}
greet() // 你好 客人
greet(person: "Aliya") // 你好 Aliya
```

### 输入输出参数 {.row-span-2}

```swift
var currentSeason = "冬天"

func season(month: Int, name: inout String) {
  switch month {
    case 1...2:
      name = "冬天 ⛄️"
    case 3...6:
      name = "春天 🌱"
    case 7...9:
      name = "夏天 ⛱"
    case 10...11:
      name = "秋天 🍂"
    default:
      name = "未知"
  }
}
season(month: 4, name: &currentSeason)

print(currentSeason) // 春天 🌱
```

### 可变参数

```swift
func totalStudent(data: String...) -> Int {
  let numStudents = data.count
  return numStudents
}

print(totalStudent(data: "Denial", "Peter"))
// 打印: 2
```

### 可选参数

```swift
func getFirstInitial(from name: String?) -> String? {
  return name?.first
}
```

函数可以接受可选类型并返回可选类型。当函数无法返回所请求类型的合理实例时，它应该返回 `nil`

## 结构体

### 结构体创建

```swift
struct Building {
  var address: String
  var floors: Int
  init(address: String, floors: Int) {
    self.address = address
    self.floors = floors
  }
}
```

结构体或 structs 用于在代码中以编程方式表示现实生活中的对象。结构体使用 `struct` 关键字创建，后跟其名称，然后是包含其属性和方法的主体

### 默认属性值

```swift
struct Car {
  var numOfWheels = 4
  var topSpeed = 80
}

var reliantRobin = Car(numOfWheels: 3)

print(reliantRobin.numOfWheels) // 打印: 3
print(reliantRobin.topSpeed)    // 打印: 80
```

### 结构体实例创建

```swift
struct Person {
  var name: String
  var age: Int

  init(name: String, age: Int) {
    self.name = name
    self.age = age
  }
}

// Person 实例:
var morty = Person(name: "Peter", age: 14)
```

### init() 方法 {.row-span-2}

```swift
struct TV {
  var size: Int
  var type: String

  init(size: Int, type: String) {
    self.size = size
    self.type = type
  }
}
```

使用 `TV` 类

```swift
var newTV = TV(size: 65, type: "LED")
```

### 检查类型

```swift
print(type(of: "abc")) // 打印: String
print(type(of: 123))   // 打印: Int (原文为 123，应为 Int)
```

### 异变方法 (mutating) {.row-span-2}

```swift
struct Menu {
  var menuItems = ["薯条", "汉堡"]
  mutating func addToMenu(dish: String) {
    self.menuItems.append(dish)
  }
}
```

使用 `Menu` 类

```swift
var dinerMenu = Menu()
dinerMenu.addToMenu(dish: "吐司")
print(dinerMenu.menuItems)
// 打印: ["薯条", "汉堡", "吐司"]
```

### 结构体方法

```swift
struct Dog {
  func bark() {
    print("汪")
  }
}
let fido = Dog()
fido.bark() // 打印: 汪
```

## 类

### 引用类型 (class) {.row-span-2}

```swift
class Player {
  var name: String

  init(name: String) {
    self.name = name
  }
}

var player1 = Player(name: "Tomoko")
var player2 = player1
player2.name = "Isabella"

print(player1.name) // Isabella
print(player2.name) // Isabella
```

### 类的实例

```swift
class Person {
  var name = ""
  var age = 0
}

var sonny = Person()
// sonny 现在是 Person 的一个实例
```

### init() 方法 {.row-span-2}

```swift
class Fruit {
  var hasSeeds = true
  var color: String

  init(color: String) {
    self.color = color
  }
}
```

使用 Fruit 类

```swift
let apple = Fruit(color: "red")
```

可以使用 `init()` 方法和相应的初始化属性来初始化类。在 `init()` 方法中，`self` 关键字用于引用类的实际实例并分配属性值

### 类属性

```swift
// 假设 Student 类已定义
class Student {
    var name: String = ""
    var year: Int = 0
    var gpa: Double = 0.0
    var honors: Bool = false
}

var ferris = Student()

ferris.name = "Ferris Bueller"
ferris.year = 12
ferris.gpa = 3.81
ferris.honors = false
```

### 继承 {.row-span-2}

假设我们有一个 BankAccount 类：

```swift
class BankAccount {
  var balance = 0.0
  func deposit(amount: Double) {
    balance += amount
  }
  func withdraw(amount: Double) {
    balance -= amount
  }
}
```

`SavingsAccount` 继承 `BankAccount` 类

```swift
class SavingsAccount: BankAccount {
  var interest = 0.0

  func addInterest() {
    let interest = balance *0.005
    self.deposit(amount: interest)
  }
}
```

新的 `SavingsAccount` 类（子类）自动获得 `BankAccount` 类（超类）的所有特性。此外，`SavingsAccount` 类定义了一个 `.interest` 属性和一个 `.addInterest()` 方法。

### 示例

使用数据类型

```swift
class Student {
  var name: String
  var year: Int
  var gpa: Double
  var honors: Bool
  // 需要初始化器
  init(name: String, year: Int, gpa: Double, honors: Bool) {
      self.name = name
      self.year = year
      self.gpa = gpa
      self.honors = honors
  }
}
```

使用默认属性值

```swift
class Student {
  var name = ""
  var gpa = 0.0
  var honors = false
}
```

### 这是一个结构体定义和类定义的示例

```swift
struct Resolution {
  var width = 0
  var height = 0
}
class VideoMode {
  var resolution = Resolution()
  var interlaced = false
  var frameRate = 0.0
  var name: String?
}
```

`Resolution` 结构体定义和 `VideoMode` 类定义仅描述 `Resolution` 或 `VideoMode` 的外观，创建结构体或类的实例：

```swift
let resolution = Resolution(width: 1920)
let someVideoMode = VideoMode()
```

## 枚举

### 定义枚举

```swift
enum Day {
  case monday
  case tuesday
  case wednesday
  case thursday
  case friday
  case saturday
  case sunday
}

let casualWorkday: Day = .friday
```

### Switch 语句

```swift
enum Dessert {
  case cake(flavor: String)
  case vanillaIceCream(scoops: Int)
  case brownie
}

let customerOrder: Dessert = .cake(flavor: "Red Velvet")
switch customerOrder {
  case let .cake(flavor):
    print("你点了一份 \(flavor) 蛋糕")
  case .brownie:
    print("你点了一份巧克力蛋糕") // 原文为 chocolate cake，但 case 是 brownie
  // 应该补充 default 或其他 case
}
// 打印: "你点了一份 red velvet 蛋糕"
```

### CaseIterable

```swift
enum Season: CaseIterable {
  case winter
  case spring
  case summer
  case falls // 通常是 fall 或 autumn
}

for season in Season.allCases {
  print(season)
}
```

添加对 `CaseIterable` 协议的一致性以访问 `allCases` 属性，该属性返回枚举所有情况的数组

### 原始值

```swift
enum Beatle: String {
  case john, paul, george, ringo // 原文格式有误，应为逗号分隔或单独 case
}

print("披头士乐队是 \(Beatle.john.rawValue).")
// 打印: 披头士乐队是 john.
```

###关联值

```swift
enum Dessert {
  case cake(flavor: String)
  case vanillaIceCream(scoops: Int)
  case brownie
}

let order: Dessert = .cake(flavor: "Red Velvet")
```

### 实例方法 {.row-span-2}

```swift
enum Traffic {
  case light
  case heavy

  mutating func reportAccident() {
    self = .heavy
  }
}

var currentTraffic: Traffic = .light

currentTraffic.reportAccident()
// currentTraffic 现在是 .heavy
```

就像类和结构体一样，枚举可以有实例方法。如果实例方法改变了枚举的值，则需要标记为 `mutating`

### 从原始值初始化

```swift
enum Hello: String {
  case english = "Hello"
  case japanese = "こんにちは" // 原文为 "Hello!"，应为日文
  case emoji = "👋"
}
let hello1 = Hello(rawValue: "こんにちは")
let hello2 = Hello(rawValue: "Привет")
print(hello1) // Optional(Hello.japanese)
print(hello2) // nil
```

### 计算属性

```swift
enum ShirtSize: String {
  case small = "S"
  case medium = "M"
  case large = "L"
  case extraLarge = "XL"
  var description: String {
    return "这件衬衫的尺码是 \(self.rawValue)"
  }
}
```

## 扩展

### 什么是扩展？

扩展是一种向现有类、结构体、枚举或协议类型添加新功能的方法。这包括添加新方法、属性、初始化器等。

### 为什么使用扩展？

扩展对于组织和模块化我们的代码特别有用，而无需修改原始类型，尤其是在我们无法访问原始源代码时。

### 扩展语法

```swift
extension SomeType {
    // 要添加的新功能
}
```

### 计算属性

```swift
extension Int {
    var isEven: Bool {
        self % 2 == 0
    }
}

print(4.isEven) // 输出: true
print(7.isEven) // 输出: false
```

### 方法

```swift
extension String {
    func reverse() -> String {
        String(self.reversed())
    }
}

print("abc".reverse()) // 输出: cba
```

### 异变方法

```swift
extension Int {
    mutating func square() {
        self = self * self
    }
}

var number = 5
number.square()
print(number) // 输出: 25
```

### 初始化器

```swift
extension Date {
    init?(timestamp: Double) {
        self.init(timeIntervalSince1970: timestamp)
    }
}

let timestamp = 1693982400.0 // 2023-09-06 06:40:00 的 Unix 时间戳
if let date = Date(timestamp: timestamp) {
    print(date) // 输出: 2023-09-06 06:40:00 +0000
}
```

### 下标

```swift
extension String {
    subscript(index: Int) -> Character {
        self[self.index(startIndex, offsetBy: index)]
    }
}

print("Swift"[0]) // 输出: S
print("Swift"[1]) // 输出: w
print("Swift"[2]) // 输出: i
print("Swift"[3]) // 输出: f
print("Swift"[4]) // 输出: t
```

### 协议扩展 {.row-span-2}

当涉及到我们希望在实现某个协议的所有类中都可用的功能时（无需从公共基类继承），它的工作方式非常类似于抽象类。

```swift
// 定义一个协议
protocol Describable {
    func describe() -> String
}

// 使用协议扩展提供默认实现
extension Describable {
    func describe() -> String {
        "这是一个通用描述"
    }
}

// 定义一个遵循 Describable 协议的结构体
struct Person: Describable {
    var name: String
    var age: Int

    // 覆盖默认实现
    func describe() -> String {
        "我的名字是 \(name)，我 \(age) 岁了。"
    }
}

struct Employee: Describable {
    var name: String
    var age: Int

    // 使用默认实现
}

// 只需实现协议，describe() 方法就可用了

let person = Person(name: "Ivan", age: 21)
let employee = Employee(name: "Saul", age: 25)

print(person.describe()) // 输出: 我的名字是 Ivan，我 21 岁了。
print(employee.describe()) // 输出: 这是一个通用描述
```

### 扩展的约束

当我们想要向符合特定协议或具有某些条件的类型添加功能时，这尤其有用。

```swift
extension Array where Element: Numeric {
    func sum() -> Element {
        reduce(0, +)
    }
}

let numbers = [1, 2, 3, 4, 5]
print(numbers.sum()) // 输出: 15

let doubles = [1.5, 2.5, 3.5]
print(doubles.sum()) // 输出: 7.5

// 这不起作用，因为 String 不是 Numeric
// let strings = ["a", "b", "c"]
// print(strings.sum()) // 错误：字符串数组无法调用 'sum'
```

### 使用扩展组织代码

扩展不仅限于添加功能；它们对于代码组织也很有用。我们可以在单独的扩展中对相关的方法、属性或视图进行分组。

```swift
import SwiftUI

struct HomeView: View {
    var body: some View {
        ScrollView {
            header
            // 添加其他视图
        }
    }
}

extension HomeView {
    private var header: some View {
        Text("页眉 ...")
    }
}

#Preview {
    HomeView()
}
```

## 泛型

### 什么是泛型？

Swift 中的泛型是一项功能，允许我们创建可以与任何数据类型一起工作的函数、类、结构体和协议。

### 为什么使用泛型？

泛型使我们能够编写清晰简洁的代码，该代码可与任何数据类型一起工作。通过使用占位符（如 `T`），这降低了引入错误的风险。

### 类型参数 {.row-span-2}

```swift
func foo<T, U>(a: T, b: U) {
  // ...
}

struct Foo<T, U> {
  var a: T
  // ...
}
```

占位符 `T` 是类型参数的一个示例，写在尖括号内（例如 `<T>`）。

### 泛型数据结构

```swift
struct Box<T> {
    var value: T
}
let intBox = Box(value: 10)
let stringBox = Box(value: "Hello")

print(intBox.value) // 输出: 10
print(stringBox.value) // 输出: "Hello"
```

### 泛型函数 {.row-span-2}

```swift
func swapValues<T>(_ a: inout T, _ b: inout T) {
    let temp = a
    a = b
    b = temp
}

var a = 10
var b = 20
swapValues(&a, &b)
print(a) // 输出: 20
print(b) // 输出: 10

var c = "Hello"
var d = "World"
swapValues(&c, &d)
print(c) // 输出: "World"
print(d) // 输出: "Hello"
```

### 泛型约束

```swift
func sum<T: Numeric>(_ array: [T]) -> T {
    array.reduce(0, +)
}

print(sum([1, 1.5, 2])) // 输出: 4.5

// 这不起作用，因为 String 不是 Numeric
// print(sum(["a", "b", "c"]))
// 错误：函数 'sum' 要求 'String' 符合 'Numeric'
```

### 关联类型

```swift
protocol Foo {
    associatedtype T
    func foo() -> T
}
```

关联类型用于协议中，以定义稍后将指定的类型的占位符。它们充当泛型占位符。确切的类型未在协议本身中定义；相反，它是在类、结构体或枚举符合协议时确定的。

### 泛型协议 {.row-span-2}

```swift
protocol Storage {
    associatedtype Item
    func store(item: Item)
    func retrieve() -> Item?
}

class SimpleStorage<T>: Storage {
    private var items: [T] = []

    func store(item: T) {
        items.append(item)
    }

    func retrieve() -> T? {
        return items.isEmpty ? nil : items.removeLast()
    }
}

let intStorage = SimpleStorage<Int>()
intStorage.store(item: 42)
print(intStorage.retrieve() ?? "Empty")  // 输出: 42
```

### 泛型类型别名

泛型类型别名允许我们为现有类型创建一个新名称（即，它们不会引入新类型）。

```swift
typealias StringDictionary<T> = [String: T]
typealias IntFunction<T> = (Int) -> Int // 这里的 T 似乎未使用，应为 (T) -> T 或 (Int) -> T
typealias Vector<T> = (T, T, T)
```

## 另请参阅

- [Swift 文档 (官方)](https://www.swift.org/documentation/) _(swift.or)_
- [Swift 编程语言 (官方)](https://docs.swift.org/swift-book/) _(swift.or)_
- [Swift 开发者一站式快速参考](https://swiftly.dev/) _(swiftly.dev)_
