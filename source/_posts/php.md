---
title: PHP
date: 2021-01-04 15:23:28
background: bg-[#7477a9]
tags:
  - web
categories:
  - 编程
intro: |
  这份 [PHP](https://www.php.net/manual/zh/) 速查表提供了一个参考，用于快速查找你最常使用的代码的正确语法。
plugins:
  - copyCode
  - runCode
---

## 入门

### hello.php

```php
<?php // 以 PHP 开始标签开始。

echo "你好，世界\n";
print("你好 r3f.cn");

?>
```

PHP 运行命令

```shell script
$ php hello.php
```

### 变量

```php
$boolean1 = true;
$boolean2 = True;

$int = 12;
$float = 3.1415926;
unset($float);  // 删除变量

$str1 = "你好吗？";
$str2 = '很好，谢谢';
```

参见：[PHP 类型](#php-类型)

### 字符串

```php
$url = "r3f.cn";
echo "我正在 $url 学习 PHP";

// 连接字符串
echo "我正在学习 PHP " . $url;

$hello = "你好，";
$hello .= "世界！";
echo $hello;   # => 你好，世界！
```

参见：[PHP 字符串](#php-字符串)

### 数组

```php
$num = [1, 3, 5, 7, 9];
$num[5] = 11;
unset($num[2]);    // 删除变量
print_r($num);     # => 1 3 7 9 11
echo count($num);  # => 5
```

参见：[PHP 数组](#php-数组)

### 运算符

```php
$x = 1;
$y = 2;

$sum = $x + $y;
echo $sum;   # => 3
```

参见：[PHP 运算符](#php-运算符)

### Include {.row-span-3}

#### vars.php

```php
<?php // 以 PHP 开始标签开始。
$fruit = '苹果';
echo "我被导入了";
return '任何你喜欢的内容。';
?>
```

#### test.php

```php
<?php
include 'vars.php';
echo $fruit . "\n";   # => 苹果

/* 与 include 相同，
如果无法包含则会导致错误 */
require 'vars.php';

// 同样有效
include('vars.php');
require('vars.php');

// 通过 HTTP 包含
include 'http://x.com/file.php';

// Include 和 return 语句
$result = include 'vars.php';
echo $result;  # => 任何你喜欢的内容。
?>
```

### 函数

```php
function add($num1, $num2 = 1) {
    return $num1 + $num2;
}
echo add(10);    # => 11
echo add(10, 5); # => 15
```

参见：[PHP 函数](#php-函数)

### 注释

```php
# 这是单行 shell 风格的注释

// 这是单行 c++ 风格的注释

/* 这是多行注释
   这是另一行注释 */
```

### 常量

```php
const MY_CONST = "你好";

echo MY_CONST;   # => 你好

# => MY_CONST 是: 你好
echo 'MY_CONST 是: ' . MY_CONST;
```

### 类

```php
class Student {
    public function __construct($name) {
        $this->name = $name;
    }
}
$alex = new Student("Alex");
```

参见：[PHP 类](#php-类)

## PHP 类型

### 布尔型 {.row-span-2}

```php
$boolean1 = true;
$boolean2 = TRUE;
$boolean3 = false;
$boolean4 = FALSE;

$boolean5 = (boolean) 1;   # => true
$boolean6 = (boolean) 0;   # => false
```

布尔值不区分大小写

### 整型 {.row-span-2}

```php
$int1 = 28;    # => 28
$int2 = -32;   # => -32
$int3 = 012;   # => 10 (八进制)
$int4 = 0x0F;  # => 15 (十六进制)
$int5 = 0b101; # => 5  (二进制)

# => 2000100000 (十进制, PHP 7.4.0)
$int6 = 2_000_100_000;
```

另请参阅：[整数](https://www.php.net/manual/zh/language.types.integer.php)

### 字符串

```php
echo '这是一个简单的字符串';
```

参见：[PHP 字符串](#php-字符串)

### 数组

```php
$arr = array("你好", "世界", "!");
```

参见：[PHP 数组](#php-数组)

### 浮点型 (双精度)

```php
$float1 = 1.234;
$float2 = 1.2e7;
$float3 = 7E-10;

$float4 = 1_234.567;  // PHP 7.4.0 起
var_dump($float4);    // float(1234.567)

$float5 = 1 + "10.5";   # => 11.5
$float6 = 1 + "-1.3e3"; # => -1299
```

### Null

```php
$a = null;
$b = '你好 php！';
echo $a ?? 'a 未设置'; # => a 未设置
echo $b ?? 'b 未设置'; # => 你好 php！

$a = array();
$a == null    # => true
$a === null   # => false
is_null($a)   # => false
```

### 可迭代对象

```php
function bar(): iterable {
    return [1, 2, 3];
}
function gen(): iterable {
    yield 1;
    yield 2;
    yield 3;
}
foreach (bar() as $value) {
    echo $value;   # => 123
}
```

## PHP 字符串

### 字符串

```php
# => '$String'
$sgl_quotes = '$String';

# => '这是一个 $String.'
$dbl_quotes = "这是一个 $sgl_quotes.";

# => a 	 制表符.
$escaped   = "a \t 制表符.";

# => 一个反斜杠和一个 t: \t
$unescaped = '一个反斜杠和一个 t: \t';
```

### 多行

```php
$str = "foo";

// 不进行插值的多行字符串
$nowdoc = <<<'END'
多行字符串
$str
END;

// 将进行字符串插值
$heredoc = <<<END
多行
$str
END;
```

### 操作

```php
$s = "你好 Phper";
echo strlen($s);       # => 11 (注意：中文字符可能占用多个字节)

echo substr($s, 0, 3); # => 你好 (注意：对于多字节字符，行为可能不同)
echo substr($s, 1);    # => 好 Phper (注意：对于多字节字符，行为可能不同)
echo substr($s, -4, 3);# => hpe

echo strtoupper($s);   # => 你好 PHPER
echo strtolower($s);   # => 你好 phper

echo strpos($s, "l");      # => 2
var_dump(strpos($s, "L")); # => false
```

参见：[字符串函数](https://www.php.net/manual/zh/ref.strings.php)

## PHP 数组

### 定义 {.row-span-2}

```php
$a1 = ["你好", "世界", "!"]
$a2 = array("你好", "世界", "!");
$a3 = explode(",", "苹果,梨,桃子");
```

#### 混合整数和字符串键

```php
$array = array(
    "foo" => "bar",
    "bar" => "foo",
    100   => -100,
    -100  => 100,
);
var_dump($array);
```

#### 短数组语法

```php
$array = [
    "foo" => "bar",
    "bar" => "foo",
];
```

### 多维数组

```php
$multiArray = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9],
];

print_r($multiArray[0][0]) # => 1
print_r($multiArray[0][1]) # => 2
print_r($multiArray[0][2]) # => 3
```

### 多类型 {.row-span-2}

```php
$array = array(
    "foo" => "bar",
    42    => 24,
    "multi" => array(
         "dim" => array(
             "a" => "foo"
         )
    )
);

# => string(3) "bar"
var_dump($array["foo"]);

# => int(24)
var_dump($array[42]);

# =>  string(3) "foo"
var_dump($array["multi"]["dim"]["a"]);
```

### 操作

```php
$arr = array(5 => 1, 12 => 2);
$arr[] = 56;      // 追加
$arr["x"] = 42;   // 使用键添加
sort($arr);       // 排序
unset($arr[5]);   // 移除
unset($arr);      // 移除所有
```

参见：[数组函数](https://www.php.net/manual/zh/ref.array.php)

### 索引迭代

```php
$array = array('a', 'b', 'c');
$count = count($array);

for ($i = 0; $i < $count; $i++) {
    echo "i:{$i}, v:{$array[$i]}\n";
}
```

### 值迭代

```php
$colors = array('红色', '蓝色', '绿色');

foreach ($colors as $color) {
    echo "你喜欢 $color 吗？\n";
}
```

### 键迭代

```php
$arr = ["foo" => "bar", "bar" => "foo"];

foreach ( $arr as $key => $value )
{
    echo "键: " . $key . "\n";
    echo "值: {$arr[$key]}\n";
}
```

### 连接数组

```php
$a = [1, 2];
$b = [3, 4];

// PHP 7.4 及更高版本
# => [1, 2, 3, 4]
$result = [...$a, ...$b];
```

### 传入函数

```php
$array = [1, 2];

function foo(int $a, int $b) {
  echo $a; # => 1
    echo $b; # => 2
}
foo(...$array);
```

### 可变参数运算符 (Splat Operator)

```php
function foo($first, ...$other) {
  var_dump($first); # => a
    var_dump($other); # => ['b', 'c']
}
foo('a', 'b', 'c' /*, ...*/ );
// 或者
function foo($first, string ...$other){}
```

## PHP 运算符 {.cols-4}

### 算术运算符

| -    | -      |
| ---- | ------ |
| `+`  | 加法   |
| `-`  | 减法   |
| `*`  | 乘法   |
| `/`  | 除法   |
| `%`  | 取模   |
| `**` | 幂运算 |

### 赋值运算符

| -        | -                   |
| -------- | ------------------- |
| `a += b` | 等同于 `a = a + b` |
| `a -= b` | 等同于 `a = a – b` |
| `a *= b` | 等同于 `a = a * b` |
| `a /= b` | 等同于 `a = a / b` |
| `a %= b` | 等同于 `a = a % b` |

### 比较运算符 {.row-span-2}

| -     | -                            |
| ----- | ---------------------------- |
| `==`  | 等于                         |
| `===` | 全等                         |
| `!=`  | 不等于                       |
| `<>`  | 不等于                       |
| `!==` | 不全等                       |
| `<`   | 小于                         |
| `>`   | 大于                         |
| `<=`  | 小于或等于                   |
| `>=`  | 大于或等于                   |
| `<=>` | 小于/等于/大于（太空船运算符） |

### 逻辑运算符

| -     | -    |
| ----- | ---- | --- | --- |
| `and` | 与   |
| `or`  | 或   |
| `xor` | 异或 |
| `!`   | 非   |
| `&&`  | 与   |
| `     |      | `   | 或   |

### 算术运算 {.col-span-2}

```php
// 算术运算
$sum        = 1 + 1; // 2
$difference = 2 - 1; // 1
$product    = 2 * 2; // 4
$quotient   = 2 / 1; // 2

// 算术简写
$num = 0;
$num += 1;       // $num 加 1
echo $num++;     // 输出 1 (求值后递增)
echo ++$num;     // 输出 3 (求值前递增)
$num /= $float;  // 除法并将商赋值给 $num
```

### 位运算符

| -    | -          | ----------------- |
| ---- | ---------- | ----------------- |
| `&`  | 按位与     |
| `    | `          | 按位或（包含或） |
| `^`  | 按位异或   |
| `~`  | 按位非     |
| `<<` | 左移       |
| `>>` | 右移       |

## PHP 条件语句

### If elseif else

```php
$a = 10;
$b = 20;

if ($a > $b) {
    echo "a 大于 b";
} elseif ($a == $b) {
    echo "a 等于 b";
} else {
    echo "a 小于 b";
}
```

### Switch

```php
$x = 0;
switch ($x) {
    case '0':
        print "它是零";
        break;
    case 'two':
    case 'three':
        // 做些什么
        break;
    default:
        // 做些什么
}
```

### 三元运算符

```php
# => Does
print (false ? 'Not' : 'Does'); // 输出 'Does'

$x = false;
# => Does
print($x ?: 'Does'); // 输出 'Does' (PHP 5.3+ Elvis 运算符)

$a = null;
$b = '打印我';
# => a 未设置
echo $a ?? 'a 未设置'; // 输出 'a 未设置' (PHP 7+ Null 合并运算符)
# => 打印我
echo $b ?? 'b 未设置'; // 输出 '打印我'
```

### Match

```php
$statusCode = 500;
$message = match($statusCode) {
  200, 300 => null,
  400 => '未找到',
  500 => '服务器错误',
  default => '未知状态码',
};
echo $message; # => 服务器错误
```

参见：[Match](https://www.php.net/manual/zh/control-structures.match.php)

### Match 表达式

```php
$age = 23;

$result = match (true) {
    $age >= 65 => '老年人',
    $age >= 25 => '成年人',
    $age >= 18 => '年轻人',
    default => '小孩',
};

echo $result; # => 年轻人
```

## PHP 循环

### while

```php
$i = 1;
# => 12345
while ($i <= 5) {
    echo $i++;
}
```

### do while

```php
$i = 1;
# => 12345
do {
    echo $i++;
} while ($i <= 5);
```

### for i

```php
# => 12345
for ($i = 1; $i <= 5; $i++) {
    echo $i;
}
```

### break

```php
# => 123
for ($i = 1; $i <= 5; $i++) {
    if ($i === 4) {
        break;
    }
    echo $i;
}
```

### continue

```php
# => 1235
for ($i = 1; $i <= 5; $i++) {
    if ($i === 4) {
        continue;
    }
    echo $i;
}
```

### foreach

```php
$a = ['foo' => 1, 'bar' => 2];
# => 12
foreach ($a as $k) {
    echo $k;
}
```

参见：[数组迭代](#php-值迭代)

## PHP 函数

### 返回值

```php
function square($x)
{
    return $x * $x;
}

echo square(4);  # => 16
```

### 返回类型

```php
// 基本返回类型声明
function sum($a, $b): float {/*...*/}
function get_item(): string {/*...*/}

class C {}
// 返回一个对象
function getC(): C { return new C; }
```

### 可空返回类型

```php
// PHP 7.1 可用
function nullOrString(int $v) : ?string
{
    return $v % 2 ? "奇数" : null;
}
echo nullOrString(3);       # => 奇数
var_dump(nullOrString(4));  # => NULL
```

参见：[可空类型](https://www.php.net/manual/zh/migration71.new-features.php#migration71.new-features.nullable-types)

### Void 函数

```php
// PHP 7.1 可用
function voidFunction(): void
{
  echo '你好';
  return;
}

voidFunction();  # => 你好
```

### 可变函数

```php
function bar($arg = '')
{
    echo "在 bar() 中；参数：'$arg'.\n";
}

$func = 'bar';
$func('test'); # => 在 bar() 中；参数：'test'.
```

### 匿名函数

```php
$greet = function($name)
{
    printf("你好 %s\r\n", $name);
};

$greet('世界'); # => 你好 世界
$greet('PHP');   # => 你好 PHP
```

### 递归函数

```php
function recursion($x)
{
    if ($x < 5) {
        echo "$x";
        recursion($x + 1);
    }
}
recursion(1);  # => 1234
```

### 默认参数

```php
function coffee($type = "卡布奇诺")
{
    return "正在制作一杯 $type。\n";
}
# => 正在制作一杯 卡布奇诺。
echo coffee();
# => 正在制作一杯 。
echo coffee(null);
# => 正在制作一杯 浓缩咖啡。
echo coffee("浓缩咖啡");
```

### 箭头函数

```php
$y = 1;

$fn1 = fn($x) => $x + $y;

// 等同于按值使用 $y：
$fn2 = function ($x) use ($y) {
    return $x + $y;
};
echo $fn1(5);   # => 6
echo $fn2(5);   # => 6
```

## PHP 类

### 构造函数

```php
class Student {
    public function __construct($name) {
        $this->name = $name;
    }
    public function print() {
        echo "姓名：" . $this->name;
    }
}
$alex = new Student("Alex");
$alex->print();    # => 姓名：Alex
```

### 继承

```php
class ExtendClass extends SimpleClass
{
    // 重定义父类方法
    function displayVar()
    {
        echo "扩展类\n";
        parent::displayVar();
    }
}

$extended = new ExtendClass();
$extended->displayVar();
```

### 类变量 {.row-span-2}

```php
class MyClass
{
    const MY_CONST       = '值';
    static $staticVar    = '静态';

    // 可见性
    public static $var1  = '公有静态';

    // 仅类内部
    private static $var2 = '私有静态';

    // 类及其子类
    protected static $var3 = '保护静态';

    // 类及其子类
    protected $var6      = '保护';

    // 仅类内部
    private $var7        = '私有';
}
```

静态访问

```php
echo MyClass::MY_CONST;   # => 值
echo MyClass::$staticVar; # => 静态
```

### 魔术方法

```php
class MyClass
{
    // 对象被视为字符串时调用
    public function __toString()
    {
        return $property; // 假设 $property 已定义
    }
    // 与 __construct() 相反，对象销毁时调用
    public function __destruct()
    {
        print "销毁中";
    }
}
```

### 接口

```php
interface Foo
{
    public function doSomething();
}
interface Bar
{
    public function doSomethingElse();
}
class Cls implements Foo, Bar
{
    public function doSomething() {}
    public function doSomethingElse() {}
}
```

## 其他

### 基本错误处理

```php
try {
    // 做些什么
} catch (Exception $e) {
    // 处理异常
} finally {
    echo "总是打印！";
}
```

### PHP 8.0 中的异常 {.col-span-2}

```php {.wrap}
$nullableValue = null;

try {
  $value = $nullableValue ?? throw new InvalidArgumentException();
} catch (InvalidArgumentException) { // 变量是可选的
    // 处理我的异常
    echo "打印我！";
}
```

### 自定义异常 {.row-span-2}

```php
class MyException extends Exception {
    // 做些什么
}
```

用法

```php
try {
    $condition = true;
    if ($condition) {
        throw new MyException('bala');
    }
} catch (MyException $e) {
    // 处理我的异常
}
```

### Nullsafe 运算符 {.row-span-2}

```php
// PHP 8.0.0 起，这行代码：
$result = $repo?->getUser(5)?->name;

// 等同于以下代码：
if (is_null($repo)) {
    $result = null;
} else {
    $user = $repository->getUser(5); // 注意：这里应该是 $repo 而不是 $repository
    if (is_null($user)) {
        $result = null;
    } else {
        $result = $user->name;
    }
}
```

另请参阅：[Nullsafe 运算符](https://wiki.php.net/rfc/nullsafe_operator) (英文)

### 正则表达式

```php
$str = "访问 r3f.cn";
echo preg_match("/ch/i", $str); # => 1
```

参见：[PHP 中的正则表达式](/regex#regex-in-php) (假设链接目标也有中文版)

### fopen() 模式

| -    | -                        |
| ---- | ------------------------ |
| `r`  | 只读                     |
| `r+` | 读写，指针在文件开头     |
| `w`  | 只写，截断文件           |
| `w+` | 读写，截断文件           |
| `a`  | 只写，追加到文件末尾     |
| `a+` | 读写，追加到文件末尾     |

### 运行时定义的常量

```php
define("CURRENT_DATE", date('Y-m-d'));

// 一种可能的表示
echo CURRENT_DATE;   # => 2021-01-05 (日期会变化)

# => CURRENT_DATE 是: 2021-01-05 (日期会变化)
echo 'CURRENT_DATE 是: ' . CURRENT_DATE;
```

## 另请参阅

- [PHP 文档](https://www.php.net/manual/zh/)
- [Y 分钟学习 X](https://learnxinyminutes.com/docs/php/) (通常为英文，但可能有社区翻译)
