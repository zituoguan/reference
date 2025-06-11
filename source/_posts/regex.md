---
title: 正则表达式 (RegEX)
date: 2020-11-25 18:28:43
background: bg-[#e56d2d]
tags:
  - 正则表达式
  - regexp
  - 模式
categories:
  - 工具箱
intro: |
  正则表达式 (regex) 快速参考，包括符号、范围、分组、断言以及一些入门示例模式。
plugins:
  - copyCode
---

<!-- 编者注：此页面使用 <yel> (黄色 tailwind span) 为匹配文本着色，使用 <red> 为不匹配文本着色 -->

## 入门指南

### 简介

这是一个正则表达式入门的快速备忘单。

- [Python 中的 Regex](#regex-in-python) _(r3f.cn)_
- [JavaScript 中的 Regex](#regex-in-javascript) _(r3f.cn)_
- [PHP 中的 Regex](#regex-in-php) _(r3f.cn)_
- [Java 中的 Regex](#regex-in-java) _(r3f.cn)_
- [MySQL 中的 Regex](#regex-in-mysql) _(r3f.cn)_
- [Vim 中的 Regex](/vim#search-and-replace) _(r3f.cn)_
- [Emacs 中的 Regex](/emacs#search) _(r3f.cn)_
- [在线 regex 测试器](https://regex101.com/) _(regex101.com)_

{.cols-2 .marker-round}

### 字符类

| 模式          | 描述                                                                       |
| ------------- | :------------------------------------------------------------------------- |
| `[abc]`       | 单个字符：<yel>a</yel>、<yel>b</yel> 或 <yel>c</yel>                         |
| `[^abc]`      | 除 <yel>a</yel>、<yel>b</yel> 或 <yel>c</yel> 之外的字符                    |
| `[a-z]`       | 范围内的字符：<yel>a-z</yel>                                                  |
| `[^a-z]`      | 不在范围内的字符：<red>a-z</red>                                              |
| `[0-9]`       | 范围内的数字：<yel>0-9</yel>                                                  |
| `[a-zA-Z]`    | 范围内的字符：<yel>a-z</yel> 或 <yel>A-Z</yel>                               |
| `[a-zA-Z0-9]` | 范围内的字符：<yel>a-z</yel>、<yel>A-Z</yel> 或 <yel>0-9</yel>                |

{.style-list}

### 量词

| 模式     | 描述              |
| -------- | :-------------------- |
| `a?`     | 零个或一个 a          |
| `a*`     | 零个或多个 a          |
| `a+`     | 一个或多个 a          |
| `[0-9]+` | 一个或多个 0-9       |
| `a{3}`   | 正好 3 个 a         |
| `a{3,}`  | 3 个或更多个 a        |
| `a{3,6}` | 3 到 6 个 a 之间    |
| `a*`     | 贪婪量词            |
| `a*?`    | 懒惰量词            |
| `a*+`    | 独占量词            |

### 常用元字符
| 模式     | 描述                                       |
| -------- | :----------------------------------------- |
| `^`      | 匹配字符串的开头。                             |
| `{`      | 开始一个量词，用于指定出现次数。                   |
| `+`      | 匹配前一个元素一次或多次。                       |
| `<`      | 不是标准的 regex 元字符（常用于 HTML）。          |
| `[`      | 开始一个字符类。                               |
| `*`      | 匹配前一个元素零次或多次。                       |
| `)`      | 结束一个捕获组。                               |
| `>`      | 不是标准的 regex 元字符（常用于 HTML）。          |
| `.`      | 匹配除换行符以外的任何字符。                     |
| `(`      | 开始一个捕获组。                               |
| `|`      | 在 regex 模式中充当逻辑或。                    |
| `$`      | 匹配字符串的结尾。                             |
| `\`      | 转义一个元字符，使其具有字面意义。                 |
| `?`      | 匹配前一个元素零次或一次。                       |

{.cols-3 .marker-none}

使用 `\` 转义这些特殊字符

### 元序列 {.row-span-4}

| 模式         | 描述                                                        |
| ------------ | :---------------------------------------------------------- |
| `.`          | 任何单个字符                                                |
| `\s`         | 任何空白字符                                                |
| `\S`         | 任何非空白字符                                              |
| `\d`         | 任何数字，与 [0-9] 相同                                     |
| `\D`         | 任何非数字字符，与 [^0-9] 相同                               |
| `\w`         | 任何单词字符                                                |
| `\W`         | 任何非单词字符                                              |
| `\X`         | 任何 Unicode 序列，包括换行符                               |
| `\C`         | 匹配一个数据单元                                            |
| `\R`         | Unicode 换行符                                              |
| `\v`         | 垂直空白字符                                                |
| `\V`         | \v 的否定 - 除换行符和垂直制表符外的任何字符                  |
| `\h`         | 水平空白字符                                                |
| `\H`         | \h 的否定                                                   |
| `\K`         | 重置匹配                                                    |
| `\n`         | 匹配第 n 个子模式                                           |
| `\pX`        | Unicode 属性 X                                              |
| `\p{...}`    | Unicode 属性或脚本类别                                      |
| `\PX`        | \pX 的否定                                                  |
| `\P{...}`    | \p 的否定                                                   |
| `\Q...\E`    | 引号；视为字面量                                            |
| `\k<name>`   | 匹配名为 `name` 的子模式                                    |
| `\k'name'`   | 匹配名为 `name` 的子模式                                    |
| `\k{name}`   | 匹配名为 `name` 的子模式                                    |
| `\gn`        | 匹配第 n 个子模式                                           |
| `\g{n}`      | 匹配第 n 个子模式                                           |
| `\g<n>`      | 递归第 n 个捕获组                                           |
| `\g'n'`      | 递归第 n 个捕获组                                           |
| `\g{-n}`     | 匹配第 n 个相对前一个子模式                                 |
| `\g<+n>`     | 递归第 n 个相对后一个子模式                                 |
| `\g'+n'`     | 匹配第 n 个相对后一个子模式                                 |
| `\g'letter'` | 递归名为 `letter` 的捕获组                                  |
| `\g{letter}` | 匹配先前命名的捕获组 `letter`                               |
| `\g<letter>` | 递归名为 `letter` 的捕获组                                  |
| `\xYY`       | 十六进制字符 YY                                             |
| `\x{YYYY}`   | 十六进制字符 YYYY                                           |
| `\ddd`       | 八进制字符 ddd                                              |
| `\cY`        | 控制字符 Y                                                  |
| `[\b]`       | 退格字符                                                    |
| `\`          | 使任何字符成为字面量                                        |

### 锚点

| 模式    | 描述                   |
| ------- | :--------------------- |
| `\G`    | 匹配的开始             |
| `^`     | 字符串的开始           |
| `$`     | 字符串的结束           |
| `\A`    | 字符串的开始           |
| `\Z`    | 字符串的结束           |
| `\z`    | 字符串的绝对结束       |
| `\b`    | 单词边界               |
| `\B`    | 非单词边界             |

### 替换

| 模式       | 描述                        |
| ---------- | :------------------------------ |
| `\0`       | 完整匹配内容                    |
| `\1`       | 捕获组 1 中的内容               |
| `$1`       | 捕获组 1 中的内容               |
| `${foo}`   | 捕获组 `foo` 中的内容           |
| `\x20`     | 十六进制替换值                  |
| `\x{06fa}` | 十六进制替换值                  |
| `\t`       | 制表符                          |
| `\r`       | 回车符                          |
| `\n`       | 换行符                          |
| `\f`       | 换页符                          |
| `\U`       | 大写转换                        |
| `\L`       | 小写转换                        |
| `\E`       | 终止任何转换                    |

### 分组构造

| 模式                  | 描述                              |
| --------------------- | :------------------------------------ |
| `(...)`               | 捕获所有括起来的内容                  |
| <code>(a\|b)</code>   | 匹配 a 或 b                         |
| `(?:...)`             | 匹配所有括起来的内容（非捕获）        |
| `(?>...)`             | 原子组（非捕获）                      |
| <code>(?\|...)</code> | 重复子模式组号                      |
| `(?#...)`             | 注释                                |
| `(?'name'...)`        | 命名捕获组                          |
| `(?<name>...)`        | 命名捕获组                          |
| `(?P<name>...)`       | 命名捕获组                          |
| `(?imsxXU)`           | 内联修饰符                          |
| `(?(DEFINE)...)`      | 在使用前预定义模式                    |

### 断言

| -                               | -                               |
| ------------------------------- | :------------------------------ |
| <code>(?(1)yes\|no)</code>      | 条件语句                          |
| <code>(?(R)yes\|no)</code>      | 条件语句                          |
| <code>(?(R#)yes\|no)</code>     | 递归条件语句                      |
| <code>(?(R&name\yes\|no)</code> | 条件语句                          |
| <code>(?(?=...)yes\|no)</code>  | 前瞻条件                          |
| <code>(?(?<=...)yes\|no)</code> | 后顾条件                          |

### 环视 (Lookarounds)

| -          | -                   |
| ---------- | :------------------ |
| `(?=...)`  | 正向前瞻            |
| `(?!...)`  | 负向前瞻            |
| `(?<=...)` | 正向后顾            |
| `(?<!...)` | 负向后顾            |

环视允许您在主模式之前（后顾）或之后（前瞻）匹配一个组，而不将其包含在结果中。

### 标志/修饰符

| 模式    | 描述                  |
| ------- | :-------------------- |
| `g`     | 全局匹配              |
| `m`     | 多行模式              |
| `i`     | 不区分大小写          |
| `x`     | 忽略空白              |
| `s`     | 单行模式              |
| `u`     | Unicode               |
| `X`     | 扩展模式 (eXtended)   |
| `U`     | 非贪婪模式            |
| `A`     | 锚定模式              |
| `J`     | 重复组名              |

### 递归

| -           | -                                 |
| ----------- | :-------------------------------- |
| `(?R)`      | 递归整个模式                      |
| `(?1)`      | 递归第一个子模式                  |
| `(?+1)`     | 递归第一个相对子模式              |
| `(?&name)`  | 递归名为 `name` 的子模式          |
| `(?P=name)` | 匹配名为 `name` 的子模式          |
| `(?P>name)` | 递归名为 `name` 的子模式          |

### POSIX 字符类 {.col-span-2}

| 字符类          | 等同于                                             | 含义                           |
| --------------- | -------------------------------------------------- | :----------------------------- |
| `[[:alnum:]]`   | `[0-9A-Za-z]`                                      | 字母和数字                     |
| `[[:alpha:]]`   | `[A-Za-z]`                                         | 字母                           |
| `[[:ascii:]]`   | `[\x00-\x7F]`                                      | ASCII 码 0-127                 |
| `[[:blank:]]`   | `[\t ]`                                            | 仅空格或制表符                 |
| `[[:cntrl:]]`   | `[\x00-\x1F\x7F]`                                  | 控制字符                       |
| `[[:digit:]]`   | `[0-9]`                                            | 十进制数字                     |
| `[[:graph:]]`   | `[[:alnum:][:punct:]]`                             | 可见字符（非空格）             |
| `[[:lower:]]`   | `[a-z]`                                            | 小写字母                       |
| `[[:print:]]`   | `[ -~] == [ [:graph:]]`                            | 可见字符                       |
| `[[:punct:]]`   | <code>[!"#$%&’()\*+,-./:;<=>?@[]^\_\`{\|}~]</code> | 可见标点字符                   |
| `[[:space:]]`   | <code>[\t\n\v\f\r ]</code>                         | 空白字符                       |
| `[[:upper:]]`   | `[A-Z]`                                            | 大写字母                       |
| `[[:word:]]`    | `[0-9A-Za-z_]`                                     | 单词字符                       |
| `[[:xdigit:]]`  | `[0-9A-Fa-f]`                                      | 十六进制数字                   |
| `[[:<:]]`       | `[\b(?=\w)]`                                       | 单词开头                       |
| `[[:>:]]`       | `[\b(?<=\w)]`                                      | 单词结尾                       |

{.show-header}

### 控制动词

| -                      | -                     |
| ---------------------- | :-------------------- |
| `(*ACCEPT)`            | 控制动词              |
| `(*FAIL)`              | 控制动词              |
| `(*MARK:NAME)`         | 控制动词              |
| `(*COMMIT)`            | 控制动词              |
| `(*PRUNE)`             | 控制动词              |
| `(*SKIP)`              | 控制动词              |
| `(*THEN)`              | 控制动词              |
| `(*UTF)`               | 模式修饰符            |
| `(*UTF8)`              | 模式修饰符            |
| `(*UTF16)`             | 模式修饰符            |
| `(*UTF32)`             | 模式修饰符            |
| `(*UCP)`               | 模式修饰符            |
| `(*CR)`                | 换行符修饰符          |
| `(*LF)`                | 换行符修饰符          |
| `(*CRLF)`              | 换行符修饰符          |
| `(*ANYCRLF)`           | 换行符修饰符          |
| `(*ANY)`               | 换行符修饰符          |
| `\R`                   | 换行符修饰符          |
| `(*BSR_ANYCRLF)`       | 换行符修饰符          |
| `(*BSR_UNICODE)`       | 换行符修饰符          |
| `(*LIMIT_MATCH=x)`     | 正则表达式引擎修饰符  |
| `(*LIMIT_RECURSION=d)` | 正则表达式引擎修饰符  |
| `(*NO_AUTO_POSSESS)`   | 正则表达式引擎修饰符  |
| `(*NO_START_OPT)`      | 正则表达式引擎修饰符  |

## 正则表达式示例 {.cols-3}

### 字符

| 模式           | 匹配                                                      |
| -------------- | :-------------------------------------------------------- |
| `ring        ` | 匹配 <yel>ring</yel> sp<yel>ring</yel>board 等。         |
| `.           ` | 匹配 <yel>a</yel>, <yel>9</yel>, <yel>+</yel> 等。       |
| `h.o         ` | 匹配 <yel>hoo</yel>, <yel>h2o</yel>, <yel>h/o</yel> 等。 |
| `ring\?      ` | 匹配 <yel>ring?</yel>                                    |
| `\(quiet\)   ` | 匹配 <yel>(quiet)</yel>                                  |
| `c:\\windows ` | 匹配 <yel>c:\windows</yel>                               |

使用 `\` 搜索这些特殊字符：<br> `[ \ ^ $ . | ? * + ( ) { }`

### 多选分支 (Alternatives)

| 模式                      | 匹配                                       |
| ------------------------- | :----------------------------------------- |
| <code>cat\|dog</code>     | 匹配 <yel>cat</yel> 或 <yel>dog</yel>     |
| <code>id\|identity</code> | 匹配 <yel>id</yel> 或 <yel>id</yel>entity |
| <code>identity\|id</code> | 匹配 <yel>id</yel> 或 <yel>identity</yel> |

当多选分支重叠时，按从长到短的顺序排列

### 字符类

| 模式              | 匹配                                                                   |
| ----------------- | :--------------------------------------------------------------------- |
| `[aeiou]`         | 匹配任何元音字母                                                       |
| `[^aeiou]`        | 匹配任何非元音字母                                                     |
| `r[iau]ng`        | 匹配 <yel>ring</yel>, w<yel>rang</yel>le, sp<yel>rung</yel>, 等。     |
| `gr[ae]y`         | 匹配 <yel>gray</yel> 或 <yel>grey</yel>                               |
| `[a-zA-Z0-9]`     | 匹配任何字母或数字                                                     |
| `[\u3a00-\ufa99]` | 匹配任何 [Unicode 韩字 (中文)](https://unicode.org/charts/unihan.html) |

在 `[ ]` 中总是转义 `. \ ]`，有时转义 `^ - .`

### 简写类

| 模式             | 含义                                                  |
| ---------------- | :---------------------------------------------------- |
| `\w            ` | “单词”字符 <br>_(字母、数字或下划线)_                  |
| `\d            ` | 数字                                                  |
| `\s            ` | 空白字符 <br>_(空格、制表符、垂直制表符、换行符)_      |
| `\W, \D, or \S ` | 非单词、非数字或非空白字符                            |
| `[\D\S]        ` | 表示非数字或非空白，两者都匹配                        |
| `[^\d\s]       ` | 不允许数字和空白字符                                  |

### 出现次数

| 模式                | 匹配                                                               |
| ------------------- | :----------------------------------------------------------------- |
| `colou?r`           | 匹配 <yel>color</yel> 或 <yel>colour</yel>                        |
| `[BW]ill[ieamy's]*` | 匹配 <yel>Bill</yel>, <yel>Willy</yel>, <yel>William's</yel> 等。 |
| `[a-zA-Z]+`         | 匹配 1 个或多个字母                                                |
| `\d{3}-\d{2}-\d{4}` | 匹配社会安全号码 (SSN)                                             |
| `[a-z]\w{1,7}`      | 匹配 UW NetID                                                      |

### 贪婪与懒惰

| 模式                     | 含义                                                    |
| ------------------------ | :------------------------------------------------------ |
| `*  + {n,}`<br>_贪婪_    | 尽可能多地匹配                                          |
| `<.+>   `                | 在 <yel>\<b>bold\<\/b></yel> 中找到 1 个大的匹配        |
| `*?  +? {n,}?`<br>_懒惰_ | 尽可能少地匹配                                          |
| `<.+?>`                  | 在 \<<yel>b</yel>>bold\<<yel>\/b</yel>> 中找到 2 个匹配 |

### 范围 (Scope) {.col-span-2}

| 模式               | 含义                                                                                    |
| ------------------ | :-------------------------------------------------------------------------------------- |
| `\b              ` | “单词”边界 (与非“单词”字符相邻)                                                         |
| `\bring          ` | 以 "ring" 开头的单词，例如 <yel>ringtone</yel>                                          |
| `ring\b          ` | 以 "ring" 结尾的单词，例如 <yel>spring</yel>                                            |
| `\b9\b           ` | 匹配单个数字 <yel>9</yel>，而不是 <red>19</red>、<red>91</red>、<red>99</red> 等。      |
| `\b[a-zA-Z]{6}\b ` | 匹配 6 个字母的单词                                                                     |
| `\B              ` | 非单词边界                                                                              |
| `\Bring\B        ` | 匹配 <yel>springs</yel> 和 <yel>wringer</yel>                                         |
| `^\d*$           ` | 整个字符串必须是数字                                                                    |
| `^[a-zA-Z]{4,20}$` | 字符串必须有 4-20 个字母                                                                |
| `^[A-Z]          ` | 字符串必须以大写字母开头                                                                |
| `[\.!?"')]$      ` | 字符串必须以终端标点符号结尾                                                            |

### 修饰符

| 模式                 | 含义                                                     |
| -------------------- | :------------------------------------------------------- |
| `(?i)`[a-z]\*`(?-i)` | 忽略大小写 开 / 关                                       |
| `(?s)`.\*`(?-s)`     | 匹配多行 (导致 . 匹配换行符)                             |
| `(?m)`^.\*;$`(?-m)`  | <yel>^</yel> & <yel>$</yel> 匹配行而不是整个字符串        |
| `(?x)`               | #自由间距模式，此行尾注释被忽略                            |
| `(?-x)`              | 自由间距模式 关                                          |
| /regex/`ismx`        | 修改整个字符串的模式                                     |

### 分组

| 模式                      | 含义                                        |
| ------------------------- | :------------------------------------------ |
| <code>(in\|out)put</code> | 匹配 <yel>input</yel> 或 <yel>output</yel> |
| `\d{5}(-\d{4})?`          | 美国邮政编码 _("+ 4" 可选)_                 |

如果匹配在组后失败，解析器会尝试每个备选项。<br> 可能导致灾难性回溯。

### 反向引用

| 模式                     | 匹配                                                                        |
| ------------------------ | :-------------------------------------------------------------------------- |
| `(to) (be) or not \1 \2` | 匹配 <yel>to be or not to be</yel>                                         |
| `([^\s])\1{2}`           | 匹配非空格字符，然后是相同的字符两次 &nbsp; <yel>aaa</yel>, <yel>...</yel> |
| `\b(\w+)\s+\1\b`         | 匹配重复的单词                                                              |

### 非捕获组

| 模式                           | 含义                               |
| ------------------------------ | :--------------------------------- |
| <code>on(?:click\|load)</code> | 比以下更快：<br>`on(click\|load)` |

尽可能使用非捕获组或原子组

### 原子组

| 模式                              | 含义                                             |
| --------------------------------- | :----------------------------------------------- |
| <code>(?>red\|green\|blue)</code> | 比非捕获组更快                                   |
| <code>(?>id\|identity)\b</code>   | 匹配 <yel>id</yel>，但不匹配 <red>id</red>entity |

"id" 匹配，但在原子组之后 `\b` 失败，解析器不会回溯到组中重试 'identity'

如果备选项重叠，则按从长到短的顺序排列。

### 环视 (Lookaround) {.row-span-2 .col-span-2}

| 模式                    | 含义                                                                  |
| ----------------------- | :-------------------------------------------------------------------- |
| `(?= )`                 | 前瞻，如果能在前面找到                                                  |
| `(?! )`                 | 前瞻，如果不能在前面找到                                                |
| `(?<= )`                | 后顾，如果能在后面找到                                                  |
| `(?<! )`                | 后顾，如果不能在后面找到                                                |
| `\b\w+?(?=ing\b)`       | 匹配 <yel>warbl</yel>ing, <yel>str</yel>ing, <yel>fish</yel>ing, ... |
| `\b(?!\w+ing\b)\w+\b`   | 不以 <red>ing</red> 结尾的单词                                        |
| `(?<=\bpre).*?\b `      | 匹配 pre<yel>tend</yel>, pre<yel>sent</yel>, pre<yel>fix</yel>, ...  |
| `\b\w{3}(?<!pre)\w*?\b` | 不以 <red>pre</red> 开头的单词                                        |
| `\b\w+(?<!ing)\b`       | 匹配不以 <red>ing</red> 结尾的单词                                    |

### If-then-else

如果字符串后面出现单词 "her"，则匹配 "Mr." 或 "Ms."

```regex
M(?(?=.*?\bher\b)s|r)\.
```

IF 条件需要环视

## Python 中的 RegEx

### 入门

导入正则表达式模块

```python
import re
```

### 示例 {.col-span-2 .row-span-3}

#### re.search()

```python
>>> sentence = 'This is a sample string'
>>> bool(re.search(r'this', sentence, flags=re.I))
True
>>> bool(re.search(r'xyz', sentence))
False
```

#### re.findall()

```python
>>> re.findall(r'\bs?pare?\b', 'par spar apparent spare part pare')
['par', 'spar', 'spare', 'pare']
>>> re.findall(r'\b0*[1-9]\d{2,}\b', '0501 035 154 12 26 98234')
['0501', '154', '98234']
```

#### re.finditer()

```python
>>> m_iter = re.finditer(r'[0-9]+', '45 349 651 593 4 204')
>>> [m[0] for m in m_iter if int(m[0]) < 350]
['45', '349', '4', '204']
```

#### re.split()

```python
>>> re.split(r'\d+', 'Sample123string42with777numbers')
['Sample', 'string', 'with', 'numbers']
```

#### re.sub()

```python
>>> ip_lines = "catapults\nconcatenate\ncat"
>>> print(re.sub(r'^', r'* ', ip_lines, flags=re.M))
* catapults
* concatenate
* cat
```

#### re.compile()

```python
>>> pet = re.compile(r'dog')
>>> type(pet)
<class '_sre.SRE_Pattern'>
>>> bool(pet.search('They bought a dog'))
True
>>> bool(pet.search('A cat crossed their path'))
False
```

### 函数

| 函数          | 描述                                                              |
| ------------- | :---------------------------------------------------------------- |
| `re.findall`  | 返回包含所有匹配项的列表                                          |
| `re.finditer` | 返回匹配对象的可迭代对象（每个匹配项一个）                        |
| `re.search`   | 如果字符串中任何位置有匹配，则返回一个 Match 对象                 |
| `re.split`    | 返回一个列表，其中字符串已在每个匹配处拆分                        |
| `re.sub`      | 用字符串替换一个或多个匹配项                                      |
| `re.compile`  | 编译正则表达式模式以供后续使用                                    |
| `re.escape`   | 返回所有非字母数字字符都已反斜杠转义的字符串                      |

### 标志

| -      | -               | -                                            |
| ------ | --------------- | :------------------------------------------- |
| `re.I` | `re.IGNORECASE` | 忽略大小写                                   |
| `re.M` | `re.MULTILINE`  | 多行模式                                     |
| `re.L` | `re.LOCALE`     | 使 `\w`、`\b`、`\s` _依赖于区域设置_          |
| `re.S` | `re.DOTALL`     | 点号匹配所有字符 _(包括换行符)_              |
| `re.U` | `re.UNICODE`    | 使 `\w`、`\b`、`\d`、`\s` _依赖于 Unicode_    |
| `re.X` | `re.VERBOSE`    | 可读样式                                     |

## JavaScript 中的 Regex

### test()

```javascript
let textA = "I like APPles very much";
let textB = "I like APPles";
let regex = /apples$/i;

// 输出: false
console.log(regex.test(textA));

// 输出: true
console.log(regex.test(textB));
```

### search()

```javascript
let text = "I like APPles very much";
let regexA = /apples/;
let regexB = /apples/i;

// 输出: -1
console.log(text.search(regexA));

// 输出: 7
console.log(text.search(regexB));
```

### exec()

```javascript
let text = "Do you like apples?";
let regex = /apples/;

// 输出: apples
console.log(regex.exec(text)[0]);

// 输出: Do you like apples?
console.log(regex.exec(text).input);
```

### match()

```javascript
let text = "Here are apples and apPleS";
let regex = /apples/gi;

// 输出: [ "apples", "apPleS" ]
console.log(text.match(regex));
```

### split() {.col-span-2}

```javascript
let text = "This 593 string will be brok294en at places where d1gits are.";
let regex = /\d+/g;

// 输出: [ "This ", " string will be brok", "en at places where d", "gits are." ]
console.log(text.split(regex));
```

### matchAll()

```javascript
let regex = /t(e)(st(\d?))/g;
let text = "test1test2";
let array = [...text.matchAll(regex)];

// 输出: ["test1", "e", "st1", "1"]
console.log(array[0]);

// 输出: ["test2", "e", "st2", "2"]
console.log(array[1]);
```

### replace()

```javascript {.wrap}
let text = "Do you like aPPles?";
let regex = /apples/i;

// 输出: Do you like mangoes?
let result = text.replace(regex, "mangoes");
console.log(result);
```

### replaceAll()

```javascript
let regex = /apples/gi;
let text = "Here are apples and apPleS";

// 输出: Here are mangoes and mangoes
let result = text.replaceAll(regex, "mangoes");
console.log(result);
```

## PHP 中的 Regex

### 函数 {.col-span-2}

| -                         | -                                                                |
| ------------------------- | :--------------------------------------------------------------- |
| `preg_match()`            | 执行正则表达式匹配                                               |
| `preg_match_all()`        | 执行全局正则表达式匹配                                           |
| `preg_replace_callback()` | 使用回调函数执行正则表达式搜索和替换                             |
| `preg_replace()`          | 执行正则表达式搜索和替换                                         |
| `preg_split()`            | 按正则表达式模式拆分字符串                                       |
| `preg_grep()`             | 返回与模式匹配的数组条目                                         |

### preg_replace

```php {.wrap}
$str = "Visit Microsoft!";
$regex = "/microsoft/i";

// 输出: Visit CheatSheets!
echo preg_replace($regex, "CheatSheets", $str);
```

### preg_match

```php
$str = "Visit CheatSheets";
$regex = "#cheatsheets#i";

// 输出: 1
echo preg_match($regex, $str);
```

### preg_matchall {.col-span-2 .row-span-2}

```php
$regex = "/[a-zA-Z]+ (\d+)/";
$input_str = "June 24, August 13, and December 30";
if (preg_match_all($regex, $input_str, $matches_out)) {

    // 输出: 2
    echo count($matches_out);

    // 输出: 3
    echo count($matches_out[0]);

    // 输出: Array("June 24", "August 13", "December 30")
    print_r($matches_out[0]);

    // 输出: Array("24", "13", "30")
    print_r($matches_out[1]);
}
```

### preg_grep

```php
$arr = ["Jane", "jane", "Joan", "JANE"];
$regex = "/Jane/";

// 输出: Jane
echo preg_grep($regex, $arr);
```

### preg_split {.col-span-2}

```php
$str = "Jane\tKate\nLucy Marion";
$regex = "@\s@";

// 输出: Array("Jane", "Kate", "Lucy", "Marion")
print_r(preg_split($regex, $str));
```

## Java 中的 Regex

### 样式 {.col-span-2}

#### 第一种方式

```java
Pattern p = Pattern.compile(".s", Pattern.CASE_INSENSITIVE);
Matcher m = p.matcher("aS");
boolean s1 = m.matches();
System.out.println(s1);   // 输出: true
```

#### 第二种方式

```java
boolean s2 = Pattern.compile("[0-9]+").matcher("123").matches();
System.out.println(s2);   // 输出: true
```

#### 第三种方式

```java
boolean s3 = Pattern.matches(".s", "XXXX");
System.out.println(s3);   // 输出: false
```

### Pattern 字段

| -                  | -                               |
| ------------------ | :------------------------------ |
| `CANON_EQ`         | 规范等价                        |
| `CASE_INSENSITIVE` | 不区分大小写匹配                |
| `COMMENTS`         | 允许空白和注释                  |
| `DOTALL`           | Dotall 模式                     |
| `MULTILINE`        | 多行模式                        |
| `UNICODE_CASE`     | Unicode 感知的大小写折叠        |
| `UNIX_LINES`       | Unix 行模式                     |

### 方法

#### Pattern

- Pattern compile(String regex [, int flags])
- boolean matches([String regex, ] CharSequence input)
- String[] split(String regex [, int limit])
- String quote(String s)

#### Matcher

- int start([int group | String name])
- int end([int group | String name])
- boolean find([int start])
- String group([int group | String name])
- Matcher reset()

#### String

- boolean matches(String regex)
- String replaceAll(String regex, String replacement)
- String[] split(String regex[, int limit])

还有更多方法...

### 示例 {.col-span-2}

替换句子：

```java
String regex = "[A-Z\n]{5}$";
String str = "I like APP\nLE";

Pattern p = Pattern.compile(regex, Pattern.MULTILINE);
Matcher m = p.matcher(str);

// 输出: I like Apple!
System.out.println(m.replaceAll("pple!"));
```

所有匹配项的数组：

```java
String str = "She sells seashells by the Seashore";
String regex = "\\w*se\\w*";

Pattern p = Pattern.compile(regex, Pattern.CASE_INSENSITIVE);
Matcher m = p.matcher(str);

List<String> matches = new ArrayList<>();
while (m.find()) {
    matches.add(m.group());
}

// 输出: [sells, seashells, Seashore]
System.out.println(matches);
```

## MySQL 中的 Regex {.cols-2}

### 函数

| 名称               | 描述                                                                     |
| ------------------ | :----------------------------------------------------------------------- |
| `REGEXP          ` | 字符串是否匹配正则表达式                                                 |
| `REGEXP_INSTR()  ` | 匹配正则表达式的子字符串的起始索引 <br>_(注意：仅限 MySQL 8.0+)_         |
| `REGEXP_LIKE()   ` | 字符串是否匹配正则表达式 <br>_(注意：仅限 MySQL 8.0+)_                   |
| `REGEXP_REPLACE()` | 替换匹配正则表达式的子字符串 <br>_(注意：仅限 MySQL 8.0+)_               |
| `REGEXP_SUBSTR() ` | 返回匹配正则表达式的子字符串 <br>_(注意：仅限 MySQL 8.0+)_               |

### REGEXP

```sql {.wrap}
expr REGEXP pat
```

#### 示例

```sql
mysql> SELECT 'abc' REGEXP '^[a-d]';
1
mysql> SELECT name FROM cities WHERE name REGEXP '^A';
mysql> SELECT name FROM cities WHERE name NOT REGEXP '^A';
mysql> SELECT name FROM cities WHERE name REGEXP 'A|B|R';
mysql> SELECT 'a' REGEXP 'A', 'a' REGEXP BINARY 'A';
1   0
```

### REGEXP_REPLACE

```{.wrap}
REGEXP_REPLACE(expr, pat, repl[, pos[, occurrence[, match_type]]])
```

#### 示例

```sql
mysql> SELECT REGEXP_REPLACE('a b c', 'b', 'X');
a X c
mysql> SELECT REGEXP_REPLACE('abc ghi', '[a-z]+', 'X', 1, 2);
abc X
```

### REGEXP_SUBSTR

```{.wrap}
REGEXP_SUBSTR(expr, pat[, pos[, occurrence[, match_type]]])
```

#### 示例

```sql
mysql> SELECT REGEXP_SUBSTR('abc def ghi', '[a-z]+');
abc
mysql> SELECT REGEXP_SUBSTR('abc def ghi', '[a-z]+', 1, 3);
ghi
```

### REGEXP_LIKE

```
REGEXP_LIKE(expr, pat[, match_type])
```

#### 示例

```sql
mysql> SELECT regexp_like('aba', 'b+')
1
mysql> SELECT regexp_like('aba', 'b{2}')
0
mysql> # i: 不区分大小写
mysql> SELECT regexp_like('Abba', 'ABBA', 'i');
1
mysql> # m: 多行模式
mysql> SELECT regexp_like('a\nb\nc', '^b$', 'm');
1
```

### REGEXP_INSTR

```{.wrap}
REGEXP_INSTR(expr, pat[, pos[, occurrence[, return_option[, match_type]]]])
```

#### 示例

```sql
mysql> SELECT regexp_instr('aa aaa aaaa', 'a{3}');
2
mysql> SELECT regexp_instr('abba', 'b{2}', 2);
2
mysql> SELECT regexp_instr('abbabba', 'b{2}', 1, 2);
5
mysql> SELECT regexp_instr('abbabba', 'b{2}', 1, 3, 1);
7
```
