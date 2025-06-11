---
title: Perl
date: 2024-05-22 9:03:44
background: bg-[#31719d]
tags:
categories:
  - 编程
intro: |
  Perl 快速参考备忘单，旨在帮助编写基本语法和方法。
plugins:
  - copyCode
  - runCode
---

## 入门

### Unix 和 Linux 安装

- 打开 Web 浏览器并转到 https://www.perl.org/get.html。
- 点击链接下载适用于 Unix/Linux 的压缩源代码。
- 下载 perl-5.x.y.tar.gz 文件并在 $ 提示符下执行以下命令。

```shell
$tar -xzf perl-5.x.y.tar.gz
$cd perl-5.x.y
$./Configure -de
$make
$make test
$make install
```

### Windows 安装

- 点击链接在 Windows 上安装 Strawberry Perl http://strawberryperl.com
- 下载 32 位或 64 位版本的安装程序。
- 在 Windows 资源管理器中双击下载的文件来运行它。这将启动 Perl 安装向导，它非常易于使用。只需接受默认设置，等待安装完成，即可开始使用！

### Macintosh 安装

- 打开 Web 浏览器并转到 https://www.perl.org/get.html。
- 点击链接下载适用于 Mac OS X 的压缩源代码。
- 下载 perl-5.x.y.tar.gz 文件并在 $ 提示符下执行以下命令

```shell
$tar -xzf perl-5.x.y.tar.gz
$cd perl-5.x.y
$./Configure -de
$make
$make test
$make install
```

### 运行 Perl

```shell
# Unix/Linux
$perl  -e <perl 代码>
# Windows/DOS
C:>perl -e <perl 代码>
```

### 可用命令行选项

|    选项     |                         描述 |
| :-----------: | ----------------------------------: |
| -d[:debugger] |         在调试器下运行程序 |
|  -Idirectory  |   指定 @INC/#include 目录 |
|      -T       |           启用污染警告 |
|      -U       |            允许不安全操作 |
|      -w       |        启用许多有用的警告 |
|      -W       |                启用所有警告 |
|      -X       |               禁用所有警告 |
|  -e program   | 作为程序运行 Perl 脚本 |
|     file      |  从给定文件运行 Perl 脚本 |

### 从命令行运行脚本

```shell
# Unix/Linux
$perl  script.pl
# Windows/DOS
C:>perl script.pl
```

### 第一个 Perl 程序

```shell
$perl -e 'print "Hello World\n"'

# #!/usr/bin/perl

# 这将打印 "Hello, World"
print "Hello, world\n";
$chmod 0755 hello.pl
$./hello.pl

```

### Perl 中的注释

```perl
# 这是 Perl 中的注释
=begin comment
这都是多行注释的一部分。
你可以使用任意多行。
这些注释将被编译器忽略，
直到遇到下一个 =cut。
=cut

```

### Perl 中的空白

```perl
#!/usr/bin/perl

# 这将在中间打印一个换行符
print "Hello
          world\n";
#输出
#Hello
#         world

```

### Perl 中的单引号和双引号

```perl
#!/usr/bin/perl

print "Hello, world\n";
print 'Hello, world\n';

#Hello, world
#Hello, world\n$
```

## 数据类型

### 创建变量

```perl
$age = 25;             # 整数赋值
$name = "John Paul";   # 字符串
$salary = 1445.50;     # 浮点数
```

### 标量变量

```perl
#!/usr/bin/perl

$age = 25;             # 整数赋值
$name = "John Paul";   # 字符串
$salary = 1445.50;     # 浮点数

print "Age = $age\n";
print "Name = $name\n";
print "Salary = $salary\n";
```

### 数组变量

```perl
#!/usr/bin/perl

@ages = (25, 30, 40);
@names = ("John Paul", "Lisa", "Kumar");

print "\$ages[0] = $ages[0]\n";
print "\$ages[1] = $ages[1]\n";
print "\$ages[2] = $ages[2]\n";
print "\$names[0] = $names[0]\n";
print "\$names[1] = $names[1]\n";
print "\$names[2] = $names[2]\n";
```

### 哈希变量

```perl
#!/usr/bin/perl

%data = ('John Paul', 45, 'Lisa', 30, 'Kumar', 40);

print "\$data{'John Paul'} = $data{'John Paul'}\n";
print "\$data{'Lisa'} = $data{'Lisa'}\n";
print "\$data{'Kumar'} = $data{'Kumar'}\n";
```

### 变量上下文

```perl
#!/usr/bin/perl

@names = ('John Paul', 'Lisa', 'Kumar');

@copy = @names;
$size = @names;

print "Given names are : @copy\n";
print "Number of names are : $size\n";
```

### 数字标量

```perl
#!/usr/bin/perl

$integer = 200;
$negative = -300;
$floating = 200.340;
$bigfloat = -1.2E-23;

# 377 八进制, 等同于十进制 255
$octal = 0377;

# FF 十六进制, 也等同于十进制 255
$hexa = 0xff;

print "integer = $integer\n";
print "negative = $negative\n";
print "floating = $floating\n";
print "bigfloat = $bigfloat\n";
print "octal = $octal\n";
print "hexa = $hexa\n";
```

### 字符串标量

```perl
#!/usr/bin/perl

$var = "This is string scalar!";
$quote = 'I m inside single quote - $var';
$double = "This is inside single quote - $var";

$escape = "This example of escape -\tHello, World!";

print "var = $var\n";
print "quote = $quote\n";
print "double = $double\n";
print "escape = $escape\n";
```

### 标量操作

```perl
#!/usr/bin/perl

$str = "hello" . "world";       # 连接字符串。
$num = 5 + 10;                  # 两个数字相加。
$mul = 4 * 5;                   # 两个数字相乘。
$mix = $str . $num;             # 连接字符串和数字。

print "str = $str\n";
print "num = $num\n";
print "mul = $mul\n";
print "mix = $mix\n";
```

### 多行字符串

```perl
#!/usr/bin/perl

$string = 'This is
a multiline
string';

print "$string\n";

##########################
print <<EOF;
This is
a multiline
string
EOF
```

### V-字符串

```perl
#!/usr/bin/perl

$smile  = v9786;
$foo    = v102.111.111;
$martin = v77.97.114.116.105.110;

print "smile = $smile\n";
print "foo = $foo\n";
print "martin = $martin\n";
```

### 特殊字面量

```perl
#!/usr/bin/perl

print "File name ". __FILE__ . "\n";
print "Line Number " . __LINE__ ."\n";
print "Package " . __PACKAGE__ ."\n";

# 它们不能被内插
print "__FILE__ __LINE__ __PACKAGE__\n";
```

### 序列号数组

```perl
#!/usr/bin/perl

@var_10 = (1..10);
@var_20 = (10..20);
@var_abc = (a..z);

print "@var_10\n";   # 打印从 1 到 10 的数字
print "@var_20\n";   # 打印从 10 到 20 的数字
print "@var_abc\n";  # 打印从 a 到 z 的字母
```

### 数组大小

```perl
#!/usr/bin/perl

@array = (1,2,3);
$array[50] = 4;

$size = @array;
$max_index = $#array;

print "Size:  $size\n";
print "Max Index: $max_index\n";
```

## 数组操作

### 在数组中添加和删除元素

| 类型                |                                                  描述                                                  |
| :------------------- | :-----------------------------------------------------------------------------------------------------------: |
| push @ARRAY, LIST    |                           将列表的值推入数组的末尾。                            |
| pop @ARRAY           |                               弹出并返回数组的最后一个值。                               |
| shift @ARRAY         | 将数组的第一个值移出并返回，使数组长度减 1 并将所有元素下移。 |
| unshift @ARRAY, LIST |         将列表前置到数组的开头，并返回新数组中的元素数量。         |

### 数组操作

```perl
#!/usr/bin/perl

# 创建一个简单数组

@coins = ("Quarter","Dime","Nickel");
print "1. \@coins = @coins\n";

# 在数组末尾添加一个元素

push(@coins, "Penny");
print "2. \@coins = @coins\n";

# 在数组开头添加一个元素

unshift(@coins, "Dollar");
print "3. \@coins = @coins\n";

# 从数组末尾删除一个元素。

pop(@coins);
print "4. \@coins = @coins\n";

# 从数组开头删除一个元素。

shift(@coins);
print "5. \@coins = @coins\n";

```

### 切片数组元素

```perl
#!/usr/bin/perl

@days = qw/Mon Tue Wed Thu Fri Sat Sun/;

@weekdays = @days[3,4,5];

print "@weekdays\n";
```

### 替换数组元素

```perl
#!/usr/bin/perl

@nums = (1..20);
print "Before - @nums\n";

splice(@nums, 5, 5, 21..25);
print "After - @nums\n";
```

### 将字符串转换为数组

```perl
#!/usr/bin/perl

# 定义字符串

$var_string = "Rain-Drops-On-Roses-And-Whiskers-On-Kittens";
$var_names = "Larry,David,Roger,Ken,Michael,Tom";

# 将上述字符串转换为数组。

@string = split('-', $var_string);
@names = split(',', $var_names);

print "$string[3]\n";  # 这将打印 Roses
print "$names[4]\n"; # 这将打印 Michael
```

### 将数组转换为字符串

```perl
#!/usr/bin/perl

# 定义字符串
$var_string = "Rain-Drops-On-Roses-And-Whiskers-On-Kittens";
$var_names = "Larry,David,Roger,Ken,Michael,Tom";

# 将上述字符串转换为数组。
@string = split('-', $var_string);
@names  = split(',', $var_names);

$string1 = join( '-', @string );
$string2 = join( ',', @names );

print "$string1\n";
print "$string2\n";
```

### 排序数组

```perl
#!/usr/bin/perl

# 定义一个数组
@foods = qw(pizza steak chicken burgers);
print "Before: @foods\n";

# 对此数组进行排序
@foods = sort(@foods);
print "After: @foods\n";
```

### $[ 特殊变量

```perl
#!/usr/bin/perl

# 定义一个数组
@foods = qw(pizza steak chicken burgers);
print "Foods: @foods\n";

# 重置所有数组的第一个索引。
$[ = 1;

print "Food at \@foods[1]: $foods[1]\n";
print "Food at \@foods[2]: $foods[2]\n";
```

### 合并数组

```perl
#!/usr/bin/perl

@odd = (1,3,5);
@even = (2, 4, 6);

@numbers = (@odd, @even);

print "numbers = @numbers\n";
```

### 从列表中选择元素

```perl
#!/usr/bin/perl

@list = (5,4,3,2,1)[1..3];

print "Value of list = @list\n";
```

### 访问哈希元素

```perl
#!/usr/bin/perl

%data = ('John Paul' => 45, 'Lisa' => 30, 'Kumar' => 40);

print "$data{'John Paul'}\n";
print "$data{'Lisa'}\n";
print "$data{'Kumar'}\n";
```

### 提取切片

```perl
#!/uer/bin/perl


%data = (-JohnPaul => 45, -Lisa => 30, -Kumar => 40);

@array = @data{-JohnPaul, -Lisa};

print "Array : @array\n";
```

### 提取键和值

```perl
#!/usr/bin/perl

%data = ('John Paul' => 45, 'Lisa' => 30, 'Kumar' => 40);

@names = keys %data;

print "$names[0]\n";
print "$names[1]\n";
print "$names[2]\n";
```

### 获取哈希大小

```perl
#!/usr/bin/perl

%data = ('John Paul' => 45, 'Lisa' => 30, 'Kumar' => 40);

@keys = keys %data;
$size = @keys;
print "1 - Hash size:  is $size\n";

@values = values %data;
$size = @values;
print "2 - Hash size:  is $size\n";
```

### 在哈希中添加和删除元素

```perl
#!/usr/bin/perl

%data = ('John Paul' => 45, 'Lisa' => 30, 'Kumar' => 40);
@keys = keys %data;
$size = @keys;
print "1 - Hash size:  is $size\n";

# 向哈希添加一个元素；
$data{'Ali'} = 55;
@keys = keys %data;
$size = @keys;
print "2 - Hash size:  is $size\n";

# 从哈希中删除相同的元素；
delete $data{'Ali'};
@keys = keys %data;
$size = @keys;
print "3 - Hash size:  is $size\n";
```

## 控制流

### if-else

```perl
#!/usr/bin/perl

# Perl 程序演示
# 决策语句

$a = 10;
$b = 15;

# if 条件检查
# 是否为偶数
if($a % 2 == 0 )
{
  printf "Even Number";
}

# if-else 条件检查
# 是否为偶数或奇数
if($b % 2 == 0 )
{
  printf "\nEven Number";
}
else
{
  printf "\nOdd Number";
}
```

### ? : 运算符

```perl
#!/usr/local/bin/perl

$name = "Ali";
$age = 10;

$status = ($age > 60 )? "A senior citizen" : "Not a senior citizen";

print "$name is  - $status\n";
```

### for 循环

```perl
#!/usr/bin/perl

# Perl 程序演示
# for 循环的用法

# for 循环
print("For Loop:\n");
for ($count = 1 ; $count <= 3 ; $count++)
{
  print "GeeksForGeeks\n"
}
```

### foreach 循环

```perl
#!/usr/bin/perl

# Perl 程序演示
# foreach 循环的用法

# 数组
@data = ('GEEKS', 4, 'GEEKS');

# foreach 循环
print("For-each Loop:\n");
foreach $word (@data)
{
  print ("$word ");
}

```

### while 和 do-while

```perl
#!/usr/bin/perl

# Perl 程序演示
# foreach 循环的用法

# while 循环
$count = 3;

print("While Loop:\n");
while ($count >= 0)
{
  $count = $count - 1;
  print "GeeksForGeeks\n";
}

print("\ndo...while Loop:\n");
$a = 10;

# do..While 循环
do {

  print "$a ";
  $a = $a - 1;
} while ($a > 0);

```

## 面向对象编程

### 类和对象

```perl
#!/usr/bin/perl

# Perl 程序创建
# 类及其对象
use strict;
use warnings;

package student;

# 构造函数
sub student_data
{

  # shift 将获取包名 'student'
  # 并将其分配给变量 'class'
  my $class_name = shift;
  my $self = {
        'StudentFirstName' => shift,
        'StudentLastName' => shift
      };
  # 使用 bless 函数
  bless $self, $class_name;

  # 从构造函数返回对象
  return $self;
}

# 创建对象并调用构造函数
my $Data = student_data student("Geeks", "forGeeks");

# 打印数据
print "$Data->{'StudentFirstName'}\n";
print "$Data->{'StudentLastName'}\n";

```

### 子程序

```perl
#!/usr/bin/perl

# Perl 程序演示
# 子程序的声明和调用

# 定义子程序
sub ask_user
{
  print "Hello Geeks!\n";
}

# 调用子程序
# 你也可以使用
# &ask_user();
ask_user();
```

### 模块和包

```perl
#!/usr/bin/perl

# 使用包 'Calculator'
use Calculator;

print "Enter two numbers to multiply";

# 为变量定义值
$a = 5;
$b = 10;

# 子程序调用
Calculator::multiplication($a, $b);

print "\nEnter two numbers to divide";

# 为变量定义值
$a = 45;
$b = 5;

# 子程序调用
Calculator::division($a, $b);
```

### 引用

```perl
# Perl 程序演示
# 数组的引用和解引用

# 定义一个数组
@array = ('1', '2', '3');

# 创建对数组变量的引用
$reference_array = \@array;

# 解引用
# 打印存储在
# $reference_array 中的值，
# 前缀 @ 表示它是一个数组引用
print @$reference_array;
```

### 正则表达式

```perl
# Perl 程序演示
# m// 和 =~ 运算符

# 实际字符串
$a = "GEEKSFORGEEKS";

# 如果在 $a 中找到匹配项，则打印 Match Found
if ($a =~ m[GEEKS])
{
  print "Match Found\n";
}

# 如果在 $a 中未找到匹配项，则打印 Match Not Found
else
{
  print "Match Not Found\n";
}
```

### 文件处理

```perl
# 打开文件
open(fh, "GFG2.txt") or die "File '$filename' can't be opened";

# 从文件中读取第一行
$firstline = <fh>;
print "$firstline\n";
```

### 文件测试运算符

```perl
#!/usr/bin/perl

# 使用预定义模块
use warnings;
use strict;

# 将文件路径提供给变量
my $filename = 'C:\Users\GeeksForGeeks\GFG.txt';

# 检查文件是否存在
if(-e $filename)
{

  # 如果文件存在
  print("File $filename exists\n");
}

else
{

  # 如果文件不存在
  print("File $filename does not exists\n");
}
```

### 使用 Excel 文件

```perl
#!/usr/bin/perl
use Excel::Writer::XLSX;

my $Excelbook = Excel::Writer::XLSX->new( 'GFG_Sample.xlsx' );
my $Excelsheet = $Excelbook->add_worksheet();

$Excelsheet->write( "A1", "Hello!" );
$Excelsheet->write( "A2", "GeeksForGeeks" );
$Excelsheet->write( "B1", "Next_Column" );

$Excelbook->close;
```

### 从 Excel 文件读取：

```perl
use 5.016;
use Spreadsheet::Read qw(ReadData);
my $book_data = ReadData (‘new_excel.xlsx');
say 'A2: ' . $book_data->[1]{A2};

```

### 错误处理

```perl
if(open(DATA, $file)) {
   ...
} else {
   die "Error: Couldn't open the file - $!"
}
#示例
open(DATA, $file) || die "Error: Couldn't open the file $!";
## 示例
unless(chdir("/etc")) {
   die "Error: Can't change directory - $!";
}
##示例
print(exists($hash{value}) ? 'There' : 'Missing',"\n");

```

### warn 函数

```perl
chdir('/etc') or warn "Can't change directory";


```

### die 函数

```perl
chdir('/etc') or die "Can't change directory";

```

### 模块内的错误

```perl
package T;

require Exporter;
@ISA = qw/Exporter/;
@EXPORT = qw/function/;
use Carp;

sub function {
   warn "Error in module!";
}
1;
#use T;
#function();
# 以下所有代码都调用该函数

```

### carp 函数

```perl
package T;

require Exporter;
@ISA = qw/Exporter/;
@EXPORT = qw/function/;
use Carp;

sub function {
   carp "Error in module!";
}
1;

```

### cluck 函数

```perl
package T;

require Exporter;
@ISA = qw/Exporter/;
@EXPORT = qw/function/;
use Carp qw(cluck);

sub function {
   cluck "Error in module!";
}
1;

```

### croak 函数

```perl
package T;

require Exporter;
@ISA = qw/Exporter/;
@EXPORT = qw/function/;
use Carp;

sub function {
   croak "Error in module!";
}
1;

```

### confess 函数

```perl
package T;

require Exporter;
@ISA = qw/Exporter/;
@EXPORT = qw/function/;
use Carp;

sub function {
   confess "Error in module!";
}
1;
```

## 日期和时间

### 当前日期和时间

```perl
#!/usr/local/bin/perl

@months = qw( Jan Feb Mar Apr May Jun Jul Aug Sep Oct Nov Dec );
@days = qw(Sun Mon Tue Wed Thu Fri Sat Sun);

($sec,$min,$hour,$mday,$mon,$year,$wday,$yday,$isdst) = localtime();
print "$mday $months[$mon] $days[$wday]\n";
#或
#!/usr/local/bin/perl

$datestring = localtime();
print "Local date and time $datestring\n";
```

### GMT 时间

```perl
#!/usr/local/bin/perl

$datestring = gmtime();
print "GMT date and time $datestring\n";
```

### 格式化日期和时间

```perl
#!/usr/local/bin/perl

($sec,$min,$hour,$mday,$mon,$year,$wday,$yday,$isdst) = localtime();

printf("Time Format - HH:MM:SS\n");
printf("%02d:%02d:%02d", $hour, $min, $sec);
```

### Epoch 时间

```perl
#!/usr/local/bin/perl

$epoc = time();

print "Number of seconds since Jan 1, 1970 - $epoc\n";
#或
#!/usr/local/bin/perl

$datestring = localtime();
print "Current date and time $datestring\n";

$epoc = time();
$epoc = $epoc - 24 * 60 * 60;   # 当前日期前一天。

$datestring = localtime($epoc);
print "Yesterday's date and time $datestring\n";
```

### POSIX 函数 strftime()

| 说明符 | 替换为                                                                                                    |         示例          |
| :-------- | :------------------------------------------------------------------------------------------------------------- | :----------------------: |
| %a        | 缩写的星期几名称                                                                                       |           Thu            |
| %A        | 完整的星期几名称                                                                                              |         Thursday         |
| %b        | 缩写的月份名称                                                                                         |           Aug            |
| %B        | 完整的月份名称                                                                                                |          August          |
| %c        | 日期和时间表示                                                                                   | Thu Aug 23 14:55:02 2001 |
| %C        | 年份除以 100 并截断为整数 (00-99)                                                           |            20            |
| %d        | 月份中的日期，零填充 (01-31)                                                                          |            23            |
| %D        | 短格式 MM/DD/YY 日期，等同于 %m/%d/%y                                                                    |         08/23/01         |
| %e        | 月份中的日期，空格填充 ( 1-31)                                                                         |            23            |
| %F        | 短格式 YYYY-MM-DD 日期，等同于 %Y-%m-%d                                                                  |        2001-08-23        |
| %g        | 基于周的年份，后两位数字 (00-99)                                                                       |            01            |
| %G        | 基于周的年份                                                                                                |           2001           |
| %h        | 缩写的月份名称 (与 %b 相同)                                                                            |           Aug            |
| %H        | 24 小时格式的小时 (00-23)                                                                                     |            14            |
| %I        | 12 小时格式的小时 (01-12)                                                                                     |            02            |
| %j        | 年份中的第几天 (001-366)                                                                                      |           235            |
| %m        | 月份作为十进制数 (01-12)                                                                              |            08            |
| %M        | 分钟 (00-59)                                                                                                 |            55            |
| %n        | 换行符 ('\n')                                                                                      |
| %p        | AM 或 PM 标志                                                                                           |            PM            |
| %r        | 12 小时制时间                                                                                             |       02:55:02 pm        |
| %R        | 24 小时制 HH:MM 时间，等同于 %H:%M                                                                        |          14:55           |
| %S        | 秒 (00-61)                                                                                                 |            02            |
| %t        | 水平制表符 ('\t')                                                                                |
| %T        | ISO 8601 时间格式 (HH:MM:SS)，等同于 %H:%M:%S                                                        |          14:55           |
| %u        | ISO 8601 星期几，星期一为 1 (1-7)                                                              |            4             |
| %U        | 周数，第一个星期日作为第一周的第一天 (00-53)                                         |            33            |
| %V        | ISO 8601 周数 (00-53)                                                                                   |            34            |
| %w        | 星期几作为十进制数，星期日为 0 (0-6)                                                              |            4             |
| %W        | 周数，第一个星期一作为第一周的第一天 (00-53)                                         |            34            |
| %x        | 日期表示                                                                                            |         08/23/01         |
| %X        | 时间表示                                                                                            |         14:55:02         |
| %y        | 年份，后两位数字 (00-99)                                                                               |            01            |
| %Y        | 年份                                                                                                           |           2001           |
| %z        | ISO 8601 时区与 UTC 的偏移量 (1 分钟 = 1, 1 小时 = 100)如果无法确定时区，则无字符 |           +100           |
| %Z        | 时区名称或缩写 如果无法确定时区，则无字符                                    |           CDT            |
| %%        | 一个 % 符号                                                                                                       |            %             |

```perl
#!/usr/local/bin/perl
use POSIX qw(strftime);

$datestring = strftime "%a %b %e %H:%M:%S %Y", localtime;
printf("date and time - $datestring\n");

# 或对于根据您的区域设置适当格式化的 GMT：
$datestring = strftime "%a %b %e %H:%M:%S %Y", gmtime;
printf("date and time - $datestring\n");
```

