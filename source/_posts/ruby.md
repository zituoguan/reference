---
title: Ruby
date: 2024-04-25 09:50:25
background: bg-red-500
tags:
  - 脚本
  - 解释型
categories:
  - 编程
intro: |
  [Ruby](https://www.ruby-lang.org/) 速查表是 Ruby 编程语言的单页参考表。
plugins:
  - copyCode
  - runCode
---

## 入门

### 安装

```bash
# Debian, Ubuntu
$ sudo apt-get install ruby-full
# Windows
$ winget install RubyInstallerTeam.Ruby
$ brew install ruby # macOS
$ docker run -it --rm ruby:latest # Docker
```

### Gemfile 和 Gemfile.lock 是什么 {.row-span-2}

- [Gemfile](https://bundler.io/v2.3/man/gemfile.5.html) 是 Bundler（也是 gem）的配置文件，其中包含项目的 gem 列表（依赖项）。

```ruby
# 在项目根目录的 Gemfile 中指定 gem
ruby '3.1.2'

source 'https://rubygems.org'
gem 'nokogiri'
gem 'rack', '~>3.0.10'
gem 'rspec', :require => 'spec'
```

安装 Gemfile 中的所有 gem

```bash
$ bundle install
```

解决开发环境 mac 和生产环境 linux 之间 Gemfile.lock 不一致的问题

```bash
bundle lock --add-platform x86_64-linux
```

### 安装特定版本的特定 ruby gem

```bash
$ gem install bundler -v 2.4.20
$ gem install minitest -v 5.22.3
```

### 使用 Bundler 更新 gem

```bash
# 使用 Bundler 更新单个 gem
$ bundle update nokogiri
# 使用 Bundler 更新 Gemfile 中的每个 gem
$ bundle update
```

### 注释 {.row-span-1}

```ruby
# 这是单行注释。
=begin
多行
注释
=end
puts "Hello world!"  # 代码的行内注释
```

### 保留字 {.col-span-1}

| 保留字        | 描述                                                                                                |
| :------------- | :--------------------------------------------------------------------------------------------------------- |
| `__ENCODING__` | 当前文件的脚本编码                                                                                    |
| `__LINE__`     | 此关键字在当前文件中的行号                                                                               |
| `__FILE__`     | 当前文件的路径                                                                                           |
| `BEGIN`        | { } 中包含的代码在程序运行之前运行                                                                      |
| `END`          | { } 中包含的代码在程序结束时运行                                                                        |
| `alias`        | 为现有方法、运算符或全局变量创建别名                                                                      |
| `and`          | 逻辑与运算符                                                                                             |
| `begin`        | 开始一个代码块                                                                                             |
| `break`        | 终止循环                                                                                                 |
| `case`         | 将表达式与匹配的 `when` 子句进行比较，以 <br/> `end` 结尾                                                |
| `class`        | 定义一个类                                                                                               |
| `def`          | 定义一个函数/方法                                                                                         |
| `defined?`     | 检查变量或函数是否存在                                                                                     |
| `do`           | 开始一个代码块，以 <br/> `end` 关键字结尾                                                                 |
| `else`         | 如果前面的条件不满足，则执行以下代码                                                                      |
| `elsif`        | if 表达式的替代条件                                                                                       |
| `end`          | 结束以 `begin`、`class`、`def`、`do`、`if` 等关键字开头的代码块                                          |
| `ensure`       | 始终在代码块的末尾执行                                                                                     |
| `false`        | 逻辑布尔值 false                                                                                         |
| `for`          | 开始一个 `for` 循环                                                                                       |
| `if`           | 如果条件为 `true`，则执行代码块                                                                          |
| `in`           | 与 `for` 循环一起使用                                                                                       |
| `module`       | 定义一个模块                                                                                             |
| `next`         | 跳转到循环条件求值之前的点                                                                                 |
| `nil`          | 表示 null、无效或始终为 false                                                                              |
| `not`          | 逻辑非运算符                                                                                             |
| `or`           | 逻辑或运算符                                                                                             |
| `redo`         | 跳转回循环条件求值                                                                                         |
| `rescue`       | 在引发异常后求值表达式                                                                                     |
| `retry`        | 在 `rescue` 外部调用时重复方法调用，在 `rescue` 内部调用时跳转到代码块的顶部                                  |
| `return`       | 从方法或代码块返回值                                                                                       |
| `self`         | 引用当前对象                                                                                             |
| `super`        | 调用超类中同名的方法                                                                                       |
| `then`         | 用作 `if`、`unless`、`when`、`case`、`rescue` 的分隔符                                                    |
| `true`         | 逻辑布尔值 true                                                                                          |
| `undef`        | 取消定义当前类中的方法/函数                                                                                 |
| `until`        | 执行代码块直到条件为 false                                                                                 |
| `when`         | 在 `case` 语句下开始一个子句                                                                               |
| `while`        | 当条件为 true 时执行代码块                                                                                 |
| `yield`        | 执行传递给方法的代码块                                                                                     |

### 运算符 {.row-span-7}

#### 逻辑运算符

- `and`
- `or`
- `not`
- `&&`
- `||`
- `!`

#### 位运算符

- `&`
- `|`
- `^`
- `~`
- `<<`
- `>>`

#### 算术运算符

- `+`
- `-`
- `*`
- `/`
- `%`
- `**`

#### 比较运算符

- `==`
- `!=`
- `>`
- `<`
- `>=`
- `<=`
- `<=>`
- `===`
- `eql?`
- `equal?`

#### 运算符示例

```bash
# 加法
1 + 1   #=> 2
# 减法
2 - 1   #=> 1
# 乘法
2 * 2   #=> 4
# 除法
10 / 5  #=> 2
17 / 5    #=> 3, 而不是 3.4
17 / 5.0  #=> 3.4
# 幂运算
2 ** 2  #=> 4
3 ** 4  #=> 81
# 模运算 (除法的余数)
8 % 2   #=> 0  (8 / 2 = 4; 没有余数)
10 % 4  #=> 2  (10 / 4 = 2 余 2)
a = 10
b = 20
a == b #=> false
a != b #=> true
a > b #=> false
a < b #=> true
a >= b #=> false
a <= b #=> true

# 比较运算符
a <=> b #=> -1
c = 20
c <=> b #=> 0
c <=> a  #=> 1
# case 语句中 when 子句使用的相等性判断
(1...10) === 5 #=> true
# 如果接收者和参数具有相同的类型和相等的值，则为 True
1.eql?(1.0) #=> false
c = a + b  #=> 30
c += a #=> 40
c -= a #=> 30
c *= a #=> 300
c /= a #=> 30
c %= a #=> 3
c **= a #=> 59049

# Ruby 并行赋值
a = 10
b = 20
c = 30
a, b, c = 10, 20, 30
# Ruby 位运算符
a = 60
b = 13
# & 二进制与运算符，如果位同时存在于两个操作数中，则将该位复制到结果中。
a & b #=> 12
# | 二进制或运算符，如果位存在于任一操作数中，则复制该位。
a | b #=> 61
# ^ 二进制异或运算符，如果位设置在一个操作数中但不在两个操作数中，则复制该位。
a ^ b #=> 49
# ~ 二进制一的补码是一元的，具有“翻转”位的效果。
~a
# << 二进制左移运算符。左操作数的值向左移动右操作数指定的位数。
a << 2
# >> 二进制右移运算符。左操作数的值向右移动右操作数指定的位数。
a >> 2

# Ruby 逻辑运算符
a and b #=> true.
a or b #=> true.
a && b #=> true.
(a || b) #=> true.
!(a && b) #=> false.
not(a && b) #=> false.
# Ruby 三元运算符
# ? :
# 如果条件为 true ? 则值为 X : 否则值为 Y
a == 10 ? puts '正确' : puts '错误'
# Ruby 范围运算符
# .. 创建从起点到终点（含）的范围
1..10 #=> 创建从 1 到 10 的范围（包含 1 和 10）
# ... 创建从起点到终点（不含）的范围
1...10 #=> 创建从 1 到 10 的不包含端点的范围
```

### 运算符优先级表

从高到低，这是 ruby 的优先级表。高优先级操作在低优先级操作之前发生。

- !, ~, 一元 +
- \*\*
- 一元 -
- \*, /, %
- +, -
- <<, >>
- &
- |, ^
- > , >=, <, <=
- <=>, ==, ===, !=, =~, !~
- &&
- ||
- .., ...
- ?, :
- 修饰符-rescue
- =, +=, -=, 等.
- defined?
- not
- or, and
- 修饰符-if, 修饰符-unless, 修饰符-while, 修饰符-until
- { } 块

### 变量和作用域 {.col-span-2}

| -              | -                 | -                             | -                                                                                                |
| -------------- | ----------------- | ----------------------------- | :----------------------------------------------------------------------------------------------- |
| 名称           | 作用域             | 示例                       | 解释                                                                                      |
| `[a-z]` 或 `_` | 局部             | `count = 10` 或 `_count = 10` | 局部变量必须初始化                                                              |
| `@`            | 实例变量 | `@id = []`                    | 实例变量在初始化前的值为 "nil"                                      |
| `@@`           | 类变量    | `@@name = []`                 | 类变量必须初始化                                                              |
| `$`            | 全局变量   | `$version = "0.8.9"`          | 全局变量在初始化前的值为 "nil"                                        |
| `[A-Z]`        | 常量          | `PI = 3.14`                   | 常量必须初始化，你可以更改常量，但会收到警告 |

有五种不同类型的变量。第一个字符决定了范围。要深入了解变量，请查看[用户指南](https://ruby-doc.org/docs/ruby-doc-bundle/UsersGuide/rg/)第 19、20、21、22、23 章。
[预定义变量和常量](https://ruby-doc.org/docs/ruby-doc-bundle/Manual/man-1.4/variable.html)

### 检查变量的作用域

```ruby
defined? count
"local-variable"
defined? @id
"instance-variable"
defined? @@name
"class variable"
defined? $version
"global-variable"
defined? PI
"constant"
```

### 数据类型 {.col-span-2}

| -         | -                            | -                                                  | -                                                                                                               |
| :-------- | :--------------------------- | :------------------------------------------------- | :-------------------------------------------------------------------------------------------------------------- |
| 类型      | 示例                      | 类                                              | 文档                                                                                                   |
| `Integer` | a = 17                       | a.class > Integer <br>a.class.superclass > Numeric | [#](<(https://ruby-doc.org/3.3.1/Integer.html)>)                                                                |
| `Float`   | a = 87.23                    | a.class > Float <br>a.class.superclass > Numeric   | [#](https://ruby-doc.org/3.3.1/Float.html)                                                                      |
| `String`  | a = "Hello universe"         | a.class > String                                   | [#](https://ruby-doc.org/3.3.1/String.html)                                                                     |
| `Array`   | a = [12, 34]                 | a.class > Array                                    | [#](https://ruby-doc.org/3.3.1/Array.html)                                                                      |
| `Hash`    | a = {type: "tea", count: 10} | a.class > Hash                                     | [#](https://ruby-doc.org/3.3.1/Hash.html)                                                                       |
| `Boolean` | a = false<br>a = true        | a.class > FalseClass <br>a.class > TrueClass       | [TrueClass](https://ruby-doc.org/3.3.1/TrueClass.html) [FalseClass](https://ruby-doc.org/3.3.1/FalseClass.html) |
| `Symbol`  | a = :status                  | a.class > Symbol                                   | [#](https://ruby-doc.org/3.3.1/Symbol.html)                                                                     |
| `Range`   | a = 1..3                     | a.class > Range                                    | [#](https://ruby-doc.org/3.3.1/Range.html)                                                                      |
| `Nil`     | a = nil                      | a.class > NilClass                                 | [#](https://ruby-doc.org/3.3.1/NilClass.html)                                                                   |

[进一步阅读](https://www.digitalocean.com/community/tutorials/understanding-data-types-in-ruby)

### 检查数据类型

```ruby
# 两者都是同义词
a = 37
a.kind_of? Integer
# true
a.is_a? Integer
# true
```

### 符号 (Symbol)

```ruby
week_days = {sunday: 11, monday: 222}
```

### 整数有用的方法

```ruby
2.even?
# true
3.even?
# false
```

### 范围 (Range)

`..` 用于创建包含性范围

```ruby
range = 1..10
range.to_a
# 输出 => [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```

`...` 用于创建排除性范围

```ruby
range = 1...10
range.to_a
# 输出 => [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

一些有用的方法

| 方法名 | 输出                                |
| :---------- | :------------------------------------ |
| `cover?`    | `(1..5).cover?(5)` => `true`          |
| `end`       | `('a'..'z').end` => `"z"`             |
| `first`     | `(1..5).first` => `1`                 |
| `first(3)`  | `('A'..'Z').first(2)` => `["A", "B"]` |
| `eql?`      | `((0..2).eql?(0..5)` => `false`       |

### 在范围中使用 `step`

```ruby
(1..20).step(2) { |number| puts "#{number}"}
# 输出
# 1
# 3
# 5
# 7
# 9
# 11
# 13
# 15
# 17
# 19
```

## Ruby 流程控制

### if

```ruby
num = 2
puts 'two' if num == 2
```

如果条件为真，则执行代码

### if elsif else

```ruby
temp = 19
if temp >= 25
  puts "热"
elsif temp < 25 && temp >= 18
  puts "正常"
else
  puts "冷"
end
# 输出 => 正常
```

### unless

```ruby
# Unless 与 if 相反，当语句为 false 时求值
name = "rob"
# if name != "bob"
unless name == "bob"
  puts "你好，陌生人"
else
  puts "你好，bob"
end
# 输出 => 你好，陌生人
num = 6
puts '不是二' unless num == 2
# 输出 => 不是二
```

### case {.row-span-2}

```ruby
# case 返回最后执行的表达式的值
case input
# 检查整数 19
when 19
  puts "它是 19"
  # 检查一个确切的字符串，“Zaman”
when "Zaman"
  puts "嗨 Zaman"
when 7..11
  puts "它在 7 和 11 之间"
  # 检查多个值，“coffee”
when "tea", "coffee"
  puts "快乐的日子"
end
```

### case (短语法)

```ruby
case input
  when 19 then puts "它是 19"
end
```

### case (可选失败)

```ruby
case input
  when 19 then puts "它是 19"
else
  puts "它不是 19"
end
```

### case (获取返回值)

```ruby
marks = 86
result = case marks
        when 0..49 then "不及格"
        when 50..64 then "及格"
        when 65..74 then "良好"
        when 75..84 then "优秀"
        when 85..100 then "特优"
        else "无效分数"
        end

puts result
# 特优
```

## 字符串

### 字符串插值

```ruby
name = "World"
puts "Hello #{name}"
puts "总数是 #{1+1}"
# "总数是 2"
```

字符串插值允许您将字符串组合在一起

### 提取子字符串

```ruby
string = "abc123"
string[0,3]
# "abc"
string[3,3]
# "123"
string[0..-2]
# "abc12"
#移除或替换子字符串
string[0..2] = ""
puts string
# "123"
```

子字符串是字符串的一小部分，如果您只需要特定部分（例如开头、中间或结尾），则非常有用。

### 将字符串转换为小写或大写

```ruby
"HELLO World".downcase  # "hello world"
"hello worlD".upcase    # "HELLO WORLD"
"hEllo wOrlD".capitalize # "Hello world"
"hEllo WOrlD".swapcase  # "HeLLO woRLd"
```

### 有用的方法 {.col-span-3}

| 函数名                  | 输出                                                                                                | 注意                                                                                                                                                                                |
| :----------------------------- | :---------------------------------------------------------------------------------------------------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| length 或 size                 | `"HELLO World".length` => `11` <br> `"HELLO World".size` => `11`                                      | 返回字符串的长度                                                                                                                                                    |
| reverse                        | `"hello worlD".reverse` => `"Dlrow olleh"`                                                            | 返回反转后的字符串                                                                                                                                                         |
| include? other_str             | `"hEllo wOrlD".include? "w"` => `true`                                                                | 如果字符串或字符存在则返回 true，否则返回 false                                                                                                             |
| gsub(pattern, replacement)     | `"hEllo wOrlD".gsub(" ", "_")` => `"hEllo_wOrlD"`                                                     | gsub 或全局替换将一个或多个字符串替换为提供的字符串                                                                                                     |
| gsub(pattern, hash)            | `"organization".gsub("z", 'z' => 's')` => `"organisation"`                                            | gsub 或全局替换将一个或多个字符串替换为提供的哈希表                                                                                                       |
| gsub(pattern) {\|match\|block} | `"Price of the phone is 1000 AUD".gsub(/\d+/) {\| s\| '$'+s }`<br>`"Price of the phone is $1000 AUD"` | gsub 或全局替换将一个或多个字符串替换为提供的代码块                                                                                                      |
| strip                          | `" hEllo WOrlD ".strip` <br> `"hEllo WOrlD"`                                                          | 它将删除（修剪）任何前导和尾随字符：null (“\x00”)、水平制表符 (“\t”)、换行符 (\n)、垂直制表符 (“\v”)、换页符 (f)、回车符(\r)、空格 (" ") |
| prepend                        | `a = "world" <br> a.prepend("hello ")` <br> `"hello world"`                                           | 在另一个字符串之前添加字符串                                                                                                                                               |
| insert                         | `a = "hello" <br> a.insert(a.length, " world")` <br> `"hello world"`                                  | 在特定位置插入字符串                                                                                                                                               |
| start_with?                    | `string = "ruby programming"` <br> `string.start_with? "ruby"` <br> `true`                            | 检查字符串是否以特定前缀开头                                                                                                                                  |
| end_with?                      | `string = "ruby programming"` <br> `string.end_with? "ruby"` <br> `false`                             | 检查字符串是否以特定前缀结尾                                                                                                                                  |
| delete_suffix                  | `string = "sausage is expensive"` <br> `string.delete_suffix(" is expensive")` <br> `"sausage"`       | 从字符串中删除后缀                                                                                                                                                  |
| delete_prefix                  | `string = "sausage is expensive"` <br> `string.delete_prefix("sausage")` <br> `" is expensive"`       | 从字符串中删除前缀                                                                                                                                                  |
| split                          | `string = "a b c d" <br> string.split` <br> `["a", "b", "c", "d"]`                                    | 将字符串转换为字符数组                                                                                                                                     |
| join                           | `arr = ['a', 'b', 'c'] <br> arr.join` => `"abc"`                                                      | 将数组转换为字符串                                                                                                                                                     |
| to_i                           | `a = "49" <br> a.to_i` => `49`                                                                        | 将字符串转换为整数                                                                                                                                                 |
| chop                           | `"abcd?".chop("?")` => `"abcd"`                                                                       | 从字符串中删除最后一个字符                                                                                                                                          |
| count                          | `str = "aaab" <br> str.count("a")` <br> `3`                                                           | 计算字符串中的字符数                                                                                                                                               |
| to_f                           | `a = "49"` <br> `a.to_f` <br> `49.0`                                                                  | 将字符串转换为浮点数                                                                                                                                               |
| to_sym                         | `a = "key"` <br> `a.to_sym` <br> `:key`                                                               | 将字符串转换为符号                                                                                                                                                 |
| match                          | `"abcd?".match(/ab/)` => `#<MatchData "ab">`                                                          | 将模式转换为正则表达式并在字符串上调用其 match 方法                                                                                                 |
| empty?                         | `"hello".empty?` => `false`                                                                           | 如果字符串长度为零则返回 true                                                                                                                                    |
| squeeze                        | `"Booook".squeeze` => `"Bok"`                                                                         | 返回字符串的副本，其中相同字符的连续出现被单个字符替换                                                                                                |
| \*                             | `puts "Ruby " * 4` => `Ruby Ruby Ruby Ruby`                                                           | 返回自身多个副本的串联                                                                                                                                |
| +                              | `"sammy " + "shark"` => `"sammyshark"`                                                                | 返回自身和给定其他字符串的串联                                                                                                                            |
| eql?                           | `s = 'foo'` => `true` <br> `s.eql?('foo')` => `true`                                                  | 如果对象具有相同的长度和内容，则返回 true；否则返回 false                                                                                                       |

## 方法

### 声明一个方法 {.row-span-3}

```ruby
def method_name(parameter1, parameter2)
    puts "#{parameter1} #{parameter2}"
    parameter1 + parameter2
end
```

---

```ruby
res = method_name(20, 10)
# 输出 => 30
def method_name(parameter1, parameter2)
    puts "#{parameter1} #{parameter2}"
    return parameter1 + parameter2
end
# 输出 => 30
```

### 调用方法

```ruby
res = method_name(parameter1, parameter2)
# 方法可以不带括号调用
res = method_name parameter1, parameter2
```

### 类方法 {.row-span-4}

类方法是类级别的方法。有多种定义类方法的方式

```ruby
class Mobile
    def self.ring
        "铃铃铃..."
    end
end

Mobile.ring
```

---

```ruby
class Mobile
    def Mobile.ring
        "铃铃铃..."
    end
end
Mobile.ring
```

---

```ruby
class Mobile
    class << self
    def ring
        "铃铃铃..."
       end
    end
end
Mobile.ring
```

类方法是类对象的实例方法。当创建一个新类时，会初始化一个类型为 "Class" 的对象并将其分配给一个全局常量（在本例中为 Mobile）

```ruby
Mobile = Class.new do
    def self.ring
        "铃铃铃..."
    end
end
Mobile.ring
```

```ruby
Mobile = Class.new
class << Mobile
    def ring
        "铃铃铃..."
    end
end
Mobile.ring
```

### 使用另一个参数作为默认值

```ruby
def method_name(num1, num2 = num1)
    return num1 + num2
end
res = method_name(10)
# 输出 => 20
```

### 为方法参数定义默认值

```ruby
def method_name(parameter1, parameter2, type = "ADD")
    puts "#{parameter1} #{parameter2}"
    return parameter1 + parameter2 if type == "ADD"
    return parameter1 - parameter2 if type == "SUB"
end
res = method_name(20, 10)
# 输出 => 30
```

### 将可变长度参数传递给方法参数

```ruby
def method_name(type, *values)
    return values.reduce(:+) if type == "ADD"
    return values.reduce(:-) if type == "SUB"
end
numbers = [2, 2, 2, 3, 3, 3]
res = method_name("ADD", *numbers)
# 输出 => 15
res = method_name("SUB", *numbers)
# 输出 => -11
# 或者你可以像这样提供一个值
res = method_name("ADD", 2, 2, 2, 3, 3, 3)
# 输出 => 15
```

### 修改对象

```ruby
a = ["戏剧", "悬疑", "犯罪",
"科幻", "灾难", "惊悚"]
a.sort
puts a
# 我们没有修改对象
# 戏剧
# 悬疑
# 犯罪
# 科幻
# 灾难
# 惊悚
a.sort!
puts a
# 修改对象
# 犯罪
# 灾难
# 戏剧
# 悬疑
# 科幻
# 惊悚
```

当您想修改对象时，请在方法后使用 `!`

### 布尔方法

在 ruby 中，以问号 (?) 结尾的方法称为布尔方法，它们返回 `true` 或 `false`

```ruby
"some text".nil?
# false
nil.nil?
# true
```

你可以拥有自己的布尔方法

```ruby
def is_vowel?(char)
    ['a','e','i','o','u'].include? char
end
is_vowel? 'a'
# true
is_vowel? 'b'
# false
```

## 代码块

### 代码块示例

```ruby
# 返回值
def give_me_data
    data = yield
    puts "data = #{data}"
end
give_me_data { "大数据" }
# 输出 => data = 大数据
```

`do` 和 `end`（用于多行）或花括号 `{` 和 `}`（用于单行）之间的代码称为代码块，它们可以在两个管道 `( |arg1, arg2|)` 之间定义多个参数。

### 单行代码块

```ruby
salary = [399, 234, 566, 533, 233]
salary.each { |s| puts s }
# puts s = 代码块主体
# |s| = 代码块参数
```

### 多行代码块

```ruby
salary.each do |s|
    a = 10
    res = a * s
    puts res
end
# 代码块
# a = 10
# res = a * s
# puts res
# 代码块参数
# |s|
```

代码块可以作为方法参数传递或与方法调用相关联。代码块返回最后求值的语句。

### 隐式传递代码块

```ruby
def give_me_data
    puts "我在 give_me_data 方法内部"
    yield
    puts "我回到了 give_me_data 方法"
end

give_me_data { puts "大数据" }

# 输出
# 我在 give_me_data 方法内部
# 大数据
# 我回到了 give_me_data 方法
```

### 多次调用

```ruby
def give_me_data
    yield
    yield
    yield
end

give_me_data { puts "大数据" }

# 输出
# 大数据
# 大数据
# 大数据
```

### 使用代码块参数调用

```ruby
def give_me_data
    yield 10
    yield 100
    yield 30
end

give_me_data { |data| puts "大数据 #{data} TB" }

# 输出
# 大数据 10 TB
# 大数据 100 TB
# 大数据 30 TB
```

### 使用多个代码块参数调用

```ruby
def give_me_data
    yield "大数据", 10, "TB"
    yield "大数据", 100, "GB"
    yield "大数据", 30, "MB"
end

give_me_data { |text, data, unit| puts "#{text} #{data} #{unit}" }

# 输出
# 大数据 10 TB
# 大数据 100 GB
# 大数据 30 MB
```

### 代码块将尝试从当前上下文中返回

```ruby
give_me_data
    puts "我在 give_me_data 方法内部"
end

def test
  puts "我在 test 方法内部"
  give_me_data { return 10 } # 代码从这里返回
  puts "我回到了 test 方法"
end

return_value = test

# 输出
# 我在 test 方法内部
# 我在 give_me_data 方法内部
# 10
```

### 使用 & 参数显式传递代码块

```ruby
def give_me_data(&block)
    block.call
    block.call
end

give_me_data { puts "大数据" }

# 输出
# 大数据
# 大数据
```

### 检查是否给定了代码块

```ruby
def give_me_data
    yield
end

give_me_data

# 输出
# LocalJumpError: 没有给出代码块 (yield)
```

### 处理异常并使代码块可选的方法

```ruby
def give_me_data
    return "没有代码块" unless block_given?
    yield
end

give_me_data { puts "大数据" }
give_me_data

# 输出
# 大数据
```

## Procs

### Procs

```ruby
p = Proc.new { puts "Hello World" }

def give_me_data(proc)
    proc.call
end

give_me_data p

# 输出
# Hello World
```

proc 就像一个可以存储在变量中的代码块

### 任意参数 {.col-span-2}

```ruby
p = Proc.new { |count| "Hello World " * count }

def give_me_data(proc)
    proc.call 5, 2
end

give_me_data p

# 输出
# "Hello World Hello World Hello World Hello World Hello World "
```

### proc 将尝试从当前上下文中返回

```ruby
p = Proc.new { return 10 }
p.call
# 输出
LocalJumpError: 意外的返回
```

### 无法从顶层上下文返回

```ruby
def give_me_data
    puts "我在 give_me_data 方法内部"
    p = Proc.new { return 10 }
    p.call # 代码从这里返回
    puts "我回到了 give_me_data 方法"
end

return_value = give_me_data
puts return_value

# 输出
# 我在 give_me_data 方法内部
# 10
```

## Lambdas

### 声明一个 lambda {.row-span-2}

```ruby
l = lambda { puts "Hello World" }
# 简写
l = -> { puts "Hello World" }
# 调用 lambda
l.call
# 输出 => Hello World
```

有多种调用 lambda 的方法

```ruby
l.()
l[]
```

### 严格参数

```ruby
l = -> (count) { "Hello World " * count }
l.call 5
# 输出
# "Hello World Hello World Hello World Hello World Hello World "
l.call 5, 2
# 输出
参数数量错误 (给出 2, 期望 1)
```

### 在代码块中声明 lambda {.row-span-2}

```ruby
def give_me_data
    puts "我在 give_me_data 方法内部"
    l = -> { return 10 }
    l.call
    puts "我回到了 give_me_data 方法"
end

return_value = give_me_data
puts return_value

# 输出
# 我在 give_me_data 方法内部
# 我回到了 give_me_data 方法
# nil # 因为 puts 返回 nil
```

### lambda 从 lambda 本身返回，就像常规方法一样

```ruby
l = -> { return 10 }
l.call

# 输出 => 10
```

## 数组

### 初始化一个空数组

```ruby
array = Array.new   #=> []
# 或
array = []
```

### 包含不同类型对象的数组

```ruby
array = [1, "two", 3.0]
#=> [1, "two", 3.0]
```

### 用初始大小和默认对象填充数组 {.row-span-2}

```ruby
numbers = Array.new(3)
#=> [nil, nil, nil]
numbers = Array.new(3, 7)
#=> [7, 7, 7]
numbers = Array.new(3, true)
#=> [true, true, true]
numbers = []
numbers.fill(7, 0..2)   #=> [7, 7, 7]
```

### 不同哈希的数组 {.col-span-2}

```ruby
array_with_hashes = Array.new(2) { {} } #=> [{}, {}]
array_with_hashes[0][:name] = "Bob"
array_with_hashes[0][:id] = 10          #=> [{:name=>"Bob", :id=>10}, {}]
```

### 二维数组

```ruby
temperature_data = [
              ["A908", 38],
              ["A909", 37],
              ["A910", 38],
          ]
temperature_data[0]    #=> ["A908", 38]
temperature_data[0][0] #=> "A908"
temperature_data[0][1] #=> 38
```

### 数组索引

```ruby
str_array = [
  "This", "is", "a", "small", "array"
]
str_array[0]            #=> "This"
str_array[1]            #=> "is"
str_array[4]            #=> "array"
```

### 负数索引

```ruby
str_array = [
  "This", "is", "a", "small", "array"
]
# 索引 -1 表示最后一个元素
str_array[-1]        #=> "array"
# 索引 -2 表示倒数第二个元素
str_array[-2]        #=> "small"
str_array[-6]        #=> nil
```

### 数组方法 at

```ruby
str_array = [
  "This", "is", "a", "small", "array"
]

puts str_array.at(0)      #=> "This"
```

### 范围获取

```ruby
arr = [1, 2, 3, 4, 5, 6]
arr[100]                  #=> nil
arr[-3]                   #=> 4
arr[2, 3]                 #=> [3, 4, 5]
arr[1..4]                 #=> [2, 3, 4, 5]
arr[1..-3]                #=> [2, 3, 4]
```

### 数组方法 fetch

```ruby
arr = ['a', 'b', 'c', 'd', 'e', 'f']
arr.fetch(100)
#=> IndexError: 索引超出数组范围 100：-6...6
arr.fetch(100, "oops")    #=> "oops"
```

超出范围，给出默认值

### 获取数组元素

```ruby
arr = [1, 2, 3, 4, 5, 6]

arr.first     # 第一个值 => 1
arr.last      # 最后一个值 => 6
# take 返回前 n 个元素
arr.take(3)   #=> [1, 2, 3]
# drop 删除 n 个元素后
arr.drop(3)   #=> [4, 5, 6]
```

### 将值添加到数组末尾 push

```ruby
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
numbers.push(11)
#=> [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11]
numbers.push(12, 13, 14)
#=> [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14]
```

### 删除数组末尾的值 pop

```ruby
num_array = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
num_array.pop             #=> 10
num_array
#=> [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

### 将值添加到数组开头 unshift

```ruby
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
numbers.unshift(0)
#=> [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
numbers.unshift(-3, -2, -1)
#=> [-3, -2, -1, 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```

### 检索并同时删除第一个元素 shift

```ruby
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
numbers.shift #=> 1
numbers
#=> [2, 3, 4, 5, 6, 7, 8, 9, 10]
```

### 删除特定索引处的元素 delete_at

```ruby
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
numbers.delete_at(2) #=> 4
numbers
#=> [2, 3, 5, 6, 7, 8, 9, 10]
```

### 删除数组中任何位置的特定元素

```ruby
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
numbers.delete(2) #=> 2
numbers           #=> [3, 5, 6, 7, 8, 9, 10]
```

### 在给定索引处插入值 insert {.row-span-2}

```ruby
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
numbers.insert(0, 0)
#=> [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
numbers.insert(0, -3, -2, -1)
#=> [-3, -2, -1, 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

numbers.insert(-1, 12, 13, 14)
#=> [-3, -2, -1, 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 12, 13, 14]
numbers.insert(-4, 11)
#=> [-3, -2, -1, 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14]
```

### 用值填充数组的代码块

```ruby
numbers = Array.new(10) { |n| n = n * 2 }
#=> [0, 2, 4, 6, 8, 10, 12, 14, 16, 18]
```

### 填充数组变得更容易

```ruby
numbers = Array(100..110)
#=> [100, 101, 102, 103, 104, 105, 106, 107, 108, 109, 110]

# 或者我们可以将范围转换为数组
(100..110).to_a
#=> [100, 101, 102, 103, 104, 105, 106, 107, 108, 109, 110]
```

### 从数组中删除 nil 值

```ruby
arr = ['foo', 0, nil, 'bar', 7, nil]
arr.compact  #=> ['foo', 0, 'bar', 7]
arr      #=> ['foo', 0, nil, 'bar', 7, nil]
arr.compact! #=> ['foo', 0, 'bar', 7]
arr      #=> ['foo', 0, 'bar', 7]
```

### 删除重复项 uniq

```ruby
arr = [2, 5, 6, 556, 6, 6, 8, 9, 0, 123, 556]
arr.uniq #=> [2, 5, 6, 556, 8, 9, 0, 123]
arr # => [2, 5, 6, 556, 6, 6, 8, 9, 0, 123, 556]
arr.uniq! #=> [2, 5, 6, 556, 8, 9, 0, 123]
arr #=> [2, 5, 6, 556, 8, 9, 0, 123]
```

### 检查数组中是否存在值（`include？`）

```ruby
planets = ["水星", "金星", "地球", "火星", "木星", "土星", "天王星", "海王星"]
planets.include? "火星"
# 输出 => true
planets.include? "冥王星"
# 输出 => false
```

### 获取数组大小

```ruby
planets = ["水星", "金星", "地球", "火星", "木星", "土星", "天王星", "海王星"]
planets.size
# 输出 => 8
planets.length
# 输出 => 8
```

您可以使用 size 或 length，两者都是同义词

### 清空数组

```ruby
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
numbers.clear
# 输出 => []
```

### 获取数组的第一个元素

```ruby
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
numbers[0]
# 或
numbers.first
# 输出 => 1
```

### 获取数组的最后一个元素

```ruby
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
numbers[-1]
# 或
numbers.last
# 输出 => 10
```

### 合并两个数组

```ruby
a = ["tom", "mot", "otm"]
b = [2, 3, 5]
a.zip(b)
# 输出
# [["tom", 2], ["mot", 3], ["otm", 5]]
```

### 排序数组 {.row-span-3}

```ruby
primes = [7, 2, 3, 5]
sorted_primes = primes.sort
puts "#{sorted_primes}"
# 输出 => [2, 3, 5, 7]
```

或就地排序

```ruby
primes = [7, 2, 3, 5]
primes.sort!
puts "#{primes}"
# 输出 => [2, 3, 5, 7]
```

```ruby
planets = ["水星", "金星", "地球", "火星", "木星", "土星", "天王星", "海王星"]
planets.sort
# 输出
# ["地球", "木星", "火星", "水星", "海王星", "土星", "天王星", "金星"]
planets.sort_by { |p| p }
# 输出
# ["地球", "木星", "火星", "水星", "海王星", "土星", "天王星", "金星"]
planets.sort_by { |p| p.length }
# 输出
# ["火星", "地球", "金星", "土星", "天王星", "海王星", "木星", "水星"]
```

### 从数组中获取最大值

```ruby
primes = [7, 2, 3, 5]
primes.max_by { |p| p }
# 输出 => 7
```

### 使用范围获取数组元素 {.row-span-2}

```ruby
# numbers[start..end]，两个索引都包含在内
puts numbers[0..3]
# 1
# 2
# 3
# 4
# numbers[start...end]，结束索引不包含在内
puts numbers[0...3]
# 1
# 2
# 3
# 或 numbers[start, length]
puts numbers[0, 1]
# 1
```

### 获取数组的前 n 个元素

```ruby
primes = [7, 2, 3, 5]
primes.take(3)
# [7, 2, 3]
```

### 访问元素

```ruby
primes = [7, 2, 3, 5]
primes.fetch(3)
# 5
# 如果元素不存在，Fetch 将引发错误
primes.fetch(10)
# (索引 10 超出数组范围：-4...4)
# 或获取默认值
primes.fetch(10, -1)
# -1
```

### 删除前 n 个元素

```ruby
primes = [7, 2, 3, 5]
primes.drop(3)
# [5]
```

### 删除第一个元素

```ruby
primes = [7, 2, 3, 5]
primes.shift
# [2, 3, 5]
```

### 删除最后一个元素

```ruby
primes = [7, 2, 3, 5]
primes.pop
# [7, 2, 3]
```

### 删除带索引的元素

```ruby
primes = [7, 2, 3, 5]
primes.delete_at(-1)
# [7, 2, 3]
```

### 删除所有出现的元素

```ruby
primes = [7, 2, 3, 5, 5]
primes.delete(5)
# [7, 2, 3]
```

### each {.row-span-3}

```ruby
# 当你有单行代码块时
salary = [399, 234, 566, 533, 233]
salary.each { |s| puts s }
# 输出
# 399
# 234
# 566
# 533
# 233
```

当您有多行代码块时，可以用 `do` 和 `end` 替换花括号 `{}`

```ruby
salary.each do |s|
  a = 10
  res = a * s
  puts res
end
# 输出
# 3990
# 2340
# 5660
# 5330
# 2330
```

或者您可以使用花括号 {} 和分号作为分隔符而不是换行符来执行相同的操作

```ruby
salary.each { |s| a = 10 ; res = a * s ; puts res }
```

### each_with_index

```ruby
salary = [399, 234, 566, 533, 233]
salary.each_with_index { |value, index| puts "#{index} #{value}" }
# 输出
# 0 399
# 1 234
# 2 566
# 3 533
# 4 233
```

### each_index

```ruby
salary = [399, 234, 566, 533, 233]
salary.each_index { |i| puts i}
# 输出
# 0
# 1
# 2
# 3
# 4
```

### map

```ruby
salary = [399, 234, 566, 533, 233]
salary.map { |s|  s * 10  }
# 返回
# [3990, 2340, 5660, 5330, 2330]
# 另一方面，each 返回原始值
salary = [399, 234, 566, 533, 233]
salary.each { |s|  s * 10  }
# 返回
# [399, 234, 566, 533, 233]
```

### collect

```ruby
salary = [399, 234, 566, 533, 233]
salary.collect { |s| s > 400 }
# 输出
# [false, false, true, true, false]
```

### for

```ruby
for value in [2, 3, 5, 7]
    puts value
end
```

### each_with_object {.col-span-2}

```ruby
colors = [
  {color: "red", count: 3}, {color: "red", count: 5}, {color: "black", count: 4}
]
colors.each_with_object(Hash.new(0)) { |color, hash| hash["color_"+color[:color]] = color[:color].upcase; hash["count_"+color[:color]] += color[:count] }
# 输出
{"color_red"=>"RED", "count_red"=>8, "color_black"=>"BLACK", "count_black"=>4}

[1, 2, 3].each_with_object(0) { |number, sum| sum += number}
# 输出
# 0
# 因为 0 是不可变的，并且由于初始对象是 0，所以该方法返回 0
```

### while

```ruby
planets = ["水星", "金星", "地球", "火星", "木星", "土星", "天王星", "海王星"]
index = 0
while index < planets.size
    puts "#{planets[index]}"
    index += 1
end
```

---

```ruby
a = 1
star = '*'
while a <= 10
    puts star
    star += '*'
    a += 1
end
```

### do while

```ruby
planets = ["水星", "金星", "地球", "火星", "木星", "土星", "天王星", "海王星"]
index = 0
loop do
    puts "#{planets[index]}"
    index += 1
    break if planets[index] == "火星" or index > planets.size
end
```

### until

```ruby
planets = ["水星", "金星", "地球", "火星", "木星", "土星", "天王星", "海王星"]
index = planets.size - 1
until index < 0
    puts "#{planets[index]}"
    index -= 1
end
```

```ruby
a = 1
star = '*'
until star.length > 10
    puts star
    star += '*'
    a += 1
end
```

### times

```ruby
10.times { puts "#{rand(1..100)}"}
# 输出
# 将打印 10 个随机数
```

仅仅因为你可以，并不意味着你应该像这样迭代数组

```ruby
data_sample = [2, 3, 5, 7]
data_sample.size.times { |index| puts "#{data_sample[index]}" }
# 输出
# 2
# 3
# 5
# 7
```

### upto

```ruby
data_sample = [2, 3, 5, 7]
0.upto((data_sample.size - 1) / 2) { |index| puts "#{data_sample[index]}" }
# 输出
# 2
# 3
```

### downto

```ruby
data_sample = [2, 3, 5, 7]
(data_sample.size - 1).downto(data_sample.size / 2) { |index| puts "#{data_sample[index]}" }
# 输出
# 7
# 5
```

### step {.row-span-2}

```ruby
1.step(20, 2) { |number| puts "#{number}"}
# 输出
# 1
# 3
# 5
# 7
# 9
# 11
# 13
# 15
# 17
# 19
```

---

```ruby
19.step(1, -2) { |number| puts "#{number}"}
# 输出
# 19
# 17
# 15
# 13
# 11
# 9
# 7
# 5
# 3
# 1
```

### inject {.row-span-2}

```ruby
numbers = [2, 2, 2, 2, 2]
numbers.inject{ |res, n| res + n }
# 输出是所有数字的总和
# 如果没有为 res 设置初始值，则数组的第一个元素用作 res 的初始值。
#10
# 现在将 res 的值设置为 11
numbers = [2, 2, 2, 2, 2]
numbers.inject(11) { |res, n| res + n }
# 所以 11 + 2, 13 + 2, 15 + 2, 17 + 2 和 19 + 2
# 21
# 使用符号
numbers = [2, 2, 2, 2, 2]
numbers.inject(:+)
# 输出
# 10
```

使用初始值和符号

```ruby
numbers = [2, 2, 2, 2, 2]
numbers.inject(11, :+)
# 输出
# 21
```

### reduce

```ruby
numbers = [2, 2, 2, 2, 2]
numbers.reduce(11, :+)
# 输出
# 21
```

### detect

```ruby
planets = ["水星", "金星", "地球", "火星", "木星", "土星", "天王星", "海王星"]
planets.detect { |name| name.start_with?("地") and name.end_with?("球") }
# 输出
# 地球
salary = [399, 234, 566, 533, 233]
salary.detect { |s| s > 1000 }
# 输出
# nil
```

### find

```ruby
planets = ["水星", "金星", "地球", "火星", "木星", "土星", "天王星", "海王星"]
planets.find { |name| name.start_with?("地") and name.end_with?("球") }
# 输出
# 地球
```

### select

```ruby
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
numbers.select { |n| n % 2 == 0 }
# 现在你有一个偶数数组
# [2, 4, 6, 8, 10]
# 如果没有满足你逻辑的值，则返回一个空数组
[1, 1, 1].select { |n| n % 2 == 0 }
# 没有偶数
# []
```

### reject

```ruby
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
numbers.reject { |n| n % 2 == 0 }
# 如果数字是偶数则拒绝，所以现在我们有一个奇数数组
# [1, 3, 5, 7, 9]
```

### keep_if

```ruby
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
numbers.keep_if { |n| n % 2 == 0 }
# numbers 数组只包含偶数
# [2, 4, 6, 8, 10]
```

### delete_if

```ruby
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
numbers.delete_if { |n| n % 2 == 0 }
# numbers 数组只包含奇数
# [1, 3, 5, 7, 9]
```

### drop_while

```ruby
numbers = [1, 2, 3, 1, 2, 3, 0]
numbers.drop_while { |n| n < 3 }
# 3 小于 3 吗？返回 false，所以删除 1, 2
# [3, 1, 2, 3, 0]
```

### reverse_each

```ruby
words = %w[第一 第二 第三 第四 第五 第六]
str = ""
words.reverse_each {|word| str += "#{word} "}
p str #=> "第六 第五 第四 第三 第二 第一 "
```

## 布尔可枚举方法

### 布尔可枚举方法 {.row-span-2}

| 名称       | 何时使用                                                              |
| :--------- | :----------------------------------------------------------------------- |
| `all?`     | 当您想检查所有元素是否满足您的条件时               |
| `any?`     | 当您想检查至少有一个项目满足您的条件时         |
| `one?`     | 当您想检查一个元素是否满足您的要求时             |
| `none?`    | 当您想检查没有项目满足您的条件时，与 any? 相反 |
| `empty?`   | 当您想检查对象是否为空时                             |
| `include?` | 当您想检查对象中是否存在元素时                |

### all?

```ruby
[2, 4, 6, 8, 10].all? { |num| num % 2 == 0 }
# true
[1, 4, 6, 8, 10].all? { |num| num % 2 == 0 }
# false
```

### any?

```ruby
[1, 3, 5, 7, 10].any? { |num| num % 2 == 0 }
# true
[1, 3, 5, 7, 19].any? { |num| num % 2 == 0 }
# false
```

### one?

```ruby
[1, 3, 2, 5, 7].one? { |num| num % 2 == 0 }
# true
[1, 3, 2, 5, 4].one? { |num| num % 2 == 0 }
# false
```

### none?

```ruby
[1, 3, 5, 7, 9].none? { |num| num % 2 == 0 }
# true
[2, 3, 5, 7, 9].none? { |num| num % 2 == 0 }
# false
```

### empty?

```ruby
[].empty?
# true
[1, 3, 5, 7, 9].empty?
# false
```

## 组合方法

### 组合方法 {.row-span-2}

- `&` 返回一个新数组，其中包含在 array 和 array other_array 中找到的每个元素；省略重复项；使用 eql? 比较项目
- `intersection` 返回一个新数组，其中包含在 self 和所有给定的 other_arrays 数组中找到的每个元素；省略重复项；使用 eql? 比较项目
- `+` 返回一个数组，其中包含 self 的所有元素，后跟给定数组的所有元素
- `-` 返回一个数组，其中包含 self 中未在给定数组中找到的所有元素
- `union` 返回一个数组，其中包含 self 的所有元素和给定数组的所有元素，并删除重复项
- `difference` 返回一个数组，其中包含 self 中未在任何给定数组中找到的所有元素
- `product` self 返回或生成 self 和给定数组中元素的所有组合

### &

```ruby
[0, 1, 2, 3] & [1, 2] # => [1, 2]
[0, 1, 0, 1] & [0, 1] # => [0, 1]
```

### intersection

```ruby
[0, 1, 2, 3].intersection([0, 1, 2], [0, 1, 3])
# => [0, 1]
[0, 0, 1, 1, 2, 3].intersection([0, 1, 2], [0, 1, 3])
# => [0, 1]
```

### +

```ruby
a = [0, 1] + [2, 3]
a # => [0, 1, 2, 3]
```

### -

```ruby
[0, 1, 1, 2, 1, 1, 3, 1, 1] - [1]
# => [0, 2, 3]
[0, 1, 2, 3] - [3, 0]
# => [1, 2]
[0, 1, 2] - [4]
# => [0, 1, 2]
```

### union

```ruby
[0, 1, 2, 3].union([4, 5], [6, 7])
# => [0, 1, 2, 3, 4, 5, 6, 7]
[0, 1, 1].union([2, 1], [3, 1])
# => [0, 1, 2, 3]
[0, 1, 2, 3].union([3, 2], [1, 0])
# => [0, 1, 2, 3]
```

### difference

```ruby
[0, 1, 1, 2, 1, 1, 3, 1, 1].difference([1])
# => [0, 2, 3]
[0, 1, 2, 3].difference([3, 0], [1, 3])
# => [2]
[0, 1, 2].difference([4])
# => [0, 1, 2]
```

### product

```ruby
a = [0, 1, 2]
a1 = [3, 4]
p = a.product(a1)
p.size # => 6 # a.size * a1.size
p # => [[0, 3], [0, 4], [1, 3], [1, 4], [2, 3], [2, 4]]
```

## 循环

### while 循环

```ruby
# 变量 count
count = 4
# 使用 while 循环
# 这里的条件是 count 即 4
while count >= 1
  # 要执行的语句
  puts "Ruby 速查表"
  count = count - 1
  # while 循环在此结束
end
```

输出

```
Ruby 速查表
Ruby 速查表
Ruby 速查表
Ruby 速查表
```

### for 循环

```ruby
# 使用范围作为表达式的循环
text = "Ruby 速查表"
# 使用 for 循环和范围
for count in 1..5 do
  puts text
end
```

输出

```
Ruby 速查表
Ruby 速查表
Ruby 速查表
Ruby 速查表
Ruby 速查表
```

### do..while 循环

```ruby
# do..while 循环的开始
loop do
  puts "Ruby 速查表"
  val = '7'
  # 使用布尔表达式
  if val == '7'
    break
  end
  # ruby do..while 循环的结束
end
```

输出

```
Ruby 速查表
```

### until 循环

```ruby
var = 7
# 这里的 do 是可选的
until var == 11 do
  # 要执行的代码
  puts var * 10
  var = var + 1
  # 循环在此结束
end
```

输出

```
70
80
90
100
```

### 跳出循环

```ruby
salary = [399, 234, 566, 533, 233]
salary.each do |s|
  break if s == 566
  puts s
end
# 输出
# 399
# 234
```

通过使用 `break` 关键字

### 在循环内跳过

```ruby
salary = [399, 234, 566, 533, 233]
salary.each do |s|
  next if s == 533
  puts s
end
# 输出
# 399
# 234
# 566
# 233
```

通过使用 next 关键字

### 重复当前迭代

```ruby
data = [456, 3000]
retry_count = 0
status = "网络故障"
sum = 0
data.each do |d|
    if retry_count == 3
        status = "连接已建立"
        retry_count = 0
        redo
    elsif status == "网络故障" and retry_count < 5
        puts "网络故障 #{retry_count}"
        retry_count += 1
        redo
    elsif status == "连接已建立"
        puts d
        sum += d
    end
end
# sum 的输出
# 3456
```

### 重新开始循环

```ruby
numbers = [2, 2, 44, 44]
sum = 0
begin
    numbers.each do |s|
        if rand(1..10) == 5
            puts "嗨 5，让我们再来一次！"
            sum = 0
            raise "嗨 5"
        end
        puts s
        sum += s
    end
rescue
    retry
end
```

## 类

### 类示例 {.row-span-2}

```ruby
class Person
    # 当你创建一个新对象时，它会查找一个名为 initialize 的方法并执行它，就像 java 中的构造函数一样
    # def initialize(name, number)
    #    @name = name
    #    @number = number
    # end
    # 实例变量
    # @name
    # 类变量
    # @@count
    # attr_accessor 充当以下实例属性的 getter 和 setter
    attr_accessor :name, :number
    # 类变量必须初始化
    @@count = 0
    def self.count
        @@count
    end
    def self.count=(count)
        @@count = count
    end
    def initialize
        @@count += 1
    end
end
# 创建 Person 类的实例
p1 = Person.new
# 设置 Person 类的属性
p1.name = "松本行弘"
p1.number = 9999999999
# 获取 Person 类的属性
puts "#{p1.name}"
puts "#{p1.number}"
puts "#{Person.count}"
# 松本行弘
# 9999999999
# 1
p2 = Person.new
p2.name = "松本行弘"
p2.number = 9999999999
# 获取 Person 类的属性
puts "#{p2.name}"
puts "#{p2.number}"
puts "#{Person.count}"
# 松本行弘
# 9999999999
# 2
# 设置类变量
Person.count = 3
puts "#{Person.count}"
# 3
```

### 继承一个类

```ruby
class Person
    attr_accessor :name, :number
end
# 使用 < 符号从父类继承方法和属性
class Student < Person
    attr_accessor :id
end
s = Student.new
s.name = "詹姆斯·邦德"
s.number = 700
s.id = 678
puts "#{s.name}" # 更正：应该是 s.name 而不是 p.name
# 詹姆斯·邦德
puts "#{s.number}" # 更正：应该是 s.number 而不是 p.number
# 700
puts "#{s.id}" # 更正：应该是 s.id 而不是 p.id
# 678
```

### 检查实例类型

```ruby
class Vehicle; end
class Car < Vehicle; end
class Audi < Car; end
car = Car.new
car.instance_of? Vehicle
false
car.instance_of? Car
true
car.instance_of? Audi
false
a = 7
a.instance_of? Integer
true
a.instance_of? Numeric
false
```

如果对象是给定类的实例而不是子类或超类，则返回 true

### 打印类的所有方法名

```ruby
puts (String.methods).sort
# 排除从 Object 类继承的方法
puts (String.methods - Object.public_instance_methods).sort
```

### 检查类是否具有特定方法

```ruby
String.respond_to?(:prepend)
true
String.respond_to?(:append)
false
```

## 另请参阅

- [Ruby](https://www.ruby-lang.org/en/) _(ruby-lang.org)_
- [Ruby 速查表](https://github.com/lifeparticle/Ruby-Cheatsheet) _(github.com)_

