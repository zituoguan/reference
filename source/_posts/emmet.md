---
title: Emmet
date: 2020-12-14 18:28:43
background: bg-[#95c844]
tags:
  - 代码片段
  - 编程
  - html
  - css
  - 缩写
categories:
  - 工具箱
intro: |
  [Emmet](https://emmet.io/) 是一个面向 Web 开发人员的工具包，用于提升 HTML 和 CSS 代码编写效率，它允许您使用众所周知的 CSS 选择器以光速编写大型 HTML 代码块。
plugins:
  - copyCode
---

## Emmet 语法

### 入门

让我们开始以光速提升您的开发效率。

- [Visual Studio Code 中的 Emmet](https://code.visualstudio.com/docs/editor/emmet) _(code.visualstudio.com)_
- [Sublime Text 的 Emmet 2 插件](https://github.com/emmetio/sublime-text-plugin) _(github.com)_
- [Coda 的 Emmet 插件](https://emmet.io/download/coda/) _(emmet.io)_
- [Atom 的 Emmet 插件](https://github.com/emmetio/emmet-atom#readme) _(github.com)_

### 重复: \*

<code>ul>li\*5</code>

```html
<ul>
  <li></li>
  <li></li>
  <li></li>
  <li></li>
  <li></li>
</ul>
```

### 子代: >

`nav>ul>li`

```html
<nav>
  <ul>
    <li></li>
  </ul>
</nav>
```

### 自定义属性 {.col-span-2}

<code>p[title="你好世界"]</code>

```html
<p title="你好世界"></p>
```

`td[rowspan=2 colspan=3 title]`

```html
<td rowspan="2" colspan="3" title=""></td>
```

`[a='value1' b="value2"]`

```html
<div a="value1" b="value2"></div>
```

### 文本: {}

<code>a{点我}</code>

```html
<a href="">点我</a>
```

<code>p>{点击 }+a{这里}+{ 继续}</code>

```html {.wrap}
<p>点击 <a href="">这里</a> 继续</p>
```

### ID 和 CLASS 属性 {.row-span-2}

`#header`

```html
<div id="header"></div>
```

`.title`

```html
<div class="title"></div>
```

`form#search.wide`

```html
<form id="search" class="wide"></form>
```

`p.class1.class2.class3`

```html
<p class="class1 class2 class3"></p>
```

### 隐式标签名 {.row-span-2}

`.class`

```html
<div class="class"></div>
```

`em>.class`

```html
<em><span class="class"></span></em>
```

`ul>.class`

```html
<ul>
  <li class="class"></li>
</ul>
```

`table>.row>.col`

```html
<table>
  <tr class="row">
    <td class="col"></td>
  </tr>
</table>
```

### 同级: +

`div+p+bq`

```html
<div></div>
<p></p>
<blockquote></blockquote>
```

### 向上一级: ^

`div+div>p>span+em^bq`

```html
<div></div>
<div>
  <p><span></span><em></em></p>
  <blockquote></blockquote>
</div>
```

`div+div>p>span+em^^bq`

```html
<div></div>
<div>
  <p><span></span><em></em></p>
</div>
<blockquote></blockquote>
```

### 分组: ()

<code>div>(header>ul>li\*2>a)+footer>p</code>

```html
<div>
  <header>
    <ul>
      <li><a href=""></a></li>
      <li><a href=""></a></li>
    </ul>
  </header>
  <footer>
    <p></p>
  </footer>
</div>
```

<code>(div>dl>(dt+dd)\*4)+footer>p</code>

```html
<div>
  <dl>
    <dt></dt>
    <dd></dd>
    <dt></dt>
    <dd></dd>
    <dt></dt>
    <dd></dd>
    <dt></dt>
    <dd></dd>
  </dl>
</div>
<footer>
  <p></p>
</footer>
```

### 编号: $ {.col-span-2}

<code>ul>li.item$\*3</code>

```html
<ul>
  <li class="item1"></li>
  <li class="item2"></li>
  <li class="item3"></li>
</ul>
```

<code>h$[title=项目$]{标题 $}\*3</code>

```html
<h1 title="项目1">标题 1</h1>
<h2 title="项目2">标题 2</h2>
<h3 title="项目3">标题 3</h3>
```

<code>ul>li.item$$$\*3</code>

```html
<ul>
  <li class="item001"></li>
  <li class="item002"></li>
  <li class="item003"></li>
</ul>
```

<code>ul>li.item$@-\*3</code>

```html
<ul>
  <li class="item3"></li>
  <li class="item2"></li>
  <li class="item1"></li>
</ul>
```

<code>ul>li.item$@2\*3</code>

```html
<ul>
  <li class="item2"></li>
  <li class="item3"></li>
  <li class="item4"></li>
</ul>
```

## 另请参阅 {.cols-1}

- [Emmet 速查表](https://docs.emmet.io/cheat-sheet/) _(docs.emmet.io)_
