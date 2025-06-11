---
title: Dart 语言
date: 2021-11-04 10:12:25
background: bg-[#58aee9]
tags:
  - dart
  - flutter
categories:
  - 编程
intro: |
  一份 Dart 速查表，包含最重要的概念、函数、方法等。为初学者准备的完整快速参考。
plugins:
  - copyCode
---

## 入门 {.cols-2}

### hello.dart

```dart
// 应用执行开始的顶级函数
void main(){
    print("Hello World!"); // 打印到控制台
}
```

每个应用都有一个 main() 函数

### 变量

```dart
int x = 2; // 显式类型
var p = 5; // 类型推断 - 具有类型推断的泛型 var

dynamic z = 8; // 变量可以接受任何类型
z = "cool"; // cool

// 如果你从不打算更改变量，请使用 final 或 const。像这样：

final email = "temid@gmail.com"; // 与 var 相同，但不能重新赋值
final String email = "temid@gmail.com"; // 你不能改变这个值

const qty = 5; // 编译时常量
```

### 数据类型

```dart

int age = 20; // 整数，范围 -2^63 到 2^63 - 1
double height = 1.85; // 浮点数

// 你也可以将变量声明为 num
num x = 1;  // x 可以同时具有 int 和 double 值
x += 2.5;
print(x); //打印: 3.5

String name = "Nicola";

bool isFavourite = true;
bool isLoaded = false;
```

### 字符串插值

```dart
// String 类型可以使用单引号或双引号
var firstName = 'Nicola';
var lastName = "Tesla";

// 可以使用 $ 在字符串中嵌入变量
String fullName = "$firstName $lastName";

// 使用 + 连接
var name = "Albert " + "Einstein";

String upperCase = '${firstName.toUpperCase()}';
print(upperCase); //打印: NICOLA
```

### 注释

```dart
// 这是一个普通的单行注释。

/// 这是一个文档注释，用于记录库、
/// 类及其成员。像 IDE 和 dartdoc 这样的工具
/// 会特殊处理文档注释。

/* 也支持像这样的注释。 */
```
### 多行字符串

```dart
// 对于多行字符串，我们必须使用 ''' 你的文本 '''
// 例如
print('''我的长字符串''');
// 这将显示长字符串
// 这只对长字符串有帮助
```


### 导入

```dart
// 导入核心库
import 'dart:math';

// 从外部包导入库
import 'package:test/test.dart';

// 导入文件
import 'path/to/my_other_file.dart';
```

## 运算符 {.cols-2}

### 算术运算符

```dart
print(2 + 3); //打印: 5
print(2 - 3); //打印: -1
print(2 * 3); //打印: 6
print(5 / 2);  //打印: 2.5 - 结果是 double 类型
print(5 ~/ 2); //打印: 2 - 结果是 int 类型
print(5 % 2); //打印: 1 - 余数

int a = 1, b;
// 递增
b = ++a; // 前缀递增 - 在 b 获取其值之前递增 a。
b = a++; // 后缀递增 - 在 b 获取其值之后递增 a。

//递减
b = --a; // 前缀递减 - 在 b 获取其值之前递减 a。
b = a--; // 后缀递减 - 在 b 获取其值之后递减 a。
```

### 相等和关系运算符

```dart
print(2 == 2);  //打印: true - 相等
print(2 != 3); //打印: true - 不相等
print(3 > 2); //打印: true - 大于
print(2 < 3); //打印: true - 小于
print(3 >= 3); //打印: true - 大于或等于
print(2 <= 3); //打印: true - 小于或等于
```

### 逻辑运算符

```dart
// !expr 反转表达式（将 false 更改为 true，反之亦然）
// ||	逻辑或
// &&	逻辑与
bool isOutOfStock = false;
int quantity = 3;
if (!isOutOfStock && (quantity == 2 || quantity == 3)) {
  // ...订购产品...
}
```

## 控制流：条件语句 {.cols-2}

### if 和 else if

```dart
if(age < 18){
    print("青少年");
} else if( age > 18 && age <60){
    print("成年人");
} else {
    print("老年人");
}
```

### switch case

```dart
enum Pet {dog, cat}
Pet myPet = Pet.dog;
switch(myPet){
    case Pet.dog:
        print('我的宠物是狗。');
        break;
    case Pet.cat:
        print('我的宠物是猫。');
        break;
    default:
        print('我没有宠物。');
}
// 打印: 我的宠物是狗。
```

## 控制流：循环

### while 循环

```dart
while (!dreamsAchieved) {
  workHard();
}
```

while 循环在循环迭代之前检查条件

### do-while 循环

```dart
do {
  workHard();
} while (!dreamsAchieved);
```

do-while 循环在执行循环内的语句后验证条件

### for 循环

```dart
for(int i=0; i< 10; i++){
    print(i);
}

var numbers = [1,2,3];
// 列表的 for-in 循环
for(var number in numbers){
    print(number);
}
```


### for in 循环

```dart
  // 定义一个数字列表
  var numbers = [1, 2, 3, 4, 5];

  // 使用 for-in 循环遍历列表
  for (var number in numbers) {
    print(number);
  }

  // 定义一个字符串列表
  var fruits = ['Apple', 'Banana', 'Cherry'];

  // 使用 for-in 循环遍历列表
  for (var fruit in fruits) {
    print(fruit);
  }
```


## 集合 {.cols-2}

### 列表 (Lists)

```dart
// 对象的有序组
var list = [1, 2, 3];

print(list.length); //打印: 3
print(list[1]); //打印: 2

// 列表声明和初始化的其他方式

List<String> cities = <String>["New York", "Mumbai", "Tokyo"];

// 创建一个编译时常量列表
const constantCities = const ["New York", "Mumbai", "Tokyo"];
```

### 集合 (Sets)

```dart
// Dart 中的集合是唯一项的无序集合。
var halogens = {'fluorine', 'chlorine', 'bromine', 'iodine', 'astatine'};

// 创建一个空集合
var names = <String>{};
Set<String> names = {}; // 这也有效。
//var names = {}; // 创建一个映射，而不是一个集合。
```

### 映射 (Maps)

```dart
// 映射是将键与值关联的对象
var person = Map<String, String>();
// 要初始化映射，请执行以下操作：

person['lastName'] = 'Tesla';

print(person); //打印: {firstName: Nicola, lastName: Tesla}
print(person['lastName']); //打印: Tesla


var nobleGases = {
  // 键: 值
  2: 'helium',
  10: 'neon',
  18: 'argon',
};
```

## 函数 {.cols-2}

### 函数

```dart
// dart 中的函数是对象并且有类型
int add(int a, int b){
    return a+b;
}

// 函数可以赋值给变量
int sum = add(2,3); // 返回: 5

// 可以作为参数传递给其他函数
int totalSum = add(2, add(2,3)); // 返回 : 7
```

### 箭头语法 (=>)

```dart
// 只包含一个表达式的函数，可以使用简写语法
bool isFav(Product product) => favProductsList.contains(product);
```

### 匿名 (lambda) 函数

```dart
// 没有名称的小型单行函数
int add(a,b) => a+b;

// lambda 函数通常作为参数传递给其他函数
const list = ['apples', 'bananas', 'oranges'];
list.forEach(
(item) => print('${list.indexOf(item)}: $item'));
//打印: 0: apples 1: bananas 2: oranges
```

## 类和对象

### 类 (Class)

```dart
class Cat {
    String name;

    // 方法
    void voice(){
        print("Meow");
    }
}
```

### 对象 (Object)

```dart
// 类的实例
// 下面的 myCat 是 Cat 类的对象

void main(){
    Cat myCat = Cat();
    myCat.name = "Kitty";
    myCat.voice(); // 打印: Meow
}
```

### 构造函数 (Constructors)

```dart
class Cat {
    String name;
    Cat(this.name);
}
void main(){
    Cat myCat = Cat("Kitty");
    print(myCat.name); // 打印: Kitty
}
```

### 抽象类 (Abstract Classes)

```dart
// 抽象类——不能被实例化的类
// 这个类被声明为 abstract，因此不能被实例化。
abstract class AbstractContainer {
  // 定义构造函数、字段、方法...

  void updateChildren(); // 抽象方法。
}
```

### Getters 和 Setters

```dart
// 提供对对象属性的读写访问
class Cat {
    String name;

    // getter
    String get catName {
        return name;
    }

    // setter
    void set catName(String name){
        this.name = name;
    }
}
```

## 隐式接口 {.cols-2}

### 一个基本的接口

```dart
// 一个人。隐式接口包含 greet()。
class Person {
  // 在接口中，但仅在此库中可见。
  final String _name;

  // 不在接口中，因为这是一个构造函数。
  Person(this._name);

  // 在接口中。
  String greet(String who) => '你好，$who。我是 $_name。';
}

// Person 接口的一个实现。
class Impostor implements Person {
  String get _name => '';

  String greet(String who) => '嗨，$who。你知道我是谁吗？';
}

String greetBob(Person person) => person.greet('Bob');

void main() {
  print(greetBob(Person('Kathy'))); // 你好，Bob。我是 Kathy。
  print(greetBob(Impostor())); // 嗨 Bob。你知道我是谁吗？
}
```

### 扩展一个类

```dart
class Phone {

    void use(){
        _call();
        _sendMessage();
    }
}
// 使用 extends 创建一个子类
class SmartPhone extends Phone {
    void use(){
        // 使用 super 引用超类
        super.use();
        _takePhotos();
        _playGames();
    }
}
```

## 异常

### Throw

```dart
// 抛出或引发异常
throw IntegerDivisionByZeroException();

// 你也可以抛出任意对象
throw "产品缺货！";
```

### Catch

```dart

try {
    int c = 3/0;
    print(c);
} on IntegerDivisionByZeroException {
    // 一个特定的异常
    print('整数不能除以 0。')
} on Exception catch (e) {
    // 其他任何异常
    print('未知异常: $e');
} catch (e) {
    // 未指定类型，处理所有异常
    print('真正未知的事情: $e');
}

```

### Finally

```dart
// 确保无论是否抛出异常，某些代码都会运行
try {
  cookFood();
} catch (e) {
  print('错误: $e'); // 首先处理异常。
} finally {
  cleanKitchen(); // 然后清理。
}
```

## Futures

### Async Await

```dart
// 异步函数：它们在设置一个可能耗时的操作后返回
// async 和 await 关键字支持异步编程

Future<String> login() {
 String userName="Temidjoy";
 return
  Future.delayed(
    Duration(seconds: 4), () => userName);
}

// 异步
main() async {
 print('正在验证，请稍候...');
 print(await login());
}
```

## 扩展 {.cols-2}

### 为什么要使用扩展？ {.row-span-2}

```dart
// 扩展允许您向现有类添加方法
// 而无需修改它们。

// 而不是定义一个工具类。
class StringUtil {
  static bool isValidEmail(String str) {
    final emailRegExp = RegExp(r"^[a-zA-Z0-9.]+@[a-zA-Z0-9]+\.[a-zA-Z]+");
    return emailRegExp.hasMatch(str);
  }
}

print(StringUtil.isValidEmail('someString')); //打印: false

// 我们可以定义一个将应用于
// 特定类型的扩展。

extension StringExtensions on String {
  bool get isValidEmail {
    final emailRegExp = RegExp(r"^[a-zA-Z0-9.]+@[a-zA-Z0-9]+\.[a-zA-Z]+");
    return emailRegExp.hasMatch(this);
  }
}

print('test@example.com'.isValidEmail); //打印: true
print('SomeString'.isValidEmail); //打印: false

```

### 泛型扩展

```dart
// 允许您将相同的逻辑应用于一系列类型。
extension NumGenericExtensions<T extends num> on T {
  T addTwo() => this + 2 as T;
}

print(7.addTwo()); // 打印: 9
```

### Flutter 中的 Dart 扩展

```dart
extension ContextExtension on BuildContext {
  double get screenHeight => MediaQuery.of(this).size.height;
  double get screenWidth => MediaQuery.of(this).size.width;
}

// 用法
@override
Widget build(BuildContext context) => MaterialApp(
    home: Scaffold(
      body: Container(
        width: context.screenWidth * 0.5,
        height: context.screenHeight * 0.3,
        color: Colors.blue,
        child: Text('Hello World!'),
      ),
    ),
  );
```

## 其他 {.cols-2}

### Null 和空值感知

```dart
int x; // 任何对象的初始值都是 null

// ?? 空值感知运算符

x ??=6; // ??= 赋值运算符，仅当该变量当前为 null 时才为其赋值
print(x); //打印: 6

x ??=3;
print(x); // 打印: 6 - 结果仍然是 6

print(null ?? 10); // 打印: 10. 如果左侧的值不为 null，则显示左侧的值，否则返回右侧的值
```

### 三元运算符

```dart
// 条件 ? 为真时的表达式 : 为假时的表达式
bool isAvailable;

isAvailable ? orderproduct() : addToFavourite();
```

### 扩展运算符 (...)

```dart
// 向集合中插入多个值。
var list = [1, 2, 3];
var list2 = [0, ...list];

print(list2.length); //打印: 4
```

### 级联表示法 (..)

```dart
// 允许您对同一对象执行一系列操作

// 而不是这样做
var user = User();
user.name = "Nicola";
user.email = "nicola@g.c";
user.age = 24;

// 你可以这样做
var user = User()
  ..name = "Nicola"
  ..email = "nicola@g.c"
  ..age = 24;
```

### 条件属性访问

```dart
userObject?.userName

//上面的代码片段等同于以下内容：
(userObject != null) ? userObject.userName : null

//您可以在单个表达式中将多个 ?. 链接在一起
userObject?.userName?.toString()

// 如果 userObject 或 userObject.userName 为 null，则前面的代码返回 null 并且从不调用 toString()
```
### Dart 中的枚举 (enum)
```dart
定义：枚举（enum，"enumeration" 的缩写）是一种特殊的数据类型，它使变量能够成为一组预定义常量。枚举用于定义只能取一小组可能值之一的变量。它们通过为这些值集提供有意义的名称来帮助使代码更具可读性并减少错误。

// 定义枚举
enum TrafficLight {
  red,
  yellow,
  green
}

// 一个根据交通灯状态打印消息的函数
void printTrafficLightMessage(TrafficLight light) {
  switch (light) {
    case TrafficLight.red:
      print('停止！');
      break;
    case TrafficLight.yellow:
      print('准备...');
      break;
    case TrafficLight.green:
      print('通行！');
      break;
  }
}

void main() {
  // 枚举的示例用法
  TrafficLight currentLight = TrafficLight.green;

  // 打印当前交通灯状态的消息
  printTrafficLightMessage(currentLight);
}


```



