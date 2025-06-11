---
title: XPath
date: 2020-12-19 22:15:43
background: bg-[#77aeeb]
tags:
  - 文档
  - 表达式
  - 选择
categories:
  - 工具箱
intro: |
  这是一个 [XPath](https://en.wikipedia.org/wiki/XPath) 选择器速查表，列出了常用的 XPath 定位方法和 CSS 选择器
plugins:
  - copyCode
---

## XPath 选择器 {.cols-6}

### 入门 {.col-span-2}

- [Xpath 测试平台](http://www.whitebeam.org/library/guide/TechNotes/xpathtestbed.rhtm) _(whitebeam.org)_

在 Firefox 或基于 Chromium 的浏览器控制台中测试：

```console
$x('/html/body')
$x('//h1')
$x('//h1')[0].innerText
$x('//a[text()="XPath"]')[0].click()
```

### 后代选择器 {.col-span-2}

| Xpath        | CSS          |
| ------------ | ------------ |
| `//h1`       | h1           |
| `//div//p`   | div p        |
| `//ul/li`    | ul > li      |
| `//ul/li/a`  | ul > li > a  |
| `//div/*`    | div > \*     |
| `/`          | :root        |
| `/html/body` | :root > body |

{.show-header}

### 顺序选择器 {.col-span-2}

| Xpath               | CSS                  |
| ------------------- | -------------------- |
| `//ul/li[1]`        | ul > li:first-child  |
| `//ul/li[2]`        | ul > li:nth-child(2) |
| `//ul/li[last()]`   | ul > li:last-child   |
| `//li[@id="id"][1]` | li#id:first-child    |
| `//a[1]`            | a:first-child        |
| `//a[last()]`       | a:last-child         |

{.show-header}

### 属性选择器 {.col-span-3 .row-span-2}

| Xpath                           | CSS                  |
| ------------------------------- | -------------------- |
| `//*[@id="id"]`                 | #id                  |
| `//*[@class="class"]`           | .class               |
| `//input[@type="submit"]`       | input[type="submit"] |
| `//a[@id="abc"][@for="xyz"]`    | a#abc[for="xyz"]     |
| `//a[@rel]`                     | a[rel]               |
| `//a[starts-with(@href, '/')]`  | a[href^='/']         |
| `//a[ends-with(@href, '.pdf')]` | a[href$='pdf']       |
| `//a[contains(@href, '://')]`   | a[href*='`:`//']     |
| `//a[contains(@rel, 'help')]`   | a[rel~='help']       |

{.show-header}

### 同级元素选择器 {.col-span-3}

| Xpath                                | CSS      |
| ------------------------------------ | -------- |
| `//h1/following-sibling::ul`         | h1 ~ ul  |
| `//h1/following-sibling::ul[1]`      | h1 + ul  |
| `//h1/following-sibling::[@id="id"]` | h1 ~ #id |

{.show-header}

### jQuery {.col-span-3}

| Xpath                            | CSS                        |
| -------------------------------- | -------------------------- |
| `//ul/li/..`                     | $('ul > li').parent()      |
| `//li/ancestor-or-self::section` | $('li').closest('section') |
| `//a/@href`                      | $('a').attr('href')        |
| `//span/text()`                  | $('span').text()           |

{.show-header}

### 其他选择器 {.col-span-3}

| Xpath                             | CSS / 含义                |                       |
| --------------------------------- | ------------------------- | --------------------- |
| `//h1[not(@id)]`                  | h1:not([id])              |                       |
| `//button[text()="Submit"]`       | 文本匹配                  |                       |
| `//button[contains(text(),"Go")]` | 文本包含 (子字符串)       |                       |
| `//product[@price > 2.50]`        | 算术运算                  |                       |
| `//ul[*]`                         | 有子元素                  |                       |
| `//ul[li]`                        | 有子元素 (特定)           |                       |
| `//a[@name or @href]`             | 或逻辑                    |                       |
| `//a                              | //div`                    | 并集 (合并结果)       |

{.show-header}

## XPath 表达式

### 步骤和轴 {.secondary}

<br/>

| -    | -    | -    | -               |
| ---- | ---- | ---- | --------------- |
| `//` | `ul` | `/`  | `a[@id='link']` |
| 轴   | 步骤 | 轴   | 步骤            |

{.left-text}

### 前缀

| 前缀   | 示例                  | 含义     |
| ------ | --------------------- | -------- |
| `//`   | `//hr[@class='edge']` | 任意位置 |
| `/`    | `/html/body/div`      | 根路径   |
| `./`   | `./div/p`             | 相对路径 |

{.show-header}

### 轴 (Axes)

| 轴   | 示例                | 含义     |
| ---- | ------------------- | -------- |
| `/`  | `//ul/li/a`         | 子节点   |
| `//` | `//[@id="list"]//a` | 后代节点 |

{.show-header}

## XPath 谓词

### 谓词

```bash
//div[true()]
//div[@class="head"]
//div[@class="head"][@id="top"]
```

仅当某个条件为真时限制节点集。它们可以被链式调用。

### 运算符

```bash
# 比较
//a[@id = "xyz"]
//a[@id != "xyz"]
//a[@price > 25]
```

```bash
# 逻辑 (and/or)
//div[@id="head" and position()=2]
//div[(x and y) or not(z)]
```

### 使用节点

```bash
# 在函数内部使用它们
//ul[count(li) > 2]
//ul[count(li[@class='hide']) > 0]
```

```bash
# 返回拥有 <li> 子元素的 <ul>
//ul[li]
```

你可以在谓词内部使用节点。

### 索引

```bash
//a[1]                # 第一个 <a>
//a[last()]           # 最后一个 <a>
//ol/li[2]            # 第二个 <li>
//ol/li[position()=2] # 与上面相同
//ol/li[position()>1] #:not(:first-child)
```

使用 `[]` 配合数字，或使用 `last()` 或 `position()`。

### 链式顺序

```bash
a[1][@href='/']
a[@href='/'][1]
```

顺序很重要，这两个是不同的。

### 嵌套谓词

```
//section[.//h1[@id='hi']]
```

如果 `<section>` 包含一个 id 为 'hi' 的 `<h1>` 后代元素，则返回该 `<section>`。

## XPath 函数 {.cols-2}

### 节点函数

```bash
name()            # //[starts-with(name(), 'h')]
text()            # //button[text()="Submit"]
                  # //button/text()
lang(str)
namespace-uri()
```

```bash
count()           # //table[count(tr)=1]
position()        # //ol/li[position()=2]
```

### 字符串函数

```bash
contains()        # font[contains(@class,"head")]
starts-with()     # font[starts-with(@class,"head")]
ends-with()       # font[ends-with(@class,"head")]
```

```bash
concat(x,y)
substring(str, start, len)
substring-before("01/02", "/")  #=> 01
substring-after("01/02", "/")   #=> 02
translate()
normalize-space()
string-length()
```

### 布尔函数

```bash
not(expr)         # button[not(starts-with(text(),"Submit"))]
```

### 类型转换

```bash
string()
number()
boolean()
```

## XPath 轴 (Axes) {.cols-2}

### 使用轴

```bash
//ul/li                       # ul > li
//ul/child::li                # ul > li (相同)
//ul/following-sibling::li    # ul ~ li
//ul/descendant-or-self::li   # ul li
//ul/ancestor-or-self::li     # $('ul').closest('li')
```

---

|      |      |            |      |
| ---- | ---- | ---------- | ---- |
| `//` | `ul` | `/child::` | `li` |
| 轴   | 步骤 | 轴         | 步骤 |

{.left-text}

表达式的步骤由 `/` 分隔，通常用于选择子节点。但这并非总是如此：你可以使用 `::` 指定不同的“轴”。

### 子节点轴 (Child axis)

```bash
# 两者相同
//ul/li/a
//child::ul/child::li/child::a
```

`child::` 是默认轴。这使得 `//a/b/c` 可以工作。

```bash
# 两者相同
# 这之所以有效，是因为 `child::li` 为真值
//ul[li]
//ul[child::li]
```

```bash
# 两者相同
//ul[count(li) > 2]
//ul[count(child::li) > 2]
```

### 后代或自身轴 (Descendant-or-self axis)

```bash
# 两者相同
//div//h4
//div/descendant-or-self::h4
```

`//` 是 `descendant-or-self::` 轴的简写。

```bash
# 两者相同
//ul//[last()]
//ul/descendant-or-self::[last()]
```

### 其他轴 {.row-span-2}

| 轴                   | 缩写   | 注释                                             |
| -------------------- | ------ | ------------------------------------------------ |
| `ancestor`           |        |                                                  |
| `ancestor-or-self`   |        |                                                  |
| `attribute`          | `@`    | `@href` 是 `attribute::href` 的简写              |
| `child`              |        | `div` 是 `child::div` 的简写                     |
| `descendant`         |        |                                                  |
| `descendant-or-self` | `//`   | `//` 是 `/descendant-or-self::node()/` 的简写    |
| `namespace`          |        |                                                  |
| `self`               | `.`    | `.` 是 `self::node()` 的简写                     |
| `parent`             | `..`   | `..` 是 `parent::node()` 的简写                  |
| `following`          |        |                                                  |
| `following-sibling`  |        |                                                  |
| `preceding`          |        |                                                  |
| `preceding-sibling`  |        |                                                  |

{.headers}

还有其他可以使用的轴。

### 并集

```bash
//a | //span
```

使用 `|` 来连接两个表达式。

## XPath 更多示例 {.cols-2}

### 示例

```bash
//*                 # 所有元素
count(//*)          # 计算所有元素的数量
(//h1)[1]/text()    # 第一个 h1 标题的文本
//li[span]          # 查找内部包含 <span> 的 <li>
                    # ...展开为 //li[child::span]
//ul/li/..          # 使用 .. 选择父元素
```

### 查找父元素

```bash
//section[h1[@id='section-name']]
```

查找直接包含 `h1#section-name` 的 `<section>`

```bash
//section[//h1[@id='section-name']]
```

查找包含 `h1#section-name` 的 `<section>`。（与上面类似，但使用 descendant-or-self 而不是 child）

### 最近的祖先元素 (Closest)

```bash
./ancestor-or-self::[@class="box"]
```

类似于 jQuery 的 `$().closest('.box')`。

### 属性

```bash
//item[@price > 2*@discount]
```

查找 `<item>` 并检查其属性

## 另请参阅

- [Devhints](https://devhints.io/xpath) _(devhints.io)_
- [Xpath 测试平台](http://www.whitebeam.org/library/guide/TechNotes/xpathtestbed.rhtm) _(whitebeam.org)_
