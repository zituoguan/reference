---
title: MATLAB
date: 2023-01-03 09:51:44
background: bg-[#692316]
tags:
categories:
  - 编程
intro: |
  此快速参考备忘单提供了一个示例性介绍，介绍如何使用 [MATLAB](https://mathworks.cn/) 科学计算语言快速入门
plugins:
  - copyCode
---

## 入门指南

### 简介

MATLAB 是 `matrix laboratory` (矩阵实验室) 的缩写

---

- [MATLAB 官方网站](https://www.mathworks.com)

### 矩阵和数组运算 {.row-span-3}

MATLAB 允许您使用单个算术运算符或函数来处理矩阵中的所有值

```matlab
a + 10
```

MATLAB 将执行上述语句并返回以下结果：

```
ans = 3×3
    11    13    15
    12    14    16
    17    18    20
```

---

```matlab
sin(a)
```

MATLAB 将执行上述语句并返回以下结果：

```
ans = 3×3
    0.8415    0.1411   -0.9589
    0.9093   -0.7568   -0.2794
    0.6570    0.9894   -0.5440
```

要转置矩阵，请使用单引号 (`'`)

```matlab
a'
```

---

```
ans = 3×3
     1     2     7
     3     4     8
     5     6    10
```

使用 `*` 运算符执行标准矩阵乘法，该运算符计算行和列之间的内积

```matlab
p = a*inv(a)
```

---

```
p = 3×3
    1.0000         0         0
         0    1.0000         0
         0         0    1.0000
```

### 串联 {.row-span-2}

串联是连接数组以形成更大数组的过程。实际上，第一个数组是通过串联其元素形成的。方括号对 `[]` 是串联运算符。

```matlab
A = [a,a]
```

---

```
A = 3×6

     1     3     5     1     3     5
     2     4     6     2     4     6
     7     8    10     7     8    10
```

使用逗号将数组彼此相邻串联称为水平串联。每个数组必须具有相同的行数。同样，如果数组具有相同的列数，则可以使用分号进行垂直串联。

```matlab
A = [a; a]
```

---

```
A = 6×3

     1     3     5
     2     4     6
     7     8    10
     1     3     5
     2     4     6
     7     8    10
```

### 矩阵和数组 {.row-span-3}

要创建每行包含四个元素的数组，请使用逗号 (`,`) 或空格分隔元素

```matlab
a = [1 2 3 4]
```

MATLAB 将执行上述语句并返回以下结果：

```
a = 1×4
     1     2     3     4
```

#### 创建多行矩阵

```matlab
a = [1 3 5; 2 4 6; 7 8 10]
```

---

```
a = 3×3
     1     3     5
     2     4     6
     7     8    10
```

#### 5×1 零列向量

```matlab
z = zeros(5,1)
```

---

```
z = 5×1
     0
     0
     0
     0
     0
```

### 复数

复数具有实部和虚部，虚数单位是 -1 的平方根。

```matlab
sqrt(-1)
```

---

```
ans = 0.0000 + 1.0000i
```

要表示复数的虚部，请使用 i 或 j。

```matlab
c = [3+4i, 4+3j; -i, 10j]
```

---

```
c = 2×2 complex

   3.0000 + 4.0000i   4.0000 + 3.0000i
   0.0000 - 1.0000i   0.0000 +10.0000i
```

## 基础知识

### 输入命令

| -                                                                               | -                                                                         |
| ------------------------------------------------------------------------------- | :------------------------------------------------------------------------ |
| [ans](https://www.mathworks.com/help/matlab/ref/ans.html)                       | 最近计算的答案                                                            |
| [clc](https://www.mathworks.com/help/matlab/ref/clc.html)                       | 清除命令行窗口                                                            |
| [diary](https://www.mathworks.com/help/matlab/ref/diary.html)                   | 将命令行窗口的文本记录到日志文件中                                        |
| [format](https://www.mathworks.com/help/matlab/ref/format.html)                 | 设置输出显示格式                                                          |
| [home](https://www.mathworks.com/help/matlab/ref/home.html)                     | 发送光标重置                                                              |
| [iskeyword](https://www.mathworks.com/help/matlab/ref/iskeyword.html)           | 判断输入是否为 <span class="trademark">MATLAB</span> 关键字                |
| [more](https://www.mathworks.com/help/matlab/ref/more.html)                     | 控制命令行窗口中的分页输出                                                |
| [commandwindow](https://www.mathworks.com/help/matlab/ref/commandwindow.html)   | 选择命令窗口                                                              |
| [commandhistory](https://www.mathworks.com/help/matlab/ref/commandhistory.html) | 打开命令历史记录窗口                                                      |

#### 对象

| -                                                                          | -                                                |
| -------------------------------------------------------------------------- | :----------------------------------------------- |
| [DisplayFormatOptions](https://www.mathworks.com/help/matlab/ref/ans.html) | 命令行窗口中的输出显示格式                       |

### 矩阵和数组 {.row-span-5}

创建和组合数组

| -                                                                 | -                                                                 |
| ----------------------------------------------------------------- | :---------------------------------------------------------------- |
| [zeros](https://www.mathworks.com/help/matlab/ref/zeros.html)     | 创建全零数组                                                      |
| [ones](https://www.mathworks.com/help/matlab/ref/ones.html)       | 创建全 1 数组                                                     |
| [rand](https://www.mathworks.com/help/matlab/ref/rand.html)       | 均匀分布的随机数                                                  |
| [true](https://www.mathworks.com/help/matlab/ref/true.html)       | 逻辑值 1 (true)                                                   |
| [false](https://www.mathworks.com/help/matlab/ref/false.html)     | 逻辑值 0 (false)                                                  |
| [eye](https://www.mathworks.com/help/matlab/ref/eye.html)         | 单位矩阵                                                          |
| [diag](https://www.mathworks.com/help/matlab/ref/diag.html)       | 创建对角矩阵或获取矩阵的对角元素                                  |
| [blkdiag](https://www.mathworks.com/help/matlab/ref/blkdiag.html) | 块对角矩阵                                                        |
| [cat](https://www.mathworks.com/help/matlab/ref/double.cat.html)  | 串联数组                                                          |
| [horzcat](https://www.mathworks.com/help/matlab/ref/horzcat.html) | 水平串联数组                                                      |
| [vertcat](https://www.mathworks.com/help/matlab/ref/vertcat.html) | 垂直串联数组                                                      |
| [repelem](https://www.mathworks.com/help/matlab/ref/repelem.html) | 重复数组元素副本                                                  |
| [repmat](https://www.mathworks.com/help/matlab/ref/repmat.html)   | 重复数组副本                                                      |

创建网格

| -                                                                     | -                                       |
| --------------------------------------------------------------------- | :-------------------------------------- |
| [linspace](https://www.mathworks.com/help/matlab/ref/linspace.html)   | 生成线性间隔向量                        |
| [logspace](https://www.mathworks.com/help/matlab/ref/logspace.html)   | 生成对数间隔向量                        |
| [freqspace](https://www.mathworks.com/help/matlab/ref/freqspace.html) | 频率响应的频率间隔                      |
| [meshgrid](https://www.mathworks.com/help/matlab/ref/meshgrid.html)   | 二维和三维网格                          |
| [ndgrid](https://www.mathworks.com/help/matlab/ref/ndgrid.html)       | N 维空间中的矩形网格                    |

确定大小、形状和顺序

| -                                                                           | -                                                          |
| --------------------------------------------------------------------------- | :--------------------------------------------------------- |
| [length](https://www.mathworks.com/help/matlab/ref/length.html)             | 最大数组维度的长度                                         |
| [size](https://www.mathworks.com/help/matlab/ref/size.html)                 | 数组大小                                                   |
| [ndims](https://www.mathworks.com/help/matlab/ref/double.ndims.html)        | 数组的维度数                                               |
| [numel](https://www.mathworks.com/help/matlab/ref/double.numel.html)        | 数组元素的数量                                             |
| [isscalar](https://www.mathworks.com/help/matlab/ref/isscalar.html)         | 判断输入是否为标量                                         |
| [issorted](https://www.mathworks.com/help/matlab/ref/issorted.html)         | 判断数组是否已排序                                         |
| [issortedrows](https://www.mathworks.com/help/matlab/ref/issortedrows.html) | 判断矩阵或表的行是否已排序                                 |
| [isvector](https://www.mathworks.com/help/matlab/ref/isvector.html)         | 判断输入是否为向量                                         |
| [ismatrix](https://www.mathworks.com/help/matlab/ref/ismatrix.html)         | 判断输入是否为矩阵                                         |
| [isrow](https://www.mathworks.com/help/matlab/ref/isrow.html)               | 判断输入是否为行向量                                       |
| [iscolumn](https://www.mathworks.com/help/matlab/ref/iscolumn.html)         | 判断输入是否为列向量                                       |
| [isempty](https://www.mathworks.com/help/matlab/ref/isempty.html)           | 判断数组是否为空                                           |

重构和重新排列

| -                                                                                   | -                                        |
| ----------------------------------------------------------------------------------- | :--------------------------------------- |
| [sort](https://www.mathworks.com/help/matlab/ref/sort.html)                         | 对数组元素进行排序                       |
| [sortrows](https://www.mathworks.com/help/matlab/ref/double.sortrows.html)          | 对矩阵行或表行进行排序                   |
| [flip](https://www.mathworks.com/help/matlab/ref/flip.html)                         | 翻转元素顺序                             |
| [fliplr](https://www.mathworks.com/help/matlab/ref/fliplr.html)                     | 从左到右翻转数组                         |
| [flipud](https://www.mathworks.com/help/matlab/ref/flipud.html)                     | 从上到下翻转数组                         |
| [rot90](https://www.mathworks.com/help/matlab/ref/rot90.html)                       | 将数组旋转 90 度                         |
| [transpose](https://www.mathworks.com/help/matlab/ref/transpose.html)               | 转置向量或矩阵                           |
| [ctranspose](https://www.mathworks.com/help/matlab/ref/ctranspose.html)             | 复共轭转置                               |
| [permute](https://www.mathworks.com/help/matlab/ref/permute.html)                   | 排列数组维度                             |
| [ipermute](https://www.mathworks.com/help/matlab/ref/ipermute.html)                 | 数组维度的逆排列                         |
| [circshift](https://www.mathworks.com/help/matlab/ref/circshift.html)               | 循环移位数组                             |
| [shiftdim](https://www.mathworks.com/help/matlab/ref/shiftdim.html)                 | 移位数组维度                             |
| [reshape](https://www.mathworks.com/help/matlab/ref/reshape.html)                   | 重塑数组                                 |
| [squeeze](https://www.mathworks.com/help/matlab/ref/squeeze.html)                   | 删除长度为 1 的维度                      |

索引

| -                                                                 | -                                                                                    |
| ----------------------------------------------------------------- | :----------------------------------------------------------------------------------- |
| [colon](https://www.mathworks.com/help/matlab/ref/colon.html)     | 向量创建、数组下标和 <code class="literal">for</code> 循环迭代                      |
| [end](https://www.mathworks.com/help/matlab/ref/end.html)         | 终止代码块或指示最大数组索引                                                         |
| [ind2sub](https://www.mathworks.com/help/matlab/ref/ind2sub.html) | 将线性索引转换为下标                                                                 |
| [sub2ind](https://www.mathworks.com/help/matlab/ref/sub2ind.html) | 将下标转换为线性索引                                                                 |

### 值类型 {.row-span-2}

创建数值变量

| -                                                               | -                                |
| --------------------------------------------------------------- | :------------------------------- |
| [double](https://www.mathworks.com/help/matlab/ref/double.html) | 双精度数组                       |
| [single](https://www.mathworks.com/help/matlab/ref/single.html) | 单精度数组                       |
| [int8](https://www.mathworks.com/help/matlab/ref/int8.html)     | 8 位有符号整数数组               |
| [int16](https://www.mathworks.com/help/matlab/ref/int16.html)   | 16 位有符号整数数组              |
| [int32](https://www.mathworks.com/help/matlab/ref/int32.html)   | 32 位有符号整数数组              |
| [int64](https://www.mathworks.com/help/matlab/ref/int64.html)   | 64 位有符号整数数组              |
| [uint8](https://www.mathworks.com/help/matlab/ref/uint8.html)   | 8 位无符号整数数组               |
| [uint16](https://www.mathworks.com/help/matlab/ref/uint16.html) | 16 位无符号整数数组              |
| [uint32](https://www.mathworks.com/help/matlab/ref/uint32.html) | 32 位无符号整数数组              |
| [uint64](https://www.mathworks.com/help/matlab/ref/uint64.html) | 64 位无符号整数数组              |

在数值类型之间转换

| -                                                                   | -                                                       |
| ------------------------------------------------------------------- | :------------------------------------------------------ |
| [cast](https://www.mathworks.com/help/matlab/ref/cast.html)         | 将变量转换为不同的数据类型                              |
| [typecast](https://www.mathworks.com/help/matlab/ref/typecast.html) | 转换数据类型而不更改基础数据                            |

查询类型和值

| -                                                                      | -                                                     |
| ---------------------------------------------------------------------- | :---------------------------------------------------- |
| [allfinite](https://www.mathworks.com/help/matlab/ref/allfinite.html") | 判断所有数组元素是否为有限值                          |
| [anynan](https://www.mathworks.com/help/matlab/ref/anynan.html")       | 判断是否有任何数组元素为 NaN                          |
| [isinteger](https://www.mathworks.com/help/matlab/ref/isinteger.html)  | 判断输入是否为整数数组                                |
| [isfloat](https://www.mathworks.com/help/matlab/ref/isfloat.html)      | 判断输入是否为浮点数组                                |
| [isnumeric](https://www.mathworks.com/help/matlab/ref/isnumeric.html)  | 判断输入是否为数值数组                                |
| [isreal](https://www.mathworks.com/help/matlab/ref/isreal.html)        | 判断数组是否使用复数存储                              |
| [isfinite](https://www.mathworks.com/help/matlab/ref/isfinite.html)    | 判断哪些数组元素是有限值                              |
| [isinf](https://www.mathworks.com/help/matlab/ref/isinf.html)          | 判断哪些数组元素是无穷大                              |
| [isnan](https://www.mathworks.com/help/matlab/ref/isnan.html)          | 判断哪些数组元素是 NaN                                |

值范围

| -                                                                   | -                                                                     |
| ------------------------------------------------------------------- | :-------------------------------------------------------------------- |
| [eps](https://www.mathworks.com/help/matlab/ref/eps.html)           | 浮点相对精度                                                          |
| [flintmax](https://www.mathworks.com/help/matlab/ref/flintmax.html) | 浮点格式中的最大连续整数                                              |
| [Inf](https://www.mathworks.com/help/matlab/ref/inf.html)           | 创建所有值为 `Inf` 的数组                                             |
| [intmax](https://www.mathworks.com/help/matlab/ref/intmax.html)     | 特定整数类型的最大值                                                  |
| [intmin](https://www.mathworks.com/help/matlab/ref/intmin.html)     | 特定整数类型的最小值                                                  |
| [NaN](https://www.mathworks.com/help/matlab/ref/nan.html)           | 创建所有值为 <code class="literal">NaN</code> 的数组                  |
| [realmax](https://www.mathworks.com/help/matlab/ref/realmax.html)   | 最大正浮点数                                                          |
| [realmin](https://www.mathworks.com/help/matlab/ref/realmin.html)   | 最小标准浮点数                                                        |

### 循环和条件语句

| -                                                                                | -                                                                 |
| -------------------------------------------------------------------------------- | :---------------------------------------------------------------- |
| [if, elseif, else](https://www.mathworks.com/help/matlab/ref/if.html)            | 条件为真时执行语句                                                |
| [switch, case, otherwise](https://www.mathworks.com/help/matlab/ref/switch.html) | 执行多组语句中的一组                                              |
| [for](https://www.mathworks.com/help/matlab/ref/for.html)                        | 用于重复指定次数的 `for` 循环                                     |
| [while](https://www.mathworks.com/help/matlab/ref/while.html)                    | 条件为真时重复执行的 `while` 循环                                 |
| [try, catch](https://www.mathworks.com/help/matlab/ref/try.html)                 | 执行语句并捕获由此产生的错误                                      |
| [break](https://www.mathworks.com/help/matlab/ref/break.html)                    | 终止 for 或 while 循环的执行                                      |
| [return](https://www.mathworks.com/help/matlab/ref/return.html)                  | 将控制权返回给调用脚本或函数                                      |
| [continue](https://www.mathworks.com/help/matlab/ref/continue.html)              | 将控制权传递给 `for` 或 `while` 循环的下一次迭代                  |
| [pause](https://www.mathworks.com/help/matlab/ref/pause.html)                    | 暂时中止 `MATLAB` 的执行                                          |
| [parfor](https://www.mathworks.com/help/matlab/ref/parfor.html)                  | 并行 for 循环                                                     |
| [end](https://www.mathworks.com/help/matlab/ref/end.html)                        | 终止代码块或指示最大数组索引                                      |

{.style-list}

### 字符串数组

| -                                                                 | -                                                      |
| ----------------------------------------------------------------- | :----------------------------------------------------- |
| [string](https://www.mathworks.com/help/matlab/ref/string.html)   | 字符串数组                                             |
| [strings](https://www.mathworks.com/help/matlab/ref/strings.html) | 创建不包含字符的字符串数组                             |
| [join](https://www.mathworks.com/help/matlab/ref/join.html)       | 合并字符串                                             |
| [plus](https://www.mathworks.com/help/matlab/ref/plus.html)       | 添加数字，附加字符串                                   |

### 字符数组

| -                                                                 | -                                            |
| ----------------------------------------------------------------- | :------------------------------------------- |
| [char](https://www.mathworks.com/help/matlab/ref/char.html)       | 字符数组                                     |
| [cellstr](https://www.mathworks.com/help/matlab/ref/cellstr.html) | 转换为字符向量元胞数组                       |
| [blanks](https://www.mathworks.com/help/matlab/ref/blanks.html)   | 创建空白字符数组                             |
| [newline](https://www.mathworks.com/help/matlab/ref/newline.html) | 创建换行符                                   |

### 字符或字符串数组

| -                                                                 | -                                         |
| ----------------------------------------------------------------- | :---------------------------------------- |
| [compose](https://www.mathworks.com/help/matlab/ref/compose.html) | 将数据格式化为多个字符串                  |
| [sprintf](https://www.mathworks.com/help/matlab/ref/sprintf.html) | 将数据格式化为字符串或字符向量            |
| [strcat](https://www.mathworks.com/help/matlab/ref/strcat.html)   | 水平连接字符串                            |
| [append](https://www.mathworks.com/help/matlab/ref/append.html)   | 合并字符串                                |

### 字符或字符串 - 转换输入参数

| -                                                                                                               | -                                                                                   |
| --------------------------------------------------------------------------------------------------------------- | :---------------------------------------------------------------------------------- |
| [convertCharsToStrings](https://www.mathworks.com/help/matlab/ref/convertcharstostrings.html)                   | 将字符数组转换为字符串数组，其他数组保持不变                                        |
| [convertStringsToChars](https://www.mathworks.com/help/matlab/ref/convertstringstochars.html)                   | 将字符串数组转换为字符数组，其他数组保持不变                                        |
| [convertContainedStringsToChars](https://www.mathworks.com/help/matlab/ref/convertcontainedstringstochars.html) | 转换元胞数组或结构体中任意级别的字符串数组 {.style-list}                            |

### 字符或字符串 - 在数值和字符串之间转换

| -                                                                       | -                                   |
| ----------------------------------------------------------------------- | :---------------------------------- |
| [double](https://www.mathworks.com/help/matlab/ref/double.html)         | 双精度数组                          |
| [string](https://www.mathworks.com/help/matlab/ref/string.html)         | 字符串数组                          |
| [str2double](https://www.mathworks.com/help/matlab/ref/str2double.html) | 将字符串转换为双精度值              |
| [num2str](https://www.mathworks.com/help/matlab/ref/num2str.html)       | 将数字转换为字符数组                |

### 字符或字符串 - 确定类型和属性 {.row-span-2}

数据类型

| -                                                                               | -                                                                    |
| ------------------------------------------------------------------------------- | :------------------------------------------------------------------- |
| [ischar](https://www.mathworks.com/help/matlab/ref/ischar.html)                 | 判断输入是否为字符数组                                               |
| [iscellstr](https://www.mathworks.com/help/matlab/ref/iscellstr.html)           | 判断输入是否为字符向量元胞数组                                       |
| [isstring](https://www.mathworks.com/help/matlab/ref/isstring.html)             | 判断输入是否为字符串数组                                             |
| [isStringScalar](https://www.mathworks.com/help/matlab/ref/isstringscalar.html) | 判断输入是否为包含一个元素的字符串数组                               |

文本属性

| -                                                                     | -                                                                               |
| --------------------------------------------------------------------- | :------------------------------------------------------------------------------ |
| [strlength](https://www.mathworks.com/help/matlab/ref/strlength.html) | 字符串长度                                                                      |
| [isstrprop](https://www.mathworks.com/help/matlab/ref/isstrprop.html) | 判断输入字符串中的哪些字符属于指定类别                                          |
| [isletter](https://www.mathworks.com/help/matlab/ref/isletter.html)   | 判断哪些字符是字母                                                              |
| [isspace](https://www.mathworks.com/help/matlab/ref/isspace.html)     | 判断哪些字符是空白字符                                                          |

### 字符或字符串 - 查找和替换 {.row-span-2}

查找

| -                                                                       | -                                                        |
| ----------------------------------------------------------------------- | :------------------------------------------------------- |
| [contains](https://www.mathworks.com/help/matlab/ref/contains.html)     | 判断字符串中是否存在模式                                 |
| [matches](https://www.mathworks.com/help/matlab/ref/matches.html)       | 判断模式是否与字符串匹配                                 |
| [count](https://www.mathworks.com/help/matlab/ref/count.html)           | 计算模式在字符串中出现的次数                             |
| [endsWith](https://www.mathworks.com/help/matlab/ref/endswith.html)     | 判断字符串是否以模式结尾                                 |
| [startsWith](https://www.mathworks.com/help/matlab/ref/startswith.html) | 判断字符串是否以模式开头                                 |
| [strfind](https://www.mathworks.com/help/matlab/ref/strfind.html)       | 在其他字符串中查找字符串                                 |
| [sscanf](https://www.mathworks.com/help/matlab/ref/sscanf.html)         | 从字符串读取格式化数据                                   |

替换

| -                                                                               | -                                               |
| ------------------------------------------------------------------------------- | :---------------------------------------------- |
| [replace](https://www.mathworks.com/help/matlab/ref/replace.html)               | 查找并替换一个或多个子字符串                    |
| [replaceBetween](https://www.mathworks.com/help/matlab/ref/replacebetween.html) | 替换开始和结束位置之间的子字符串                |
| [strrep](https://www.mathworks.com/help/matlab/ref/strrep.html)                 | 查找并替换子字符串                              |

### 字符串匹配模式 - 构建模式

| -                                                                 | -                                       |
| ----------------------------------------------------------------- | :-------------------------------------- |
| [pattern](https://www.mathworks.com/help/matlab/ref/pattern.html) | 用于搜索和匹配文本的模式                |

### 字符串匹配模式 - 字符匹配模式

| -                                                                                           | -                                               |
| ------------------------------------------------------------------------------------------- | :---------------------------------------------- |
| [alphanumericsPattern](https://www.mathworks.com/help/matlab/ref/alphanumericspattern.html) | 匹配字母数字字符                                |
| [characterListPattern](https://www.mathworks.com/help/matlab/ref/characterlistpattern.html) | 匹配列表中的字符                                |
| [digitsPattern](https://www.mathworks.com/help/matlab/ref/digitspattern.html)               | 匹配数字字符                                    |
| [lettersPattern](https://www.mathworks.com/help/matlab/ref/letterspattern.html)             | 匹配字母模式                                    |
| [whitespacePattern](https://www.mathworks.com/help/matlab/ref/whitespacepattern.html)       | 匹配空白字符                                    |
| [wildcardPattern](https://www.mathworks.com/help/matlab/ref/wildcardpattern.html)           | 尽可能少地匹配任何类型的字符                    |

### 字符串匹配模式 - 模式搜索规则

| -                                                                                               | -                                                          |
| ----------------------------------------------------------------------------------------------- | :--------------------------------------------------------- |
| [optionalPattern](https://www.mathworks.com/help/matlab/ref/optionalpattern.html)               | 使模式匹配可选                                             |
| [possessivePattern](https://www.mathworks.com/help/matlab/ref/possessivepattern.html)           | 匹配模式而不回溯                                           |
| [caseSensitivePattern](https://www.mathworks.com/help/matlab/ref/casesensitivepattern.html)     | 以区分大小写的方式匹配模式                                 |
| [caseInsensitivePattern](https://www.mathworks.com/help/matlab/ref/caseinsensitivepattern.html) | 以不区分大小写的方式匹配模式                               |
| [asFewOfPattern](https://www.mathworks.com/help/matlab/ref/asfewofpattern.html)                 | 模式匹配次数应尽可能少                                     |
| [asManyOfPattern](https://www.mathworks.com/help/matlab/ref/asmanyofpattern.html)               | 模式匹配尽可能多次                                         |

### 字符串匹配模式 - 边界模式 {.row-span-2}

| -                                                                                           | -                                                                         |
| ------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------ |
| [alphanumericBoundary](https://www.mathworks.com/help/matlab/ref/alphanumericboundary.html) | 匹配字母数字字符和非字母数字字符之间的边界                                |
| [digitBoundary](https://www.mathworks.com/help/matlab/ref/digitboundary.html)               | 匹配数字字符和非数字字符之间的边界                                        |
| [letterBoundary](https://www.mathworks.com/help/matlab/ref/letterboundary.html)             | 匹配字母字符和非字母字符之间的边界                                        |
| [whitespaceBoundary](https://www.mathworks.com/help/matlab/ref/whitespaceboundary.html)     | 匹配空白字符和非空白字符之间的边界                                        |
| [lineBoundary](https://www.mathworks.com/help/matlab/ref/lineboundary.html)                 | 匹配行的开头或结尾                                                        |
| [textBoundary](https://www.mathworks.com/help/matlab/ref/textboundary.html)                 | 匹配文本的开头或结尾                                                      |
| [lookAheadBoundary](https://www.mathworks.com/help/matlab/ref/lookaheadboundary.html)       | 匹配指定模式之前的边界                                                    |
| [lookBehindBoundary](https://www.mathworks.com/help/matlab/ref/lookbehindboundary.html)     | 匹配指定模式之后的边界                                                    |

{.style-list}

### 字符串匹配模式 - 自定义模式显示

| -                                                                             | -                                   |
| ----------------------------------------------------------------------------- | :---------------------------------- |
| [maskedPattern](https://www.mathworks.com/help/matlab/ref/maskedpattern.html) | 具有指定显示名称的模式              |
| [namedPattern](https://www.mathworks.com/help/matlab/ref/namedpattern.html)   | 指定命名模式                        |

### 字符串匹配模式 - 正则表达式

| -                                                                                 | -                                                     |
| --------------------------------------------------------------------------------- | :---------------------------------------------------- |
| [regexp](https://www.mathworks.com/help/matlab/ref/regexp.html)                   | 匹配正则表达式 (区分大小写)                           |
| [regexpi](https://www.mathworks.com/help/matlab/ref/regexpi.html)                 | 匹配正则表达式 (不区分大小写)                         |
| [regexprep](https://www.mathworks.com/help/matlab/ref/regexprep.html)             | 使用正则表达式替换文本                                |
| [regexptranslate](https://www.mathworks.com/help/matlab/ref/regexptranslate.html) | 将文本转换为正则表达式                                |
| [regexpPattern](https://www.mathworks.com/help/matlab/ref/regexppattern.html)     | 匹配指定正则表达式的模式                              |

### 字符串匹配模式 - 连接和拆分

| -                                                                               | -                                                                     |
| ------------------------------------------------------------------------------- | :-------------------------------------------------------------------- |
| [join](https://www.mathworks.com/help/matlab/ref/join.html)                     | 合并字符串                                                            |
| [plus](https://www.mathworks.com/help/matlab/ref/plus.html)                     | 添加数字，附加字符串                                                  |
| [split](https://www.mathworks.com/help/matlab/ref/split.html)                   | 在分隔符处拆分字符串                                                  |
| [splitlines](https://www.mathworks.com/help/matlab/ref/splitlines.html)         | 在换行符处拆分字符串                                                  |
| [strjoin](https://www.mathworks.com/help/matlab/ref/strjoin.html)               | 连接数组中的字符串                                                    |
| [strsplit](https://www.mathworks.com/help/matlab/ref/strsplit.html)             | 在指定分隔符处拆分字符串或字符向量                                    |
| [strtok](https://www.mathworks.com/help/matlab/ref/strtok.html)                 | 选定的字符串部分                                                      |
| [extract](https://www.mathworks.com/help/matlab/ref/extract.html)               | 从字符串中提取子字符串                                                |
| [extractAfter](https://www.mathworks.com/help/matlab/ref/extractafter.html)     | 提取指定位置之后的子字符串                                            |
| [extractBefore](https://www.mathworks.com/help/matlab/ref/extractbefore.html)   | 提取指定位置之前的子字符串                                            |
| [extractBetween](https://www.mathworks.com/help/matlab/ref/extractbetween.html) | 提取起始点和结束点之间的子字符串                                      |

### 字符串编辑 {.row-span-2}

| -                                                                               | -                                                                     |
| ------------------------------------------------------------------------------- | :-------------------------------------------------------------------- |
| [erase](https://www.mathworks.com/help/matlab/ref/erase.html)                   | 删除字符串中的子字符串                                                |
| [eraseBetween](https://www.mathworks.com/help/matlab/ref/erasebetween.html)     | 删除开始和结束之间的子字符串                                          |
| [extract](https://www.mathworks.com/help/matlab/ref/extract.html)               | 从字符串中提取子字符串                                                |
| [extractAfter](https://www.mathworks.com/help/matlab/ref/extractafter.html)     | 提取指定位置之后的子字符串                                            |
| [extractBefore](https://www.mathworks.com/help/matlab/ref/extractbefore.html)   | 提取指定位置之前的子字符串                                            |
| [extractBetween](https://www.mathworks.com/help/matlab/ref/extractbetween.html) | 提取起始点和结束点之间的子字符串                                      |
| [insertAfter](https://www.mathworks.com/help/matlab/ref/insertafter.html)       | 在指定子字符串之后插入字符串                                          |
| [insertBefore](https://www.mathworks.com/help/matlab/ref/insertbefore.html)     | 在指定子字符串之前插入字符串                                          |
| [pad](https://www.mathworks.com/help/matlab/ref/pad.html)                       | 向字符串添加前导或尾随字符                                            |
| [strip](https://www.mathworks.com/help/matlab/ref/strip.html)                   | 删除字符串中的前导和尾随字符                                          |
| [lower](https://www.mathworks.com/help/matlab/ref/lower.html)                   | 将字符串转换为小写                                                    |
| [upper](https://www.mathworks.com/help/matlab/ref/upper.html)                   | 将字符串转换为大写                                                    |
| [reverse](https://www.mathworks.com/help/matlab/ref/reverse.html)               | 反转字符串中字符的顺序                                                |
| [deblank](https://www.mathworks.com/help/matlab/ref/deblank.html)               | 删除字符串末尾的尾随空格                                              |
| [strtrim](https://www.mathworks.com/help/matlab/ref/strtrim.html)               | 从字符串中删除前导和尾随空格                                          |
| [strjust](https://www.mathworks.com/help/matlab/ref/strjust.html)               | 对齐字符串                                                            |

### 字符串比较

| -                                                                   | -                                                                                           |
| ------------------------------------------------------------------- | :------------------------------------------------------------------------------------------ |
| [matches](https://www.mathworks.com/help/matlab/ref/matches.html)   | 判断模式是否与字符串匹配                                                                    |
| [strcmp](https://www.mathworks.com/help/matlab/ref/strcmp.html)     | 比较字符串                                                                                  |
| [strcmpi](https://www.mathworks.com/help/matlab/ref/strcmpi.html)   | 比较字符串 (不区分大小写)                                                                   |
| [strncmp](https://www.mathworks.com/help/matlab/ref/strncmp.html)   | 比较字符串的前 <code class="literal">n</code> 个字符 (区分大小写)                          |
| [strncmpi](https://www.mathworks.com/help/matlab/ref/strncmpi.html) | 比较字符串的前 <code class="literal">n</code> 个字符 (不区分大小写)                        |

### 基本算术 {.row-span-3}

#### 加法

- [+](https://www.mathworks.com/help/matlab/ref/plus.html) 添加数字，附加字符串
- [sum](https://www.mathworks.com/help/matlab/ref/sum.html) 数组元素之和
- [cumsum](https://www.mathworks.com/help/matlab/ref/cumsum.html) 累积和
- [movsum](https://www.mathworks.com/help/matlab/ref/movsum.html) 移动和

{.cols-2 .marker-none}

#### 减法

- [-](https://www.mathworks.com/help/matlab/ref/minus.html) 减法
- [diff](https://www.mathworks.com/help/matlab/ref/diff.html) 差分和近似导数

{.cols-2 .marker-none}

#### 乘法

| -                                                                       | -                                   |
| ----------------------------------------------------------------------- | :---------------------------------- |
| [.\*](https://www.mathworks.com/help/matlab/ref/times.html)             | 乘法                                |
| [\*](https://www.mathworks.com/help/matlab/ref/mtimes.html)             | 矩阵乘法                            |
| [prod](https://www.mathworks.com/help/matlab/ref/prod.html)             | 数组元素的乘积                      |
| [cumprod](https://www.mathworks.com/help/matlab/ref/cumprod.html)       | 累积乘积                            |
| [pagemtimes](https://www.mathworks.com/help/matlab/ref/pagemtimes.html) | 按页矩阵乘法                        |
| [tensorprod](https://www.mathworks.com/help/matlab/ref/tensorprod.html) | 两个张量之间的张量积                |

#### 除法

| -                                                             | -                                                             |
| ------------------------------------------------------------- | :------------------------------------------------------------ |
| [./](https://www.mathworks.com/help/matlab/ref/rdivide.html)  | 数组右除                                                      |
| [.\\](https://www.mathworks.com/help/matlab/ref/ldivide.html) | 数组左除                                                      |
| [/](https://www.mathworks.com/help/matlab/ref/mrdivide.html)  | 求解关于 x 的线性方程组 xA = B                                |
| [\\](https://www.mathworks.com/help/matlab/ref/mldivide.html) | 求解关于 x 的线性方程组 Ax = B                                |

#### 幂运算

- [.^](https://www.mathworks.com/help/matlab/ref/power.html) 逐元素求幂
- [^](https://www.mathworks.com/help/matlab/ref/mpower.html) 矩阵幂

{.cols-2 .marker-none}

#### 转置

| -                                                                               | -                                   |
| ------------------------------------------------------------------------------- | :---------------------------------- |
| [.'](https://www.mathworks.com/help/matlab/ref/transpose.html)                  | 转置向量或矩阵                      |
| ['](https://www.mathworks.com/help/matlab/ref/ctranspose.html)                  | 复共轭转置                          |
| [pagetranspose](https://www.mathworks.com/help/matlab/ref/pagetranspose.html)   | 按页转置                            |
| [pagectranspose](https://www.mathworks.com/help/matlab/ref/pagectranspose.html) | 按页复共轭转置                      |

#### 数组符号

- [uminus](https://www.mathworks.com/help/matlab/ref/uminus.html) 一元减法
- [uplus](https://www.mathworks.com/help/matlab/ref/uplus.html) 一元加法

{.cols-2 .marker-none}

### 模除和舍入

| -                                                                 | -                                           |
| ----------------------------------------------------------------- | :------------------------------------------ |
| [mod](https://www.mathworks.com/help/matlab/ref/mod.html)         | 除法后的余数 (模运算)                       |
| [rem](https://www.mathworks.com/help/matlab/ref/rem.html)         | 除法后的余数                                |
| [idivide](https://www.mathworks.com/help/matlab/ref/idivide.html) | 带舍入选项的整除                            |
| [ceil](https://www.mathworks.com/help/matlab/ref/ceil.html)       | 向正无穷大舍入                              |
| [fix](https://www.mathworks.com/help/matlab/ref/fix.html)         | 向零舍入                                    |
| [floor](https://www.mathworks.com/help/matlab/ref/floor.html)     | 向负无穷大舍入                              |
| [round](https://www.mathworks.com/help/matlab/ref/round.html)     | 舍入到最近的小数或整数                      |

### 自定义二元函数

| -                                                               | -                                                                             |
| --------------------------------------------------------------- | :---------------------------------------------------------------------------- |
| [bsxfun](https://www.mathworks.com/help/matlab/ref/bsxfun.html) | 对两个数组应用逐元素运算 (启用隐式扩展)                                       |

### 关系运算

值比较

| -                                                                   | -                                                |
| ------------------------------------------------------------------- | :----------------------------------------------- |
| [==](https://www.mathworks.com/help/matlab/ref/eq.html)             | 判断相等                                         |
| [>=](https://www.mathworks.com/help/matlab/ref/ge.html)             | 判断大于或等于                                   |
| [>](https://www.mathworks.com/help/matlab/ref/gt.html)              | 判断大于                                         |
| [<=](https://www.mathworks.com/help/matlab/ref/le.html)             | 判断小于或等于                                   |
| [<](https://www.mathworks.com/help/matlab/ref/lt.html)              | 判断小于                                         |
| [~=](https://www.mathworks.com/help/matlab/ref/ne.html)             | 判断不等                                         |
| [isequal](https://www.mathworks.com/help/matlab/ref/isequal.html)   | 判断数组相等                                     |
| [isequaln](https://www.mathworks.com/help/matlab/ref/isequaln.html) | 测试数组相等性，将 `NaN` 值视为相等              |

### 逻辑 (布尔) 运算

真或假条件

| -                                                                                                     | -                                                           |
| ----------------------------------------------------------------------------------------------------- | :---------------------------------------------------------- |
| [Short-circuit &&, \|\|](https://www.mathworks.com/help/matlab/ref/logicaloperatorsshortcircuit.html) | 具有短路功能的逻辑运算符                                    |
| [&](https://www.mathworks.com/help/matlab/ref/and.html)                                               | 计算逻辑 `AND`                                              |
| [~](https://www.mathworks.com/help/matlab/ref/not.html)                                               | 计算逻辑 `NOT`                                              |
| [\|](https://www.mathworks.com/help/matlab/ref/or.html)                                               | 计算逻辑 `OR`                                               |
| [xor](https://www.mathworks.com/help/matlab/ref/xor.html)                                             | 计算逻辑异或 `OR`                                           |
| [all](https://www.mathworks.com/help/matlab/ref/all.html)                                             | 判断所有数组元素是否非零或 `true`                           |
| [any](https://www.mathworks.com/help/matlab/ref/any.html)                                             | 判断是否有任何数组元素非零                                  |
| [false](https://www.mathworks.com/help/matlab/ref/false.html)                                         | 逻辑 `0` (false)                                            |
| [find](https://www.mathworks.com/help/matlab/ref/find.html)                                           | 查找非零元素的索引和值                                      |
| [islogical](https://www.mathworks.com/help/matlab/ref/islogical.html)                                 | 判断输入是否为逻辑数组                                      |
| [logical](https://www.mathworks.com/help/matlab/ref/logical.html)                                     | 将数值转换为逻辑值                                          |
| [true](https://www.mathworks.com/help/matlab/ref/true.html)                                           | 逻辑值 `1` (true)                                           |

### 集合运算

并集、交集、集合关系

| -                                                                            | -                                                              |
| ---------------------------------------------------------------------------- | :------------------------------------------------------------- |
| [intersect](https://www.mathworks.com/help/matlab/ref/double.intersect.html) | 两个数组的集合交集                                             |
| [ismember](https://www.mathworks.com/help/matlab/ref/double.ismember.html)   | 判断数组元素是否为集合数组成员                                 |
| [setdiff](https://www.mathworks.com/help/matlab/ref/double.setdiff.html)     | 两个数组的集合差集                                             |
| [setxor](https://www.mathworks.com/help/matlab/ref/double.setxor.html)       | 两个数组的集合异或                                             |
| [union](https://www.mathworks.com/help/matlab/ref/double.union.html)         | 两个数组的集合并集                                             |
| [unique](https://www.mathworks.com/help/matlab/ref/double.unique.html)       | 数组中的唯一值                                                 |
| [ismembertol](https://www.mathworks.com/help/matlab/ref/ismembertol.html)    | 容差范围内的集合成员资格                                       |
| [uniquetol](https://www.mathworks.com/help/matlab/ref/uniquetol.html)        | 容差范围内的唯一值                                             |
| [join](https://www.mathworks.com/help/matlab/ref/table.join.html)            | 使用键变量逐行合并两个表或时间表                               |
| [innerjoin](https://www.mathworks.com/help/matlab/ref/innerjoin.html)        | 两个表或时间表之间的内连接                                     |
| [outerjoin](https://www.mathworks.com/help/matlab/ref/outerjoin.html)        | 两个表或时间表之间的外连接                                     |

### 按位运算

设置、偏移或比较特定位域

| -                                                                     | -                                      |
| --------------------------------------------------------------------- | :------------------------------------- |
| [bitand](https://www.mathworks.com/help/matlab/ref/bitand.html)       | 按位 `AND`                             |
| [bitor](https://www.mathworks.com/help/matlab/ref/bitor.html)         | 按位 `OR`                              |
| [bitxor](https://www.mathworks.com/help/matlab/ref/bitxor.html)       | 按位 `XOR`                             |
| [bitcmp](https://www.mathworks.com/help/matlab/ref/bitcmp.html)       | 按位补码                               |
| [bitget](https://www.mathworks.com/help/matlab/ref/bitget.html)       | 获取指定位置的位                       |
| [bitset](https://www.mathworks.com/help/matlab/ref/bitset.html)       | 设置指定位置的位                       |
| [bitshift](https://www.mathworks.com/help/matlab/ref/bitshift.html)   | 将位移位指定的位数                     |
| [swapbytes](https://www.mathworks.com/help/matlab/ref/swapbytes.html) | 交换字节顺序                           |

## 数据导入和导出

### 文本文件 - 读写表或时间表 {.row-span-2}

#### 基本导入和导出

| -                                                                               | -                                  |
| ------------------------------------------------------------------------------- | :--------------------------------- |
| [readtable](https://www.mathworks.com/help/matlab/ref/readtable.html)           | 基于文件创建表                     |
| [writetable](https://www.mathworks.com/help/matlab/ref/writetable.html)         | 将表写入文件                       |
| [readtimetable](https://www.mathworks.com/help/matlab/ref/readtimetable.html)   | 基于文件创建时间表                 |
| [writetimetable](https://www.mathworks.com/help/matlab/ref/writetimetable.html) | 将时间表写入文件                   |

#### 定义导入规则

| -                                                                                                                      | -                                                           |
| ---------------------------------------------------------------------------------------------------------------------- | :---------------------------------------------------------- |
| [detectImportOptions](https://www.mathworks.com/help/matlab/ref/detectimportoptions.html)                              | 基于文件内容生成导入选项                                    |
| [delimitedTextImportOptions](https://www.mathworks.com/help/matlab/ref/matlab.io.text.delimitedtextimportoptions.html) | 分隔文本的导入选项对象                                      |
| [fixedWidthImportOptions](https://www.mathworks.com/help/matlab/ref/matlab.io.text.fixedwidthimportoptions.html)       | 固定宽度文本文件的导入选项对象                              |
| [xmlImportOptions](https://www.mathworks.com/help/matlab/ref/matlab.io.xml.xmlimportoptions.html)                      | XML 文件的导入选项对象                                      |
| [htmlImportOptions](https://www.mathworks.com/help/matlab/ref/matlab.io.html.htmlimportoptions.html)                   | HTML 文件的导入选项对象                                     |
| [wordDocumentImportOptions](https://www.mathworks.com/help/matlab/ref/matlab.io.word.worddocumentimportoptions.html)   | `Microsoft Word` 文件导入选项对象                           |
| [getvaropts](https://www.mathworks.com/help/matlab/ref/matlab.io.text.delimitedtextimportoptions.getvaropts.html)      | 获取变量导入选项                                            |
| [setvaropts](https://www.mathworks.com/help/matlab/ref/matlab.io.text.delimitedtextimportoptions.setvaropts.html)      | 设置变量导入选项                                            |
| [setvartype](https://www.mathworks.com/help/matlab/ref/matlab.io.text.delimitedtextimportoptions.setvartype.html)      | 设置变量数据类型                                            |
| [preview](https://www.mathworks.com/help/matlab/ref/matlab.io.text.delimitedtextimportoptions.preview.html)            | 使用导入选项预览文件中的八行数据                            |

{.style-list}

### 文本文件 - 读写矩阵和数组

| -                                                                         | -                                              |
| ------------------------------------------------------------------------- | :--------------------------------------------- |
| [readmatrix](https://www.mathworks.com/help/matlab/ref/readmatrix.html)   | 从文件读取矩阵                                 |
| [writematrix](https://www.mathworks.com/help/matlab/ref/writematrix.html) | 将矩阵写入文件                                 |
| [readcell](https://www.mathworks.com/help/matlab/ref/readcell.html)       | 从文件读取元胞数组                             |
| [writecell](https://www.mathworks.com/help/matlab/ref/writecell.html)     | 将元胞数组写入文件                             |
| [readvars](https://www.mathworks.com/help/matlab/ref/readvars.html)       | 从文件读取变量                                 |
| [textscan](https://www.mathworks.com/help/matlab/ref/textscan.html)       | 从文本文件或字符串读取格式化数据               |
| [type](https://www.mathworks.com/help/matlab/ref/type.html)               | 显示文件内容                                   |
| [fileread](https://www.mathworks.com/help/matlab/ref/fileread.html)       | 以文本格式读取文件内容                         |
| [readlines](https://www.mathworks.com/help/matlab/ref/readlines.html)     | 将文件的行作为字符串数组读取                   |
| [writelines](https://www.mathworks.com/help/matlab/ref/writelines.html)   | 将文本写入文件                                 |

### 电子表格 - 读写表或时间表 {.row-span-2}

基本导入和导出

| -                                                                               | -                                      |
| ------------------------------------------------------------------------------- | :------------------------------------- |
| [readtable](https://www.mathworks.com/help/matlab/ref/readtable.html)           | 从文件创建表                           |
| [writetable](https://www.mathworks.com/help/matlab/ref/writetable.html)         | 将表写入文件                           |
| [readtimetable](https://www.mathworks.com/help/matlab/ref/readtimetable.html)   | 从文件创建时间表                       |
| [writetimetable](https://www.mathworks.com/help/matlab/ref/writetimetable.html) | 将时间表写入文件                       |
| [sheetnames](https://www.mathworks.com/help/matlab/ref/sheetnames.html)         | 从电子表格文件获取工作表名称           |

{.style-list}

定义导入规则

| -                                                                                                                         | -                                                        |
| ------------------------------------------------------------------------------------------------------------------------- | :------------------------------------------------------- |
| [detectImportOptions](https://www.mathworks.com/help/matlab/ref/detectimportoptions.html)                                 | 基于文件内容生成导入选项                                 |
| [spreadsheetImportOptions](https://www.mathworks.com/help/matlab/ref/matlab.io.spreadsheet.spreadsheetimportoptions.html) | 电子表格导入选项对象                                     |
| [getvaropts](https://www.mathworks.com/help/matlab/ref/matlab.io.text.delimitedtextimportoptions.getvaropts.html)         | 获取变量导入选项                                         |
| [setvaropts](https://www.mathworks.com/help/matlab/ref/matlab.io.text.delimitedtextimportoptions.setvaropts.html)         | 设置变量导入选项                                         |
| [setvartype](https://www.mathworks.com/help/matlab/ref/matlab.io.text.delimitedtextimportoptions.setvartype.html)         | 设置变量数据类型                                         |
| [preview](https://www.mathworks.com/help/matlab/ref/matlab.io.text.delimitedtextimportoptions.preview.html)               | 使用导入选项预览文件中的八行数据                         |

{.style-list}

### 电子表格 - 读写矩阵和数组

| -                                                                         | -                             |
| ------------------------------------------------------------------------- | :---------------------------- |
| [readmatrix](https://www.mathworks.com/help/matlab/ref/readmatrix.html)   | 从文件读取矩阵                |
| [writematrix](https://www.mathworks.com/help/matlab/ref/writematrix.html) | 将矩阵写入文件                |
| [readcell](https://www.mathworks.com/help/matlab/ref/readcell.html)       | 从文件读取元胞数组            |
| [writecell](https://www.mathworks.com/help/matlab/ref/writecell.html)     | 将元胞数组写入文件            |
| [readvars](https://www.mathworks.com/help/matlab/ref/readvars.html)       | 从文件读取变量                |
| [importdata](https://www.mathworks.com/help/matlab/ref/importdata.html)   | 从文件加载数据                |

### 图像

| -                                                                 | -                                         |
| ----------------------------------------------------------------- | :---------------------------------------- |
| [imfinfo](https://www.mathworks.com/help/matlab/ref/imfinfo.html) | 关于图形文件的信息                        |
| [imread](https://www.mathworks.com/help/matlab/ref/imread.html)   | 从图形文件读取图像                        |
| [imwrite](https://www.mathworks.com/help/matlab/ref/imwrite.html) | 将图像写入图形文件                        |
| [Tiff](https://www.mathworks.com/help/matlab/ref/tiff.html)       | LibTIFF 库例程的 MATLAB 入口点            |

### 读取或写入 NetCDF 文件 {.row-span-2}

| -                                                                             | -                                                              |
| ----------------------------------------------------------------------------- | :------------------------------------------------------------- |
| [nccreate](https://www.mathworks.com/help/matlab/ref/nccreate.html)           | 在 NetCDF 文件中创建变量                                       |
| [ncdisp](https://www.mathworks.com/help/matlab/ref/ncdisp.html)               | 在命令行窗口中显示 NetCDF 数据源内容                           |
| [ncinfo](https://www.mathworks.com/help/matlab/ref/ncinfo.html)               | 返回有关 NetCDF 数据源的信息                                   |
| [ncread](https://www.mathworks.com/help/matlab/ref/ncread.html)               | 从 NetCDF 数据源读取变量数据                                   |
| [ncreadatt](https://www.mathworks.com/help/matlab/ref/ncreadatt.html)         | 读取 NetCDF 数据源中的属性值                                   |
| [ncwrite](https://www.mathworks.com/help/matlab/ref/ncwrite.html)             | 将数据写入 NetCDF 文件                                         |
| [ncwriteatt](https://www.mathworks.com/help/matlab/ref/ncwriteatt.html)       | 将属性写入 NetCDF 文件                                         |
| [ncwriteschema](https://www.mathworks.com/help/matlab/ref/ncwriteschema.html) | 将 NetCDF 模式定义添加到 NetCDF 文件                           |

### NetCDF 库包 - 库函数

| -                                                                                                 | -                                                            |
| ------------------------------------------------------------------------------------------------- | :----------------------------------------------------------- |
| [netcdf.getChunkCache](https://www.mathworks.com/help/matlab/ref/netcdf.getchunkcache.html)       | 检索 NetCDF 库的块缓存设置                                   |
| [netcdf.inqLibVers](https://www.mathworks.com/help/matlab/ref/netcdf.inqlibvers.html)             | 返回 NetCDF 库版本信息                                       |
| [netcdf.setChunkCache](https://www.mathworks.com/help/matlab/ref/netcdf.setchunkcache.html)       | 设置 NetCDF 库的默认块缓存设置                               |
| [netcdf.setDefaultFormat](https://www.mathworks.com/help/matlab/ref/netcdf.setdefaultformat.html) | 更改默认的 netCDF 文件格式                                   |

{.style-list}

### NetCDF 库包 - 文件操作 {.row-span-2}

| -                                                                                         | -                                                  |
| ----------------------------------------------------------------------------------------- | :------------------------------------------------- |
| [netcdf.abort](https://www.mathworks.com/help/matlab/ref/netcdf.abort.html)               | 恢复最近的 netCDF 文件定义                         |
| [netcdf.close](https://www.mathworks.com/help/matlab/ref/netcdf.close.html)               | 关闭 netCDF 文件                                   |
| [netcdf.create](https://www.mathworks.com/help/matlab/ref/netcdf.create.html)             | 创建新的 NetCDF 数据集                             |
| [netcdf.endDef](https://www.mathworks.com/help/matlab/ref/netcdf.enddef.html)             | 结束 netCDF 文件定义模式                           |
| [netcdf.inq](https://www.mathworks.com/help/matlab/ref/netcdf.inq.html)                   | 返回有关 netCDF 文件的信息                         |
| [netcdf.inqFormat](https://www.mathworks.com/help/matlab/ref/netcdf.inqformat.html)       | 确定 NetCDF 文件的格式                             |
| [netcdf.inqGrps](https://www.mathworks.com/help/matlab/ref/netcdf.inqgrps.html)           | 检索子组 ID 数组                                   |
| [netcdf.inqUnlimDims](https://www.mathworks.com/help/matlab/ref/netcdf.inqunlimdims.html) | 检索组中无限维度的列表                             |
| [netcdf.open](https://www.mathworks.com/help/matlab/ref/netcdf.open.html)                 | 打开 NetCDF 数据源                                 |
| [netcdf.reDef](https://www.mathworks.com/help/matlab/ref/netcdf.redef.html)               | 将打开的 netCDF 文件置于定义模式                   |
| [netcdf.setFill](https://www.mathworks.com/help/matlab/ref/netcdf.setfill.html)           | 设置 netCDF 填充模式                               |
| [netcdf.sync](https://www.mathworks.com/help/matlab/ref/netcdf.sync.html)                 | 将 netCDF 文件同步到磁盘                           |

### NetCDF 库包 - 维度

| -                                                                                   | -                                          |
| ----------------------------------------------------------------------------------- | :----------------------------------------- |
| [netcdf.defdim](https://www.mathworks.com/help/matlab/ref/netcdf.defdim.html)       | 创建 netCDF 维度                           |
| [netcdf.inqDim](https://www.mathworks.com/help/matlab/ref/netcdf.inqdim.html)       | 返回 netCDF 维度名称和长度                 |
| [netcdf.inqDimID](https://www.mathworks.com/help/matlab/ref/netcdf.inqdimid.html)   | 返回维度 ID                                |
| [netcdf.renameDim](https://www.mathworks.com/help/matlab/ref/netcdf.renamedim.html) | 更改 netCDF 维度名称                       |

### NetCDF 库包 - 组

| -                                                                                             | -                                                    |
| --------------------------------------------------------------------------------------------- | :--------------------------------------------------- |
| [netcdf.defGrp](https://www.mathworks.com/help/matlab/ref/netcdf.defgrp.html)                 | 在 NetCDF 文件中创建组                               |
| [netcdf.inqDimIDs](https://www.mathworks.com/help/matlab/ref/netcdf.inqdimids.html)           | 检索组中维度标识符的列表                             |
| [netcdf.inqGrpName](https://www.mathworks.com/help/matlab/ref/netcdf.inqgrpname.html)         | 检索组名称                                           |
| [netcdf.inqGrpNameFull](https://www.mathworks.com/help/matlab/ref/netcdf.inqgrpnamefull.html) | 组的完整路径名                                       |
| [netcdf.inqGrpParent](https://www.mathworks.com/help/matlab/ref/netcdf.inqgrpparent.html)     | 检索父组的 ID                                        |
| [netcdf.inqNcid](https://www.mathworks.com/help/matlab/ref/netcdf.inqncid.html)               | 返回命名组的 ID                                      |
| [netcdf.inqVarIDs](https://www.mathworks.com/help/matlab/ref/netcdf.inqvarids.html)           | 组中所有变量的 ID                                    |

### NetCDF 库包 - 变量 {.row-span-3}

| -                                                                                                 | -                                                         |
| ------------------------------------------------------------------------------------------------- | :-------------------------------------------------------- |
| [netcdf.defVarFill](https://www.mathworks.com/help/matlab/ref/netcdf.defvarfill.html)             | 定义 NetCDF 变量的填充参数                                |
| [netcdf.defVar](https://www.mathworks.com/help/matlab/ref/netcdf.defvar.html)                     | 创建 NetCDF 变量                                          |
| [netcdf.defVarChunking](https://www.mathworks.com/help/matlab/ref/netcdf.defvarchunking.html)     | 定义 NetCDF 变量的分块行为                                |
| [netcdf.defVarDeflate](https://www.mathworks.com/help/matlab/ref/netcdf.defvardeflate.html)       | 定义 NetCDF 变量的压缩参数                                |
| [netcdf.defVarFletcher32](https://www.mathworks.com/help/matlab/ref/netcdf.defvarfletcher32.html) | 定义 NetCDF 变量的验证参数                                |
| [netcdf.getVar](https://www.mathworks.com/help/matlab/ref/netcdf.getvar.html)                     | 读取 NetCDF 变量中的数据                                  |
| [netcdf.inqVar](https://www.mathworks.com/help/matlab/ref/netcdf.inqvar.html)                     | 关于变量的信息                                            |
| [netcdf.inqVarChunking](https://www.mathworks.com/help/matlab/ref/netcdf.inqvarchunking.html)     | 确定 NetCDF 变量的分块设置                                |
| [netcdf.inqVarDeflate](https://www.mathworks.com/help/matlab/ref/netcdf.inqvardeflate.html)       | 确定 NetCDF 变量的压缩设置                                |
| [netcdf.inqVarFill](https://www.mathworks.com/help/matlab/ref/netcdf.inqvarfill.html)             | 确定 NetCDF 变量的填充参数值                              |
| [netcdf.inqVarFletcher32](https://www.mathworks.com/help/matlab/ref/netcdf.inqvarfletcher32.html) | 关于 NetCDF 变量的 Fletcher32 校验和设置                  |
| [netcdf.inqVarID](https://www.mathworks.com/help/matlab/ref/netcdf.inqvarid.html)                 | 返回与变量名称关联的 ID                                   |
| [netcdf.putVar](https://www.mathworks.com/help/matlab/ref/netcdf.putvar.html)                     | 将数据写入 netCDF 变量                                    |
| [netcdf.renameVar](https://www.mathworks.com/help/matlab/ref/netcdf.renamevar.html)               | 更改 netCDF 变量名称                                      |

{.style-list}

### NetCDF 库包 - 属性

| -                                                                                     | -                                           |
| ------------------------------------------------------------------------------------- | :------------------------------------------ |
| [netcdf.copyAtt](https://www.mathworks.com/help/matlab/ref/netcdf.copyatt.html)       | 将属性复制到新位置                          |
| [netcdf.delAtt](https://www.mathworks.com/help/matlab/ref/netcdf.delatt.html)         | 删除 netCDF 属性                            |
| [netcdf.getAtt](https://www.mathworks.com/help/matlab/ref/netcdf.getatt.html)         | 返回 NetCDF 属性                            |
| [netcdf.inqAtt](https://www.mathworks.com/help/matlab/ref/netcdf.inqatt.html)         | 返回有关 netCDF 属性的信息                  |
| [netcdf.inqAttID](https://www.mathworks.com/help/matlab/ref/netcdf.inqattid.html)     | 返回 netCDF 属性的 ID                       |
| [netcdf.inqAttName](https://www.mathworks.com/help/matlab/ref/netcdf.inqattname.html) | 返回 netCDF 属性名称                        |
| [netcdf.putAtt](https://www.mathworks.com/help/matlab/ref/netcdf.putatt.html)         | 写入 netCDF 属性                            |
| [netcdf.renameAtt](https://www.mathworks.com/help/matlab/ref/netcdf.renameatt.html)   | 更改属性名称                                |

### NetCDF 库包 - 用户定义类型

| :-                                                                                      | :-                                                       |
| :-------------------------------------------------------------------------------------- | :------------------------------------------------------- |
| [netcdf.defVlen](https://www.mathworks.com/help/matlab/ref/netcdf.defvlen.html)         | 定义用户定义的可变长度数组类型 (NC_VLEN)                 |
| [netcdf.inqUserType](https://www.mathworks.com/help/matlab/ref/netcdf.inqusertype.html) | 返回有关用户定义类型的信息                               |
| [netcdf.inqVlen](https://www.mathworks.com/help/matlab/ref/netcdf.inqvlen.html)         | 返回有关用户定义 `NC_VLEN` 类型的信息                    |

{.style-list}

### NetCDF 库包 - 实用程序

| -                                                                                                 | -                                                       |
| ------------------------------------------------------------------------------------------------- | :------------------------------------------------------ |
| [netcdf.getConstant](https://www.mathworks.com/help/matlab/ref/netcdf.getconstant.html)           | 返回命名常量的值                                        |
| [netcdf.getConstantNames](https://www.mathworks.com/help/matlab/ref/netcdf.getconstantnames.html) | 返回 netCDF 库已知的常量列表                            |

{.style-list}

### 读取或写入 HDF5 文件

| -                                                                       | -                                 |
| ----------------------------------------------------------------------- | :-------------------------------- |
| [h5create](https://www.mathworks.com/help/matlab/ref/h5create.html)     | 创建 HDF5 数据集                  |
| [h5disp](https://www.mathworks.com/help/matlab/ref/h5disp.html)         | 显示 HDF5 文件的内容              |
| [h5info](https://www.mathworks.com/help/matlab/ref/h5info.html)         | 关于 HDF5 文件的信息              |
| [h5read](https://www.mathworks.com/help/matlab/ref/h5read.html)         | 从 HDF5 数据集读取数据            |
| [h5readatt](https://www.mathworks.com/help/matlab/ref/h5readatt.html)   | 从 HDF5 文件读取属性              |
| [h5write](https://www.mathworks.com/help/matlab/ref/h5write.html)       | 写入 HDF5 数据集                  |
| [h5writeatt](https://www.mathworks.com/help/matlab/ref/h5writeatt.html) | 写入 HDF5 属性                    |

### HDF5 库包 {.row-span-4}

| -                                                                                           | -                                                                |
| ------------------------------------------------------------------------------------------- | :--------------------------------------------------------------- |
| [库 (H5)](https://www.mathworks.com/help/matlab/ref/libraryh5.html)                         | 与整个 HDF5 库一起使用的通用函数                                 |
| [属性 (H5A)](https://www.mathworks.com/help/matlab/ref/attributeh5a.html)                   | 与数据集或组关联的元数据                                         |
| [数据集 (H5D)](https://www.mathworks.com/help/matlab/ref/dataseth5d.html)                   | 数据元素的多维数组和支持元数据                                   |
| [维度刻度 (H5DS)](https://www.mathworks.com/help/matlab/ref/dimensionscaleh5ds.html)        | 与数据集维度关联的维度刻度                                       |
| [错误 (H5E)](https://www.mathworks.com/help/matlab/ref/errorh5e.html)                       | 错误处理                                                         |
| [文件 (H5F)](https://www.mathworks.com/help/matlab/ref/fileh5f.html)                        | HDF5 文件访问                                                    |
| [组 (H5G)](https://www.mathworks.com/help/matlab/ref/grouph5g.html)                         | 文件中对象的组织                                                 |
| [标识符 (H5I)](https://www.mathworks.com/help/matlab/ref/identifierh5i.html)                 | HDF5 对象标识符                                                  |
| [链接 (H5L)](https://www.mathworks.com/help/matlab/ref/linkh5l.html)                        | HDF5 文件中的链接                                                |
| [MATLAB (H5ML)](https://www.mathworks.com/help/matlab/ref/matlabh5ml.html)                  | `MATLAB` 实用函数，不属于 HDF5 C 库                              |
| [对象 (H5O)](https://www.mathworks.com/help/matlab/ref/objecth5o.html)                      | 文件中的对象                                                     |
| [属性 (H5P)](https://www.mathworks.com/help/matlab/ref/propertyh5p.html)                    | 对象属性列表                                                     |
| [引用 (H5R)](https://www.mathworks.com/help/matlab/ref/referenceh5r.html)                  | HDF5 引用                                                        |
| [数据空间 (H5S)](https://www.mathworks.com/help/matlab/ref/dataspaceh5s.html)               | 数据集的维度                                                     |
| [数据类型 (H5T)](https://www.mathworks.com/help/matlab/ref/datatypeh5t.html)                | 数据集中元素的数据类型                                           |

{.style-list}

### HDF4 文件 - 高级函数

| -                                                                 | -                                       |
| ----------------------------------------------------------------- | :-------------------------------------- |
| [hdfinfo](https://www.mathworks.com/help/matlab/ref/hdfinfo.html) | 关于 HDF4 或 HDF-EOS 文件的信息         |
| [hdfread](https://www.mathworks.com/help/matlab/ref/hdfread.html) | 从 HDF4 或 HDF-EOS 文件读取数据         |
| [imread](https://www.mathworks.com/help/matlab/ref/imread.html)   | 从图形文件读取图像                      |
| [imwrite](https://www.mathworks.com/help/matlab/ref/imwrite.html) | 将图像写入图形文件                      |

### 低级函数 - 包 {.row-span-3}

| -                                                                                         | -                                                                            |
| ----------------------------------------------------------------------------------------- | :--------------------------------------------------------------------------- |
| [matlab.io.hdf4.sd](https://www.mathworks.com/help/matlab/ref/matlab.io.hdf4.sd.html)     | 直接与 HDF4 多文件科学数据集 (SD) 接口交互                                   |
| [matlab.io.hdfeos.gd](https://www.mathworks.com/help/matlab/ref/matlab.io.hdfeos.gd.html) | 对 HDF-EOS 网格数据的低级访问                                                |
| [matlab.io.hdfeos.sw](https://www.mathworks.com/help/matlab/ref/matlab.io.hdfeos.sw.html) | 对 HDF-EOS 分段文件的低级访问                                                |

#### 低级函数 - 函数

| -                                                                 | -                                                     |
| ----------------------------------------------------------------- | :---------------------------------------------------- |
| [hdfan](https://www.mathworks.com/help/matlab/ref/hdfan.html)     | HDF 多文件注释 (AN) 接口的入口点                      |
| [hdfhx](https://www.mathworks.com/help/matlab/ref/hdfhx.html)     | HDF 外部数据 (HX) 接口的入口点                        |
| [hdfh](https://www.mathworks.com/help/matlab/ref/hdfh.html)       | HDF H 接口的入口点                                    |
| [hdfhd](https://www.mathworks.com/help/matlab/ref/hdfhd.html)     | HDF HD 接口的入口点                                   |
| [hdfhe](https://www.mathworks.com/help/matlab/ref/hdfhe.html)     | HDF HE 接口的入口点                                   |
| [hdfml](https://www.mathworks.com/help/matlab/ref/hdfml.html)     | 与 `MATLAB` HDF 入口函数一起使用的实用程序            |
| [hdfpt](https://www.mathworks.com/help/matlab/ref/hdfpt.html)     | HDF-EOS 点对象的接口                                  |
| [hdfv](https://www.mathworks.com/help/matlab/ref/hdfv.html)       | HDF Vgroup (V) 接口的入口点                           |
| [hdfvf](https://www.mathworks.com/help/matlab/ref/hdfvf.html)     | HDF Vdata 接口中 VF 函数的入口点                      |
| [hdfvh](https://www.mathworks.com/help/matlab/ref/hdfvh.html)     | HDF Vdata 接口中 VH 函数的入口点                      |
| [hdfvs](https://www.mathworks.com/help/matlab/ref/hdfvs.html)     | HDF Vdata 接口中 VS 函数的入口点                      |
| [hdfdf24](https://www.mathworks.com/help/matlab/ref/hdfdf24.html) | HDF 24 位光栅图像 (DF24) 接口入口点                   |
| [hdfdfr8](https://www.mathworks.com/help/matlab/ref/hdfdfr8.html) | HDF 8 位光栅图像 (DFR8) 接口入口点                    |

### FITS 文件 - 函数

| -                                                                     | -                            |
| --------------------------------------------------------------------- | :--------------------------- |
| [fitsdisp](https://www.mathworks.com/help/matlab/ref/fitsdisp.html)   | 显示 FITS 元数据             |
| [fitsinfo](https://www.mathworks.com/help/matlab/ref/fitsinfo.html)   | 关于 FITS 文件的信息         |
| [fitsread](https://www.mathworks.com/help/matlab/ref/fitsread.html)   | 读取 FITS 文件中的数据       |
| [fitswrite](https://www.mathworks.com/help/matlab/ref/fitswrite.html) | 将图像写入 FITS 文件         |

### FITS 文件 - 文件访问

| -                                                                                          | -                         |
| ------------------------------------------------------------------------------------------ | :------------------------ |
| [createFile](https://www.mathworks.com/help/matlab/ref/matlab.io.fits.createfile.html)     | 创建 FITS 文件            |
| [openFile](https://www.mathworks.com/help/matlab/ref/matlab.io.fits.openfile.html)         | 打开 FITS 文件            |
| [openDiskFile](https://www.mathworks.com/help/matlab/ref/matlab.io.fits.opendiskfile.html) | 打开 FITS 文件            |
| [closeFile](https://www.mathworks.com/help/matlab/ref/matlab.io.fits.closefile.html)       | 关闭 FITS 文件            |
| [deleteFile](https://www.mathworks.com/help/matlab/ref/matlab.io.fits.deletefile.html)     | 删除 FITS 文件            |
| [fileName](https://www.mathworks.com/help/matlab/ref/matlab.io.fits.filename.html)         | FITS 文件的名称           |
| [fileMode](https://www.mathworks.com/help/matlab/ref/matlab.io.fits.filemode.html)         | FITS 文件的 I/O 模式      |

### FITS 文件 - 图像处理

| -                                                                                      | -                                           |
| -------------------------------------------------------------------------------------- | :------------------------------------------ |
| [createImg](https://www.mathworks.com/help/matlab/ref/matlab.io.fits.createimg.html)   | 创建 FITS 图像                              |
| [getImgSize](https://www.mathworks.com/help/matlab/ref/matlab.io.fits.getimgsize.html) | 图像大小                                    |
| [getImgType](https://www.mathworks.com/help/matlab/ref/matlab.io.fits.getimgtype.html) | 图像的数据类型                              |
| [insertImg](https://www.mathworks.com/help/matlab/ref/matlab.io.fits.insertimg.html)   | 在当前图像之后插入 FITS 图像                |
| [readImg](https://www.mathworks.com/help/matlab/ref/matlab.io.fits.readimg.html)       | 读取图像数据                                |
| [setBscale](https://www.mathworks.com/help/matlab/ref/matlab.io.fits.setbscale.html)   | 重置图像缩放                                |
| [writeImg](https://www.mathworks.com/help/matlab/ref/matlab.io.fits.writeimg.html)     | 写入 FITS 图像                              |

### FITS 文件 - 关键字 {.row-span-2}

| -                                                                                                | -                                               |
| ------------------------------------------------------------------------------------------------ | :---------------------------------------------- |
| [readCard](https://www.mathworks.com/help/matlab/ref/matlab.io.fits.readcard.html)               | 关键字的标头记录                                |
| [readKey](https://www.mathworks.com/help/matlab/ref/matlab.io.fits.readkey.html)                 | 关键字                                          |
| [readKeyCmplx](https://www.mathworks.com/help/matlab/ref/matlab.io.fits.readkeycmplx.html)       | 复数标量值形式的关键字                          |
| [readKeyDbl](https://www.mathworks.com/help/matlab/ref/matlab.io.fits.readkeydbl.html)           | 双精度值形式的关键字                            |
| [readKeyLongLong](https://www.mathworks.com/help/matlab/ref/matlab.io.fits.readkeylonglong.html) | `int64` 形式的关键字                            |
| [readKeyLongStr](https://www.mathworks.com/help/matlab/ref/matlab.io.fits.readkeylongstr.html)   | 长字符串值                                      |
| [readKeyUnit](https://www.mathworks.com/help/matlab/ref/matlab.io.fits.readkeyunit.html)         | 关键字中的物理单位字符串                        |
| [readRecord](https://www.mathworks.com/help/matlab/ref/matlab.io.fits.readrecord.html)           | 按编号指定的标头记录                            |
| [writeComment](https://www.mathworks.com/help/matlab/ref/matlab.io.fits.writecomment.html)       | 将 COMMENT 关键字写入或附加到 CHU               |
| [writeDate](https://www.mathworks.com/help/matlab/ref/matlab.io.fits.writedate.html)             | 将 DATE 关键字写入 CHU                          |
| [writeKey](https://www.mathworks.com/help/matlab/ref/matlab.io.fits.writekey.html)               | 更新或向当前 HDU 添加新关键字                   |
| [writeKeyUnit](https://www.mathworks.com/help/matlab/ref/matlab.io.fits.writekeyunit.html)       | 写入物理单位字符串                              |
| [writeHistory](https://www.mathworks.com/help/matlab/ref/matlab.io.fits.writehistory.html)       | 将 HISTORY 关键字写入或附加到 CHU               |
| [deleteKey](https://www.mathworks.com/help/matlab/ref/matlab.io.fits.deletekey.html)             | 按名称删除关键字                                |
| [deleteRecord](https://www.mathworks.com/help/matlab/ref/matlab.io.fits.deleterecord.html)       | 按记录编号删除关键字                            |
| [getHdrSpace](https://www.mathworks.com/help/matlab/ref/matlab.io.fits.gethdrspace.html)         | 标头中的关键字数量                              |

### FITS 文件 - 标头数据单元 (HDU) 访问

| -                                                                                            | -                                                                  |
| -------------------------------------------------------------------------------------------- | :----------------------------------------------------------------- |
| [copyHDU](https://www.mathworks.com/help/matlab/ref/matlab.io.fits.copyhdu.html)             | 将当前 HDU 从一个文件复制到另一个文件                              |
| [getHDUnum](https://www.mathworks.com/help/matlab/ref/matlab.io.fits.gethdunum.html)         | FITS 文件中当前 HDU 的编号                                         |
| [getHDUtype](https://www.mathworks.com/help/matlab/ref/matlab.io.fits.gethdutype.html)       | 当前 HDU 类型                                                      |
| [getNumHDUs](https://www.mathworks.com/help/matlab/ref/matlab.io.fits.getnumhdus.html)       | FITS 文件中的 HDU 总数                                             |
| [movAbsHDU](https://www.mathworks.com/help/matlab/ref/matlab.io.fits.movabshdu.html)         | 移动到绝对 HDU 编号                                                |
| [movNamHDU](https://www.mathworks.com/help/matlab/ref/matlab.io.fits.movnamhdu.html)         | 移动到包含特定类型和关键字值的第一个 HDU                           |
| [movRelHDU](https://www.mathworks.com/help/matlab/ref/matlab.io.fits.movrelhdu.html)         | 从当前 HDU 移动相对数量的 HDU                                      |
| [writeChecksum](https://www.mathworks.com/help/matlab/ref/matlab.io.fits.writechecksum.html) | 计算并写入当前 HDU 的校验和                                        |
| [deleteHDU](https://www.mathworks.com/help/matlab/ref/matlab.io.fits.deletehdu.html)         | 删除 FITS 文件中的当前 HDU                                         |

### FITS 文件 - 图像压缩

| -                                                                                                      | -                                                     |
| ------------------------------------------------------------------------------------------------------ | :---------------------------------------------------- |
| [imgCompress](https://www.mathworks.com/help/matlab/ref/matlab.io.fits.imgcompress.html)               | 将 HDU 从一个文件压缩到另一个文件                     |
| [isCompressedImg](https://www.mathworks.com/help/matlab/ref/matlab.io.fits.iscompressedimg.html)       | 判断当前图像是否已压缩                                |
| [setCompressionType](https://www.mathworks.com/help/matlab/ref/matlab.io.fits.setcompressiontype.html) | 设置图像压缩类型                                      |
| [setHCompScale](https://www.mathworks.com/help/matlab/ref/matlab.io.fits.sethcompscale.html)           | 设置 HCOMPRESS 算法的缩放参数                         |
| [setHCompSmooth](https://www.mathworks.com/help/matlab/ref/matlab.io.fits.sethcompsmooth.html)         | 设置使用 HCOMPRESS 压缩的图像的平滑处理               |
| [setTileDim](https://www.mathworks.com/help/matlab/ref/matlab.io.fits.settiledim.html)                 | 设置图块维度                                          |

### FITS 文件 - ASCII 表和二进制表 {.row-span-3}

| -                                                                                          | -                                                         |
| ------------------------------------------------------------------------------------------ | :-------------------------------------------------------- |
| [createTbl](https://www.mathworks.com/help/matlab/ref/matlab.io.fits.createtbl.html)       | 创建新的 ASCII 或二进制表扩展                             |
| [insertCol](https://www.mathworks.com/help/matlab/ref/matlab.io.fits.insertcol.html)       | 向表中插入列                                              |
| [insertRows](https://www.mathworks.com/help/matlab/ref/matlab.io.fits.insertrows.html)     | 向表中插入行                                              |
| [insertATbl](https://www.mathworks.com/help/matlab/ref/matlab.io.fits.insertatbl.html)     | 在当前 HDU 之后插入 ASCII 表                              |
| [insertBTbl](https://www.mathworks.com/help/matlab/ref/matlab.io.fits.insertbtbl.html)     | 在当前 HDU 之后插入二进制表                               |
| [deleteCol](https://www.mathworks.com/help/matlab/ref/matlab.io.fits.deletecol.html)       | 从表中删除列                                              |
| [deleteRows](https://www.mathworks.com/help/matlab/ref/matlab.io.fits.deleterows.html)     | 从表中删除行                                              |
| [getAColParms](https://www.mathworks.com/help/matlab/ref/matlab.io.fits.getacolparms.html) | ASCII 表信息                                              |
| [getBColParms](https://www.mathworks.com/help/matlab/ref/matlab.io.fits.getbcolparms.html) | 二进制表信息                                              |
| [getColName](https://www.mathworks.com/help/matlab/ref/matlab.io.fits.getcolname.html)     | 表列名称                                                  |
| [getColType](https://www.mathworks.com/help/matlab/ref/matlab.io.fits.getcoltype.html)     | 数据类型、重复值、缩放列的宽度                            |
| [getEqColType](https://www.mathworks.com/help/matlab/ref/matlab.io.fits.geteqcoltype.html) | 列数据类型、重复值、宽度                                  |
| [getNumCols](https://www.mathworks.com/help/matlab/ref/matlab.io.fits.getnumcols.html)     | 表中的列数                                                |
| [getNumRows](https://www.mathworks.com/help/matlab/ref/matlab.io.fits.getnumrows.html)     | 表中的行数                                                |
| [readATblHdr](https://www.mathworks.com/help/matlab/ref/matlab.io.fits.readatblhdr.html)   | 从当前 ASCII 表读取标头信息                               |
| [readBTblHdr](https://www.mathworks.com/help/matlab/ref/matlab.io.fits.readbtblhdr.html)   | 从当前二进制表读取标头信息                                |
| [readCol](https://www.mathworks.com/help/matlab/ref/matlab.io.fits.readcol.html)           | 读取 ASCII 或二进制表列的行                               |
| [setTscale](https://www.mathworks.com/help/matlab/ref/matlab.io.fits.settscale.html)       | 重置图像缩放                                              |
| [writeCol](https://www.mathworks.com/help/matlab/ref/matlab.io.fits.writecol.html)         | 将元素写入 ASCII 或二进制表列                             |

### FITS 文件 - 实用程序

| -                                                                                                  | -                                          |
| -------------------------------------------------------------------------------------------------- | :----------------------------------------- |
| [getConstantValue](https://www.mathworks.com/help/matlab/ref/matlab.io.fits.getconstantvalue.html) | 指定常量值                                 |
| [getVersion](https://www.mathworks.com/help/matlab/ref/matlab.io.fits.getversion.html)             | CFITSIO 库的修订号                         |
| [getOpenFiles](https://www.mathworks.com/help/matlab/ref/matlab.io.fits.getopenfiles.html)         | 已打开的 FITS 文件列表                     |

### 条带交错文件

| -                                                                               | -                                                  |
| ------------------------------------------------------------------------------- | :------------------------------------------------- |
| [multibandread](https://www.mathworks.com/help/matlab/ref/multibandread.html)   | 从二进制文件读取条带交错文件                       |
| [multibandwrite](https://www.mathworks.com/help/matlab/ref/multibandwrite.html) | 将条带交错数据写入文件                             |

### 通用数据格式 (CDF)

| -                                                                     | -                                                                      |
| --------------------------------------------------------------------- | :--------------------------------------------------------------------- |
| [cdfinfo](https://www.mathworks.com/help/matlab/ref/cdfinfo.html)     | 关于通用数据格式 (CDF) 文件的信息                                      |
| [cdfread](https://www.mathworks.com/help/matlab/ref/cdfread.html)     | 读取通用数据格式 (CDF) 文件中的数据                                    |
| [cdfepoch](https://www.mathworks.com/help/matlab/ref/cdfepoch.html)   | 将日期文字或日期序列值转换为 CDF 格式的日期                            |
| [todatenum](https://www.mathworks.com/help/matlab/ref/todatenum.html) | 将 CDF 纪元对象转换为 `MATLAB` 日期序列值                              |

#### 包

| -                                                               | -                                   |
| --------------------------------------------------------------- | :---------------------------------- |
| [cdflib](https://www.mathworks.com/help/matlab/ref/cdflib.html) | 直接与 CDF 库交互                   |

### 读取视频数据

| -                                                                                           | -                                                              |
| ------------------------------------------------------------------------------------------- | :------------------------------------------------------------- |
| [VideoReader](https://www.mathworks.com/help/matlab/ref/videoreader.html)                   | 创建用于读取视频文件的对象                                     |
| [read](https://www.mathworks.com/help/matlab/ref/videoreader.read.html)                     | 读取一个或多个视频帧                                           |
| [readFrame](https://www.mathworks.com/help/matlab/ref/videoreader.readframe.html)           | 读取下一个视频帧                                               |
| [hasFrame](https://www.mathworks.com/help/matlab/ref/videoreader.hasframe.html)             | 判断是否有可供读取的视频帧                                     |
| [getFileFormats](https://www.mathworks.com/help/matlab/ref/videoreader.getfileformats.html) | `VideoReader` 支持的文件格式                                   |
| [mmfileinfo](https://www.mathworks.com/help/matlab/ref/mmfileinfo.html)                     | 关于多媒体文件的信息                                           |

### 写入视频数据

| -                                                                                     | -                                                             |
| ------------------------------------------------------------------------------------- | :------------------------------------------------------------ |
| [VideoWriter](https://www.mathworks.com/help/matlab/ref/videowriter.html)             | 创建用于写入视频文件的对象                                    |
| [open](https://www.mathworks.com/help/matlab/ref/videowriter.open.html)               | 打开文件以写入视频数据                                        |
| [writeVideo](https://www.mathworks.com/help/matlab/ref/videowriter.writevideo.html)   | 将视频数据写入文件                                            |
| [close](https://www.mathworks.com/help/matlab/ref/videowriter.close.html)             | 写入视频数据后关闭文件                                        |
| [getProfiles](https://www.mathworks.com/help/matlab/ref/videowriter.getprofiles.html) | `VideoWriter` 支持的描述文件和文件格式                        |

### 读取或写入音频

| -                                                                       | -                                            |
| ----------------------------------------------------------------------- | :------------------------------------------- |
| [audioread](https://www.mathworks.com/help/matlab/ref/audioread.html)   | 读取音频文件                                 |
| [audiowrite](https://www.mathworks.com/help/matlab/ref/audiowrite.html) | 写入音频文件                                 |
| [lin2mu](https://www.mathworks.com/help/matlab/ref/lin2mu.html)         | 将线性音频信号转换为 mu-law                  |
| [mu2lin](https://www.mathworks.com/help/matlab/ref/mu2lin.html)         | 将 mu-law 音频信号转换为线性格式             |
| [audioinfo](https://www.mathworks.com/help/matlab/ref/audioinfo.html)   | 关于音频文件的信息                           |

### 播放音频

| -                                                                                       | -                                                                           |
| --------------------------------------------------------------------------------------- | :-------------------------------------------------------------------------- |
| [audioplayer](https://www.mathworks.com/help/matlab/ref/audioplayer.html)               | 用于播放音频的对象                                                          |
| [isplaying](https://www.mathworks.com/help/matlab/ref/audioplayer.isplaying.html)       | 判断播放是否正在进行                                                        |
| [pause](https://www.mathworks.com/help/matlab/ref/audioplayer.pause.html)               | 暂停播放或录制                                                              |
| [play](https://www.mathworks.com/help/matlab/ref/audioplayer.play.html)                 | 从 `audioplayer` 对象播放音频                                               |
| [playblocking](https://www.mathworks.com/help/matlab/ref/audioplayer.playblocking.html) | 在 `audioplayer` 对象中播放音频，保持控制直到播放完成                       |
| [resume](https://www.mathworks.com/help/matlab/ref/audioplayer.resume.html)             | 从暂停状态恢复播放或录制                                                    |
| [stop](https://www.mathworks.com/help/matlab/ref/audioplayer.stop.html)                 | 停止播放或录制                                                              |

### 录制音频

| -                                                                                             | -                                                                                     |
| --------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------ |
| [audiorecorder](https://www.mathworks.com/help/matlab/ref/audiorecorder.html)                 | 用于录制音频的对象                                                                    |
| [getaudiodata](https://www.mathworks.com/help/matlab/ref/audiorecorder.getaudiodata.html)     | 将录制的音频信号存储在数值数组中                                                      |
| [getplayer](https://www.mathworks.com/help/matlab/ref/audiorecorder.getplayer.html)           | 创建关联的 `audioplayer` 对象                                                         |
| [isrecording](https://www.mathworks.com/help/matlab/ref/audiorecorder.isrecording.html)       | 判断录制是否正在进行                                                                  |
| [record](https://www.mathworks.com/help/matlab/ref/audiorecorder.record.html)                 | 将音频录制到 `audiorecorder` 对象中                                                   |
| [recordblocking](https://www.mathworks.com/help/matlab/ref/audiorecorder.recordblocking.html) | 将音频录制到 `audiorecorder` 对象中，保持控制直到录制完成                             |

### 播放声音

| -                                                                             | -                                           |
| ----------------------------------------------------------------------------- | :------------------------------------------ |
| [audiodevinfo](https://www.mathworks.com/help/matlab/ref/audiodevinfo.html)   | 关于音频设备的信息                          |
| [audiodevreset](https://www.mathworks.com/help/matlab/ref/audiodevreset.html) | 刷新可用音频设备列表                        |
| [sound](https://www.mathworks.com/help/matlab/ref/sound.html)                 | 将信号数据矩阵转换为声音                    |
| [soundsc](https://www.mathworks.com/help/matlab/ref/soundsc.html)             | 缩放数据并将其作为声音播放                  |
| [beep](https://www.mathworks.com/help/matlab/ref/beep.html)                   | 生成操作系统蜂鸣声                          |

### 读写 XML 文档

| -                                                                                                                                         | -                                                           |
| ----------------------------------------------------------------------------------------------------------------------------------------- | :---------------------------------------------------------- |
| [matlab.io.xml.dom.DOMWriter](https://www.mathworks.com/help/matlab/ref/matlab.io.xml.dom.domwriter-class.html)                           | 写入序列化 XML 文档注入器                                   |
| [matlab.io.xml.dom.EntityResolver](https://www.mathworks.com/help/matlab/ref/matlab.io.xml.dom.entityresolver-class.html)                 | 实体解析器的抽象基类                                        |
| [matlab.io.xml.dom.FileWriter](https://www.mathworks.com/help/matlab/ref/matlab.io.xml.dom.filewriter-class.html)                         | 用于创建文本文件的写入器                                    |
| [matlab.io.xml.dom.Locator](https://www.mathworks.com/help/matlab/ref/matlab.io.xml.dom.locator-class.html)                               | XML 文件中元素的位置                                        |
| [matlab.io.xml.dom.Parser](https://www.mathworks.com/help/matlab/ref/matlab.io.xml.dom.parser-class.html)                                 | XML 标记解析器                                              |
| [matlab.io.xml.dom.ParserConfiguration](https://www.mathworks.com/help/matlab/ref/matlab.io.xml.dom.parserconfiguration-class.html)       | XML 解析器选项                                              |
| [matlab.io.xml.dom.ParseError](https://www.mathworks.com/help/matlab/ref/matlab.io.xml.dom.parseerror-class.html)                         | 指定的 XML 标记解析错误                                     |
| [matlab.io.xml.dom.ParseErrorHandler](https://www.mathworks.com/help/matlab/ref/matlab.io.xml.dom.parseerrorhandler-class.html)           | 解析错误处理程序的抽象基类                                  |
| [matlab.io.xml.dom.ParseErrorLocator](https://www.mathworks.com/help/matlab/ref/matlab.io.xml.dom.parseerrorlocator-class.html)           | 指定解析错误的位置                                          |
| [matlab.io.xml.dom.ParseErrorSeverity](https://www.mathworks.com/help/matlab/ref/matlab.io.xml.dom.parseerrorseverity-class.html)         | 指示 XML 标记解析错误严重性的枚举类                         |
| [matlab.io.xml.dom.ResourceIdentifier](https://www.mathworks.com/help/matlab/ref/matlab.io.xml.dom.resourceidentifier-class.html)         | XML 资源标识符                                              |
| [matlab.io.xml.dom.ResourceIdentifierType](https://www.mathworks.com/help/matlab/ref/matlab.io.xml.dom.resourceidentifiertype-class.html) | XML 资源标识符类型                                          |
| [matlab.io.xml.dom.WriterConfiguration](https://www.mathworks.com/help/matlab/ref/matlab.io.xml.dom.writerconfiguration-class.html)       | XML DOM 写入器选项                                          |

{.style-list-arrow}

### W3C DOM

| -                                                                                                                                       | -                                    |
| --------------------------------------------------------------------------------------------------------------------------------------- | :----------------------------------- |
| [matlab.io.xml.dom.Attr](https://www.mathworks.com/help/matlab/ref/matlab.io.xml.dom.attr-class.html)                                   | XML 元素的属性                       |
| [matlab.io.xml.dom.CDATASection](https://www.mathworks.com/help/matlab/ref/matlab.io.xml.dom.cdatasection-class.html)                   | CDATA 部分                           |
| [matlab.io.xml.dom.Comment](https://www.mathworks.com/help/matlab/ref/matlab.io.xml.dom.comment-class.html)                             | XML 文档中的注释                     |
| [matlab.io.xml.dom.Document](https://www.mathworks.com/help/matlab/ref/matlab.io.xml.dom.document-class.html)                           | XML 文档                             |
| [matlab.io.xml.dom.DocumentFragment](https://www.mathworks.com/help/matlab/ref/matlab.io.xml.dom.documentfragment-class.html)           | 文档节点组                           |
| [matlab.io.xml.dom.DocumentType](https://www.mathworks.com/help/matlab/ref/matlab.io.xml.dom.documenttype-class.html)                   | 文档类型                             |
| [matlab.io.xml.dom.Element](https://www.mathworks.com/help/matlab/ref/matlab.io.xml.dom.element-class.html)                             | XML 文档的元素                       |
| [matlab.io.xml.dom.Entity](https://www.mathworks.com/help/matlab/ref/matlab.io.xml.dom.entity-class.html)                               | 文档类型定义的实体                   |
| [matlab.io.xml.dom.NamedNodeMap](https://www.mathworks.com/help/matlab/ref/matlab.io.xml.dom.namednodemap-class.html)                   | 一组带名称的文档节点                 |
| [matlab.io.xml.dom.NodeList](https://www.mathworks.com/help/matlab/ref/matlab.io.xml.dom.nodelist-class.html)                           | 文档节点列表                         |
| [matlab.io.xml.dom.Notation](https://www.mathworks.com/help/matlab/ref/matlab.io.xml.dom.notation-class.html)                           | 文档类型定义中的表示法               |
| [matlab.io.xml.dom.ProcessingInstruction](https://www.mathworks.com/help/matlab/ref/matlab.io.xml.dom.processinginstruction-class.html) | XML 处理指令                         |
| [matlab.io.xml.dom.Text](https://www.mathworks.com/help/matlab/ref/matlab.io.xml.dom.text-class.html)                                   | XML 文档中的文本                     |
| [matlab.io.xml.dom.TypeInfo](https://www.mathworks.com/help/matlab/ref/matlab.io.xml.dom.typeinfo-class.html)                           | 模式类型信息                         |

{.style-list-arrow}

### XML 转换

| -                                                                                                                                                         | -                                             |
| --------------------------------------------------------------------------------------------------------------------------------------------------------- | :-------------------------------------------- |
| [matlab.io.xml.transform.CompiledStylesheet](https://www.mathworks.com/help/matlab/ref/matlab.io.xml.transform.compiledstylesheet-class.html)             | 编译的样式表                                  |
| [matlab.io.xml.transform.ResultDocument](https://www.mathworks.com/help/matlab/ref/matlab.io.xml.transform.resultdocument-class.html)                     | 将转换结果存储为文档                          |
| [matlab.io.xml.transform.ResultString](https://www.mathworks.com/help/matlab/ref/matlab.io.xml.transform.resultstring-class.html)                         | 将转换结果存储为字符串                        |
| [matlab.io.xml.transform.ResultFile](https://www.mathworks.com/help/matlab/ref/matlab.io.xml.transform.resultfile-class.html)                             | 将转换结果存储为文件                          |
| [matlab.io.xml.transform.SourceDocument](https://www.mathworks.com/help/matlab/ref/matlab.io.xml.transform.sourcedocument-class.html)                     | 用于转换的 XML 源文档                         |
| [matlab.io.xml.transform.SourceFile](https://www.mathworks.com/help/matlab/ref/matlab.io.xml.transform.sourcefile-class.html)                             | 用于转换的 XML 源文件                         |
| [matlab.io.xml.transform.SourceString](https://www.mathworks.com/help/matlab/ref/matlab.io.xml.transform.sourcestring-class.html)                         | 用于转换字符串的 XML 源字符串                 |
| [matlab.io.xml.transform.StylesheetSourceDocument](https://www.mathworks.com/help/matlab/ref/matlab.io.xml.transform.stylesheetsourcedocument-class.html) | 用于转换文档的样式表源                        |
| [matlab.io.xml.transform.StylesheetSourceFile](https://www.mathworks.com/help/matlab/ref/matlab.io.xml.transform.stylesheetsourcefile-class.html)         | 用于转换文档的样式表源                        |
| [matlab.io.xml.transform.StylesheetSourceString](https://www.mathworks.com/help/matlab/ref/matlab.io.xml.transform.stylesheetsourcestring-class.html)     | 用于转换字符串的 XSL 源字符串                 |
| [matlab.io.xml.transform.Tracer](https://www.mathworks.com/help/matlab/ref/matlab.io.xml.transform.tracer-class.html)                                     | 跟踪样式表的执行                              |

{.style-list-arrow}

### XPath 查询

| -                                                                                                                                     | -                                                     |
| ------------------------------------------------------------------------------------------------------------------------------------- | :---------------------------------------------------- |
| [matlab.io.xml.xpath.CompiledExpression](https://www.mathworks.com/help/matlab/ref/matlab.io.xml.xpath.compiledexpression-class.html) | 编译的 XPath 表达式                                   |
| [matlab.io.xml.xpath.EvalResultType](https://www.mathworks.com/help/matlab/ref/matlab.io.xml.xpath.evalresulttype-class.html)         | XPath 表达式计算的结果类型                            |
| [matlab.io.xml.xpath.Evaluator](https://www.mathworks.com/help/matlab/ref/matlab.io.xml.xpath.evaluator-class.html)                   | XPath 表达式求值器                                    |
| [matlab.io.xml.xpath.PrefixResolver](https://www.mathworks.com/help/matlab/ref/matlab.io.xml.xpath.prefixresolver-class.html)         | 命名空间前缀解析器的抽象基类                          |

{.style-list-arrow}

### JSON 格式

| -                                                                       | -                                                        |
| ----------------------------------------------------------------------- | :------------------------------------------------------- |
| [jsondecode](https://www.mathworks.com/help/matlab/ref/jsondecode.html) | 解码 JSON 格式的文本                                     |
| [jsonencode](https://www.mathworks.com/help/matlab/ref/jsonencode.html) | 从结构化 `MATLAB` 数据创建 JSON 格式的文本               |

### 工作区变量和 MAT 文件 {.row-span-2}

| -                                                                                           | -                                                                                 |
| ------------------------------------------------------------------------------------------- | :-------------------------------------------------------------------------------- |
| [load](https://www.mathworks.com/help/matlab/ref/load.html)                                 | 将文件变量加载到工作区                                                            |
| [save](https://www.mathworks.com/help/matlab/ref/save.html)                                 | 将工作区变量保存到文件                                                            |
| [matfile](https://www.mathworks.com/help/matlab/ref/matlab.io.matfile.html)                 | 访问和更改 MAT 文件中的变量，而无需将文件加载到内存中                               |
| [disp](https://www.mathworks.com/help/matlab/ref/disp.html)                                 | 显示变量的值                                                                      |
| [formattedDisplayText](https://www.mathworks.com/help/matlab/ref/formatteddisplaytext.html) | 将显示输出捕获为字符串                                                            |
| [who](https://www.mathworks.com/help/matlab/ref/who.html)                                   | 列出工作区中的变量                                                                |
| [whos](https://www.mathworks.com/help/matlab/ref/whos.html)                                 | 列出工作区中的变量及其大小和类型                                                  |
| [clear](https://www.mathworks.com/help/matlab/ref/clear.html)                               | 从工作区删除项目并释放系统内存                                                    |
| [clearvars](https://www.mathworks.com/help/matlab/ref/clearvars.html)                       | 清除内存中的变量                                                                  |
| [openvar](https://www.mathworks.com/help/matlab/ref/openvar.html)                           | 在变量编辑器或其他图形编辑工具中打开工作区变量                                    |
| [工作区浏览器](https://www.mathworks.com/help/matlab/ref/workspace.html)                    | 打开工作区浏览器以管理工作区                                                      |

### 低级文件 I/O {.row-span-2}

| -                                                                   | -                                                                    |
| ------------------------------------------------------------------- | :------------------------------------------------------------------- |
| [fclose](https://www.mathworks.com/help/matlab/ref/fclose.html)     | 关闭一个或所有打开的文件                                             |
| [feof](https://www.mathworks.com/help/matlab/ref/feof.html)         | 检测文件末尾                                                         |
| [ferror](https://www.mathworks.com/help/matlab/ref/ferror.html)     | 文件 I/O 错误消息                                                    |
| [fgetl](https://www.mathworks.com/help/matlab/ref/fgetl.html)       | 读取文件中的行并删除换行符                                           |
| [fgets](https://www.mathworks.com/help/matlab/ref/fgets.html)       | 读取文件中的行并保留换行符                                           |
| [fileread](https://www.mathworks.com/help/matlab/ref/fileread.html) | 以文本格式读取文件内容                                               |
| [fopen](https://www.mathworks.com/help/matlab/ref/fopen.html)       | 打开文件或获取有关打开文件的信息                                     |
| [fprintf](https://www.mathworks.com/help/matlab/ref/fprintf.html)   | 将数据写入文本文件                                                   |
| [fread](https://www.mathworks.com/help/matlab/ref/fread.html)       | 读取二进制文件中的数据                                               |
| [frewind](https://www.mathworks.com/help/matlab/ref/frewind.html)   | 将文件位置指示器移动到打开文件的开头                                 |
| [fscanf](https://www.mathworks.com/help/matlab/ref/fscanf.html)     | 读取文本文件中的数据                                                 |
| [fseek](https://www.mathworks.com/help/matlab/ref/fseek.html)       | 移动到文件中的指定位置                                               |
| [ftell](https://www.mathworks.com/help/matlab/ref/ftell.html)       | 当前位置                                                             |
| [fwrite](https://www.mathworks.com/help/matlab/ref/fwrite.html)     | 将数据写入二进制文件                                                 |

### 串行和 USB 通信 - 连接和配置

| -                                                                                                    | -                                                                                       |
| ---------------------------------------------------------------------------------------------------- | :-------------------------------------------------------------------------------------- |
| [serialportlist](https://www.mathworks.com/help/matlab/ref/serialportlist.html)                      | 连接到系统的串行端口列表                                                                |
| [serialport](https://www.mathworks.com/help/matlab/ref/serialport.html)                              | 连接到串行端口                                                                          |
| [configureTerminator](https://www.mathworks.com/help/matlab/ref/serialport.configureterminator.html) | 设置与串行端口进行 ASCII 字符串通信的终止符                                             |
| [configureCallback](https://www.mathworks.com/help/matlab/ref/serialport.configurecallback.html)     | 设置与串行端口设备通信的回调函数和触发条件                                              |

### 串行和 USB 通信 - 读取和写入

| -                                                                                | -                                            |
| -------------------------------------------------------------------------------- | :------------------------------------------- |
| [read](https://www.mathworks.com/help/matlab/ref/serialport.read.html)           | 从串行端口读取数据                           |
| [readline](https://www.mathworks.com/help/matlab/ref/serialport.readline.html)   | 从串行端口读取 ASCII 字符串数据行            |
| [write](https://www.mathworks.com/help/matlab/ref/serialport.write.html)         | 将数据写入串行端口                           |
| [writeline](https://www.mathworks.com/help/matlab/ref/serialport.writeline.html) | 将 ASCII 数据行写入串行端口                  |

### 串行和 USB 通信 - 控制引脚和内存

| -                                                                                      | -                                   |
| -------------------------------------------------------------------------------------- | :---------------------------------- |
| [flush](https://www.mathworks.com/help/matlab/ref/serialport.flush.html)               | 清除串行端口设备缓冲区              |
| [getpinstatus](https://www.mathworks.com/help/matlab/ref/serialport.getpinstatus.html) | 获取串行端口状态                    |
| [setRTS](https://www.mathworks.com/help/matlab/ref/serialport.setrts.html)             | 设置串行端口 RTS 引脚               |
| [setDTR](https://www.mathworks.com/help/matlab/ref/serialport.setdtr.html)             | 设置串行 DTR 引脚                   |

### TCP/IP 通信 - 连接和配置

| -                                                                                                   | -                                                                                         |
| --------------------------------------------------------------------------------------------------- | :---------------------------------------------------------------------------------------- |
| [tcpclient](https://www.mathworks.com/help/matlab/ref/tcpclient.html)                               | 创建到 TCP/IP 服务器的 TCP/IP 客户端连接                                                  |
| [echotcpip](https://www.mathworks.com/help/matlab/ref/echotcpip.html)                               | 启动或停止 TCP/IP 回显服务器                                                              |
| [configureTerminator](https://www.mathworks.com/help/matlab/ref/tcpclient.configureterminator.html) | 设置通过 TCP/IP 与远程主机进行 ASCII 字符串通信的终止符                                   |
| [configureCallback](https://www.mathworks.com/help/matlab/ref/tcpclient.configurecallback.html)     | 设置通过 TCP/IP 与远程主机通信的回调函数和触发条件                                        |

{.style-list}

### TCP/IP 通信 - 读取和写入

| -                                                                               | -                                                            |
| ------------------------------------------------------------------------------- | :----------------------------------------------------------- |
| [read](https://www.mathworks.com/help/matlab/ref/tcpclient.read.html)           | 通过 TCP/IP 读取远程主机上的数据                             |
| [readline](https://www.mathworks.com/help/matlab/ref/tcpclient.readline.html)   | 通过 TCP/IP 从远程主机读取 ASCII 字符串数据行                |
| [write](https://www.mathworks.com/help/matlab/ref/tcpclient.write.html)         | 通过 TCP/IP 将数据写入远程主机                               |
| [writeline](https://www.mathworks.com/help/matlab/ref/tcpclient.writeline.html) | 通过 TCP/IP 将 ASCII 数据行写入远程主机                      |
| [flush](https://www.mathworks.com/help/matlab/ref/tcpclient.flush.html)         | 清除通过 TCP/IP 与远程主机通信的缓冲区                       |

{.style-list}

### 蓝牙通信 - 连接和配置

| -                                                                                                   | -                                                                                     |
| --------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------ |
| [bluetoothlist](https://www.mathworks.com/help/matlab/ref/bluetoothlist.html)                       | 扫描附近的 `蓝牙` 经典设备                                                            |
| [bluetooth](https://www.mathworks.com/help/matlab/ref/bluetooth.html)                               | 连接到 `蓝牙` 经典设备                                                                |
| [configureTerminator](https://www.mathworks.com/help/matlab/ref/bluetooth.configureterminator.html) | 设置与 `蓝牙` 设备进行 ASCII 字符串通信的终止符                                         |
| [configureCallback](https://www.mathworks.com/help/matlab/ref/bluetooth.configurecallback.html)     | 设置与 `蓝牙` 设备通信的回调函数和触发条件                                              |

{.style-list}

### 蓝牙通信 - 读取和写入 {.row-span-2}

| -                                                                               | -                                                   |
| ------------------------------------------------------------------------------- | :-------------------------------------------------- |
| [read](https://www.mathworks.com/help/matlab/ref/bluetooth.read.html)           | 从 `蓝牙` 设备读取数据                              |
| [readline](https://www.mathworks.com/help/matlab/ref/bluetooth.readline.html)   | 从 `蓝牙` 设备读取 ASCII 字符串数据行               |
| [write](https://www.mathworks.com/help/matlab/ref/bluetooth.write.html)         | 将数据写入 `蓝牙` 设备                              |
| [writeline](https://www.mathworks.com/help/matlab/ref/bluetooth.writeline.html) | 将 ASCII 数据行写入 `蓝牙` 设备                     |
| [flush](https://www.mathworks.com/help/matlab/ref/bluetooth.flush.html)         | 清除 `蓝牙` 设备缓冲区                              |

{.style-list}

### 蓝牙低功耗通信 {.row-span-2}

| -                                                                                                            | -                                                                                          |
| ------------------------------------------------------------------------------------------------------------ | :----------------------------------------------------------------------------------------- |
| [blelist](https://www.mathworks.com/help/matlab/ref/blelist.html)                                            | 扫描附近的低功耗 `蓝牙` 外围设备                                                           |
| [ble](https://www.mathworks.com/help/matlab/ref/ble.html)                                                    | 连接到低功耗 `蓝牙` 外围设备                                                               |
| [characteristic](https://www.mathworks.com/help/matlab/ref/matlabshared.blelib.characteristic.html)          | 访问 `蓝牙` 低功耗外围设备的特征                                                           |
| [descriptor](https://www.mathworks.com/help/matlab/ref/matlabshared.blelib.descriptor.html)                  | 访问 `蓝牙` 低功耗外围设备上的描述符                                                       |
| [read](https://www.mathworks.com/help/matlab/ref/matlabshared.blelib.characteristic.read.html)               | 读取 `蓝牙` 低功耗外围设备上的特征或描述符数据                                               |
| [write](https://www.mathworks.com/help/matlab/ref/matlabshared.blelib.characteristic.write.html)             | 将数据写入 `蓝牙` 低功耗外围设备的特征或描述符                                               |
| [subscribe](https://www.mathworks.com/help/matlab/ref/matlabshared.blelib.characteristic.subscribe.html)     | 订阅特征通知或指示                                                                         |
| [unsubscribe](https://www.mathworks.com/help/matlab/ref/matlabshared.blelib.characteristic.unsubscribe.html) | 取消订阅特征通知和指示                                                                     |

{.style-list}

### Web 服务

| -                                                                       | -                                           |
| ----------------------------------------------------------------------- | :------------------------------------------ |
| [webread](https://www.mathworks.com/help/matlab/ref/webread.html)       | 从 RESTful Web 服务读取内容                 |
| [webwrite](https://www.mathworks.com/help/matlab/ref/webwrite.html)     | 将数据写入 RESTful Web 服务                 |
| [websave](https://www.mathworks.com/help/matlab/ref/websave.html)       | 将 RESTful Web 服务中的内容保存到文件       |
| [weboptions](https://www.mathworks.com/help/matlab/ref/weboptions.html) | 指定 RESTful Web 服务的参数                 |
| [web](https://www.mathworks.com/help/matlab/ref/web.html)               | 在浏览器中打开网页或文件                    |
| [sendmail](https://www.mathworks.com/help/matlab/ref/sendmail.html)     | 向地址列表发送电子邮件                      |

### FTP 文件操作 {.row-span-2}

| -                                                                   | -                                                          |
| ------------------------------------------------------------------- | :--------------------------------------------------------- |
| [ftp](https://www.mathworks.com/help/matlab/ref/ftp.html)           | 连接到 FTP 服务器以访问其文件                              |
| [sftp](https://www.mathworks.com/help/matlab/ref/sftp.html)         | 连接到 SFTP 服务器以访问其文件                             |
| [ascii](https://www.mathworks.com/help/matlab/ref/ftp.ascii.html)   | 将 FTP 传输模式设置为 ASCII                                |
| [binary](https://www.mathworks.com/help/matlab/ref/ftp.binary.html) | 将 FTP 传输模式设置为二进制                                |
| [cd](https://www.mathworks.com/help/matlab/ref/ftp.cd.html)         | 更改或查看 SFTP 或 FTP 服务器上的当前文件夹                |
| [close](https://www.mathworks.com/help/matlab/ref/ftp.close.html)   | 关闭与 SFTP 或 FTP 服务器的连接                            |
| [delete](https://www.mathworks.com/help/matlab/ref/ftp.delete.html) | 删除 SFTP 或 FTP 服务器上的文件                            |
| [dir](https://www.mathworks.com/help/matlab/ref/ftp.dir.html)       | 列出 SFTP 或 FTP 服务器上的文件夹内容                      |
| [mget](https://www.mathworks.com/help/matlab/ref/ftp.mget.html)     | 从 SFTP 或 FTP 服务器下载文件                              |
| [mkdir](https://www.mathworks.com/help/matlab/ref/ftp.mkdir.html)   | 在 SFTP 或 FTP 服务器上创建新文件夹                        |
| [mput](https://www.mathworks.com/help/matlab/ref/ftp.mput.html)     | 将文件或文件夹上传到 SFTP 或 FTP 服务器                    |
| [rename](https://www.mathworks.com/help/matlab/ref/ftp.rename.html) | 重命名 SFTP 或 FTP 服务器上的文件                          |
| [rmdir](https://www.mathworks.com/help/matlab/ref/ftp.rmdir.html)   | 删除 SFTP 或 FTP 服务器上的文件夹                          |

### 物联网 (IoT) 数据

| -                                                                                 | -                                        |
| --------------------------------------------------------------------------------- | :--------------------------------------- |
| [thingSpeakRead](https://www.mathworks.com/help/matlab/ref/thingspeakread.html)   | 读取存储在 `ThingSpeak` 通道中的数据     |
| [thingSpeakWrite](https://www.mathworks.com/help/matlab/ref/thingspeakwrite.html) | 将数据写入 `ThingSpeak` 通道             |

