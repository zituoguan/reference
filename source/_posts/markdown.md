---
title: Markdown
date: 2020-12-14 18:28:43
background: bg-[#6319bf]
tags:
  - md
  - Markup
  - text
  - format
categories:
  - 编程
intro: 这是 Markdown 语法的快速参考备忘单。
plugins:
  - copyCode
  - runCode
---

## Markdown 快速参考

### 标题 (atx 样式)

<!-- prettier-ignore -->
```markdown
# h1
## h2
### h3
#### h4
##### h5
###### h6
```

### 标题 (setext 样式)

<!-- prettier-ignore -->
```markdown
Header 1
========

Header 2
--------
```

### 块引用

```markdown
> 这是
> 一个块引用
>
> > 嵌套的
> > 块引用
```

### 无序列表 {.row-span-2}

<!-- prettier-ignore -->
```markdown
* 项目 1
* 项目 2
  * 项目 3a
  * 项目 3b
```

或

```markdown
- 项目 1
- 项目 2
```

或

<!-- prettier-ignore -->
```markdown
_ 项目 1
+ 项目 2
```

或

```markdown
- [ ] 未选复选框
- [x] 已选复选框
```

### 有序列表

```markdown
1. 项目 1
2. 项目 2
   a. 项目 3a
   b. 项目 3b
```

### 链接

```markdown
[链接](http://google.com)

[链接][google]
[google]: http://google.com

<http://google.com>
```

### 强调

<!-- prettier-ignore -->
```markdown
*斜体*
_斜体_

**粗体**
__粗体__

`行内代码`
~~删除线~~
```

### 水平线

连字符

<!-- prettier-ignore -->
```markdown
---
```

星号

<!-- prettier-ignore -->
```markdown
***
```

下划线

<!-- prettier-ignore -->
```markdown
___
```

### 代码

````markdown
```javascript
console.log("这是一个代码块");
```
````

<!-- prettier-ignore -->
```markdown
~~~css
.button {
  border: none;
}
~~~
```

```markdown
    4 个空格缩进形成一个代码块
```

### 转义代码

转义代码块可以在外部使用更多的反引号或不同的符号。

<!-- prettier-ignore -->
`````markdown
````markdown
```bash
echo hi
```
````

~~~markdown
```bash
echo hi
```
~~~

`````

#### 行内代码

```markdown
`行内代码` 两边有反引号
```

### 表格

```markdown
| 左对齐列 | 居中列 | 右对齐列 |
| :---------- | :-----------: | -----------: |
| 单元格 1      |   居中    |        $1600 |
| 单元格 2      |    单元格 3     |          $12 |
```

简单样式

<!-- prettier-ignore -->
```markdown
左对齐列 | 居中列 | 右对齐列
:----------:|:-------------:|:-----------:
   单元格 1   |   居中    |    $1600
   单元格 2   |    单元格 3     |     $12
```

一个 Markdown 表格生成器：[tableconvert.com](https://tableconvert.com/)

### 图片 {.col-span-2}

```markdown
![GitHub Logo](/images/logo.png)

![替代文本](url)
```

#### 带链接的图片

```markdown
[![GitHub Logo](/images/logo.png)](https://github.com/)

[![替代文本](image_url)](link_url)
```

#### 引用样式

```markdown
![替代文本][logo]

[logo]: /images/logo.png "Logo 标题"
```

### 反斜杠转义

| 字符              | 转义                  | 描述                  |
| ----------------- | --------------------- | :-------------------- |
| <code>\\</code>   | <code>\\\\</code>     | 反斜杠                |
| <code>\`</code>   | <code>\\\`</code>     | 反引号                |
| <code>\*</code>   | <code>\\\*</code>     | 星号                  |
| <code>\_</code>   | <code>\\\_</code>     | 下划线                |
| <code>\{\}</code> | <code>\\\{\\\}</code> | 大括号                |
| <code>\[\]</code> | <code>\\\[\\\]</code> | 方括号                |
| <code>\(\)</code> | <code>\\\(\\\)</code> | 圆括号                |
| <code>\#</code>   | <code>\\\#</code>     | 井号                  |
| <code>\+</code>   | <code>\\\+</code>     | 加号                  |
| <code>\-</code>   | <code>\\\-</code>     | 减号（连字符）        |
| <code>\.</code>   | <code>\\\.</code>     | 点号                  |
| <code>\!</code>   | <code>\\\!</code>     | 感叹号                |

{.show-header}

