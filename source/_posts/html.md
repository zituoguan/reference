---
title: HTML
date: 2021-07-20 19:16:42
background: bg-[#cc5534]
tags:
  - web
categories:
  - 编程
intro: |
  这份 HTML 快速参考备忘单以易读的布局列出了常用的 HTML 和 HTML5 标签。
plugins:
  - copyCode
  - runCode
---

## 入门

### hello.html {.col-span-2 .row-span-2}

```html
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>HTML5 样板</title>
  </head>
  <body>
    <h1>你好世界，你好 r3f.cn！</h1>
  </body>
</html>
```

或者在 [jsfiddle](https://jsfiddle.net/Fechin/1e4wz20b/) 中尝试一下

### 注释

```html
<!-- 这是一个注释 -->

<!--
    或者你可以注释掉
    大量的代码行。
-->
```

### 段落

```html
<p>我来自 r3f.cn</p>
<p>分享快速参考备忘单。</p>
```

参见：[段落元素 (The Paragraph element)](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/p)

### HTML 链接

```html
<a href="https://r3f.cn">CheatSheets</a>
<a href="mailto:jack@abc.com">邮件</a>
<a href="tel:+12345678">呼叫</a>
<a href="sms:+12345678&body=ha%20ha">短信</a>
```

---

|     |          |                                                                 |
| --- | -------- | --------------------------------------------------------------- |
|     | `href`   | 超链接指向的 URL                                                |
|     | `rel`    | 链接 URL 的关系                                                 |
|     | `target` | 链接目标位置：<br/>`_self` (自身)、`_blank` (新窗口)、`_top` (顶层)、`_parent` (父框架) |

{.left-text}

参见：[\<a> 属性 (The \<a> Attributes)](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/a#attributes)

### 图像标签

```html {.wrap}
<img loading="lazy" src="https://xxx.png" alt="在此描述图像" width="400" height="400" />
```

---

|     |           |                                          |
| --- | --------- | ---------------------------------------- |
|     | `src`     | 必需，图像位置 (URL | 路径)             |
|     | `alt`     | 图像描述                                 |
|     | `width`   | 图像宽度                                 |
|     | `height`  | 图像高度                                 |
|     | `loading` | 浏览器应如何加载                         |

{.left-text}

参见：[图像嵌入元素 (The Image Embed element)](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/img)

### 文本格式化标签

```html
<b>粗体文本</b>
<strong>此文本很重要</strong>
<i>斜体文本</i>
<em>此文本被强调</em>
<u>下划线文本</u>
<pre>预格式化文本</pre>
<code>源代码</code>
<del>删除的文本</del>
<mark>高亮文本 (HTML5)</mark>
<ins>插入的文本</ins>
<sup>使文本成为上标</sup>
<sub>使文本成为下标</sub>
<small>使文本更小</small>
<kbd>Ctrl</kbd>
<blockquote>文本块引用</blockquote>
```

### 标题

```html
<h1>这是标题 1</h1>
<h2>这是标题 2</h2>
<h3>这是标题 3</h3>
<h4>这是标题 4</h4>
<h5>这是标题 5</h5>
<h6>这是标题 6</h6>
```

你的页面上应该只有一个 h1 标签

### 区块划分

|                 |                                      |
| --------------- | ------------------------------------ |
| `<div></div>`   | 页面内容的分区或区块                 |
| `<span></span>` | 其他内容中的文本区块                 |
| `<p></p>`       | 文本段落                             |
| `<br>`          | 换行符                               |
| `<hr>`          | 基本水平线                           |

这些是用于将页面划分为区块的标签

### 内联框架 {.row-span-2}

```html {.wrap}
<iframe
  title="纽约"
  width="342"
  height="306"
  id="gmap_canvas"
  src="https://maps.google.com/maps?q=2880%20Broadway,%20New%20York&t=&z=13&ie=UTF8&iwloc=&output=embed"
  scrolling="no"
>
</iframe>
```

#### ↓ 预览

<iframe title="纽约"
    width="342"
    height="306"
    id="gmap_canvas"
    src="https://maps.google.com/maps?q=2880%20Broadway,%20New%20York&t=&z=13&ie=UTF8&iwloc=&output=embed"
    scrolling="no">
</iframe>

参见：[内联框架元素 (The Inline Frame element)](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/iframe)

### HTML 中的 JavaScript

```html
<script type="text/javascript">
  let text = "你好 r3f.cn";
  alert(text);
</script>
```

#### 外部 JavaScript

```html
<body>
  ...

  <script src="app.js"></script>
</body>
```

### HTML 中的 CSS

```html
<style type="text/css">
  h1 {
    color: purple;
  }
</style>
```

#### 外部样式表

```html
<head>
  ...
  <link rel="stylesheet" href="style.css" />
</head>
```

## HTML5 标签

### 文档

```html
<body>
  <header>
    <nav>...</nav>
  </header>
  <main>
    <h1>r3f.cn</h1>
  </main>
  <footer>
    <p>©2023 r3f.cn</p>
  </footer>
</body>
```

### 头部导航

```html
<header>
  <nav>
    <ul>
      <li><a href="#">编辑页面</a></li>
      <li><a href="#">Twitter</a></li>
      <li><a href="#">Facebook</a></li>
    </ul>
  </nav>
</header>
```

### HTML5 标签 {.row-span-4}

|                                                                                    |                                        |
| ---------------------------------------------------------------------------------- | -------------------------------------- |
| [article](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/article)       | 独立的内容                             |
| [aside](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/aside)           | 次要内容                               |
| [audio](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/audio)           | 嵌入声音或音频流                       |
| [bdi](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/bdi)               | 双向隔离元素                           |
| [canvas](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/canvas)         | 通过 JavaScript 绘制图形               |
| [data](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/data)             | 机器可读内容                           |
| [datalist](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/datalist)     | 一组预定义选项                         |
| [details](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/details)       | 附加信息                               |
| [dialog](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/dialog)         | 对话框或子窗口                         |
| [embed](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/embed)           | 嵌入外部应用程序                       |
| [figcaption](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/figcaption) | figure 元素的标题或图例                |
| [figure](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/figure)         | 图示                                   |
| [footer](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/footer)         | 页脚或最不重要的信息                   |
| [header](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/header)         | 页眉或重要信息                         |
| [main](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/main)             | 文档的主要内容                         |
| [mark](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/mark)             | 高亮文本                               |
| [meter](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/meter)           | 已知范围内的标量值                     |
| [nav](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/nav)               | 导航链接区块                           |
| [output](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/output)         | 计算结果                               |
| [picture](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/picture)       | 多个图像源的容器                       |
| [progress](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/progress)     | 任务的完成进度                         |
| [rp](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/rp)                 | 提供回退括号                           |
| [rt](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/rt)                 | 定义字符的发音                         |
| [ruby](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/ruby)             | 表示 ruby 注解                         |
| [section](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/section)       | 一系列相关内容中的一个组               |
| [source](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/source)         | 媒体元素的资源                         |
| [summary](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/summary)       | \<details> 元素的摘要                  |
| [template](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/template)     | 定义 HTML 片段                         |
| [time](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/time)             | 时间或日期                             |
| [track](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/track)           | 媒体元素的文本轨道                     |
| [video](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/video)           | 嵌入视频                               |
| [wbr](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/wbr)               | 换行机会                               |

### HTML5 视频

```html {.wrap}
<video controls="" width="100%">
  <source src="https://interactive-examples.mdn.mozilla.net/media/cc0-videos/flower.mp4" type="video/mp4" />
  抱歉，您的浏览器不支持嵌入式视频。
</video>
```

#### ↓ 预览

<video controls="" width="100%">
    <source src="https://interactive-examples.mdn.mozilla.net/media/cc0-videos/flower.mp4" type="video/mp4">
    抱歉，您的浏览器不支持嵌入式视频。
</video>

### HTML5 音频

```html {.wrap}
<audio controls src="https://interactive-examples.mdn.mozilla.net/media/cc0-audio/t-rex-roar.mp3">
  您的浏览器不支持音频元素。
</audio>
```

#### ↓ 预览

<audio controls class="w-full"
    src="https://interactive-examples.mdn.mozilla.net/media/cc0-audio/t-rex-roar.mp3"> 您的浏览器不支持音频元素。 </audio>

### HTML5 Ruby

```html {.wrap}
<ruby> 汉 <rp>(</rp><rt>hàn</rt><rp>)</rp> 字 <rp>(</rp><rt>zì</rt><rp>)</rp> </ruby>
```

#### ↓ 预览

<ruby class="mt-4 text-center text-5xl">
  汉 <rp>(</rp><rt>hàn</rt><rp>)</rp>
  字 <rp>(</rp><rt>zì</rt><rp>)</rp>
</ruby>

### HTML5 bdi

```html
<ul>
  <li>用户 <bdi>hrefs</bdi>: 60 分</li>
  <li>用户 <bdi>jdoe</bdi>: 80 分</li>
  <li>用户 <bdi>إيان</bdi>: 90 分</li>
</ul>
```

#### ↓ 预览

<ul>
 <li>用户 <bdi>hrefs</bdi>: 60 分</li>
 <li>用户 <bdi>jdoe</bdi>: 80 分</li>
 <li>用户 <bdi>إيان</bdi>: 90 分</li>
</ul>

### HTML5 progress

```html
<progress value="50" max="100"></progress>
```

<progress value="50" max="100" class="w-full"></progress>

### HTML5 mark

```html
<p>我爱 <mark>r3f.cn</mark></p>
```

<p>我爱 <mark>r3f.cn</mark></p>

## HTML 表格

### 表格示例 {.row-span-2}

```html
<table>
  <thead>
    <tr>
      <td>姓名</td>
      <td>年龄</td>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Roberta</td>
      <td>39</td>
    </tr>
    <tr>
      <td>Oliver</td>
      <td>25</td>
    </tr>
  </tbody>
</table>
```

### HTML 表格标签 {.row-span-2}

| 标签                                                                              | 描述                             |
| --------------------------------------------------------------------------------- | -------------------------------- |
| [\<table>](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/table)       | 定义一个表格                     |
| [\<th>](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/th)             | 定义表格中的表头单元格           |
| [\<tr>](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/tr)             | 定义表格中的行                   |
| [\<td>](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/td)             | 定义表格中的单元格               |
| [\<caption>](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/caption)   | 定义表格标题                     |
| [\<colgroup>](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/colgroup) | 定义一组列                       |
| [\<col>](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/col)           | 定义表格中的列                   |
| [\<thead>](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/thead)       | 对表头内容进行分组               |
| [\<tbody>](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/tbody)       | 对表体内容进行分组               |
| [\<tfoot>](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/tfoot)       | 对表尾内容进行分组               |

### \<td> 属性

| 属性      | 描述                                   |
| --------- | -------------------------------------- |
| `colspan` | 单元格应跨越的列数                     |
| `headers` | 单元格关联的一个或多个表头单元格       |
| `rowspan` | 单元格应跨越的行数                     |

参见：[td\#属性 (td\#Attributes)](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/td#attributes)

### \<th> 属性

| 属性                                                                             | 描述                                   |
| -------------------------------------------------------------------------------- | -------------------------------------- |
| `colspan`                                                                        | 单元格应跨越的列数                     |
| `headers`                                                                        | 单元格关联的一个或多个表头单元格       |
| `rowspan`                                                                        | 单元格应跨越的行数                     |
| `abbr`                                                                           | 单元格内容的描述                       |
| [scope](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/th#attr-scope) | 表头元素关联的范围                     |

参见：[th\#属性 (th\#Attributes)](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/th#attributes)

## HTML 列表

### 无序列表

```html
<ul>
  <li>我是一个列表项</li>
  <li>我是另一个列表项</li>
  <li>我是又一个列表项</li>
</ul>
```

参见：[无序列表元素 (The Unordered List element)](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/ul)

### 有序列表

```html
<ol>
  <li>我是第一个列表项</li>
  <li>我是第二个列表项</li>
  <li>我是第三个列表项</li>
</ol>
```

参见：[有序列表元素 (The Ordered List element)](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/ol)

### 定义列表

```html
<dl>
  <dt>一个术语</dt>
  <dd>术语的定义</dd>
  <dt>另一个术语</dt>
  <dd>另一个术语的定义</dd>
</dl>
```

参见：[描述列表元素 (The Description List element)](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/dl)

## HTML 表单

### 表单标签 {.row-span-2}

```html
<form method="POST" action="api/login">
  <label for="mail">邮箱：</label>
  <input type="email" id="mail" name="mail" />
  <br />
  <label for="pw">密码：</label>
  <input type="password" id="pw" name="pw" />
  <br />
  <input type="submit" value="登录" />
  <br />
  <input type="checkbox" id="ck" name="ck" />
  <label for="ck">记住我</label>
</form>
```

#### ↓ 预览

<form method="POST" action="api/login" style="padding: 20px;">
    <label for="email">邮箱：</label>
    <input type="email" id="email" name="email" class="border border-slate-400 mt-2">
    <br/>
    <label for="pwd">密码：</label>
    <input type="password" id="pwd" name="pwd" class="border border-slate-400 mt-2">
    <br/>
    <input type="submit" value="登录" class="mt-2">
    <br/>
    <input type="checkbox" id="ck" name="ck" class="mt-2">
    <label for="ck">记住我</label>
</form>

HTML `<form>` 元素用于收集信息并将其发送到外部源。

### 表单属性

| 属性       | 描述                                                                                         |
| ---------- | -------------------------------------------------------------------------------------------- |
| `name`     | 用于脚本的表单名称                                                                           |
| `action`   | 表单脚本的 URL                                                                               |
| `method`   | HTTP 方法，`POST` / `GET` (默认)                                                             |
| `enctype`  | 媒体类型，参见 [enctype](https://developer.mozilla.org/zh-CN/docs/Web/API/HTMLFormElement/enctype) |
| `onsubmit` | 表单提交时运行                                                                               |
| `onreset`  | 表单重置时运行                                                                               |

### Label 标签

```html
<!-- 嵌套标签 -->
<label
  >点我
  <input type="text" id="user" name="name" />
</label>
```

---

```html
<!-- 'for' 属性 -->
<label for="user">点我</label>
<input id="user" type="text" name="name" />
```

label 中的 `for` 引用 input 的 `id` 属性

### Input 标签

```html
<label for="Name">姓名：</label> <input type="text" name="Name" id="" />
```

#### ↓ 预览

<form style="padding: 20px;">
    <label for="username">用户名：</label>
    <input type="text" name="username" id="username" class="border border-slate-400">
</form>

参见：[HTML input 标签](/html#html-input-tags)

### Textarea 标签

```html {.wrap}
<textarea rows="2" cols="30" name="address" id="address"></textarea>
```

#### ↓ 预览

<form style="padding: 20px;">
    <textarea rows="2" cols="30" name="address" id="address" class="border border-slate-400"style="width: 100%"></textarea>
</form>

Textarea 是一个多行文本输入控件

### 单选按钮

```html
<input type="radio" name="gender" id="m" />
<label for="m">男</label>
<input type="radio" name="gender" id="f" />
<label for="f">女</label>
```

#### ↓ 预览

<form style="padding: 20px;">
    <input type="radio" name="gender" id="m">
    <label for="m">男</label>
    <input type="radio" name="gender" id="f">
    <label for="f">女</label>
</form>

单选按钮用于让用户精确选择一个选项

### 复选框

```html
<input type="checkbox" name="s" id="soc" />
<label for="soc">足球</label>
<input type="checkbox" name="s" id="bas" />
<label for="bas">棒球</label>
```

#### ↓ 预览

<form style="padding: 20px;">
    <input type="checkbox" name="sports" id="soccer">
    <label for="soccer">足球</label>
    <input type="checkbox" name="sports" id="baseball">
    <label for="baseball">棒球</label>
</form>

复选框允许用户选择一个或多个选项

### Select 标签

```html
<label for="city">城市：</label>
<select name="city" id="city">
  <option value="1">悉尼</option>
  <option value="2">墨尔本</option>
  <option value="3">克伦威尔</option>
</select>
```

#### ↓ 预览

<form style="padding: 20px">
    <label for="city">城市：</label>
    <select name="city" id="city" class="border border-slate-400">
        <option value="1">悉尼</option>
        <option value="2">墨尔本</option>
        <option value="3">克伦威尔</option>
    </select>
</form>

选择框是一个下拉选项列表

### Fieldset 标签

```html
<fieldset>
  <legend>你最喜欢的怪物</legend>
  <input type="radio" id="kra" name="m" />
  <label for="kraken">克拉肯</label><br />
  <input type="radio" id="sas" name="m" />
  <label for="sas">大脚怪</label>
</fieldset>
```

#### ↓ 预览

<form style="padding: 20px">
    <fieldset class="border border-slate-400" style="padding: 20px">
        <legend>你最喜欢的怪物</legend>
        <input type="radio" id="kra" name="monster">
        <label for="kra">克拉肯</label><br/>
        <input type="radio" id="sas" name="monster">
        <label for="sas">大脚怪</label>
    </fieldset>
</form>

### Datalist 标签 (HTML5)

```html
<label for="b">选择一个浏览器：</label>
<input list="list" id="b" name="browser" />
<datalist id="list">
  <option value="Chrome"></option>
  <option value="Firefox"></option>
  <option value="Internet Explorer"></option>
  <option value="Opera"></option>
  <option value="Safari"></option>
  <option value="Microsoft Edge"></option>
</datalist>
```

#### ↓ 预览

<form style="padding: 20px">
    <label for="myBrowser">选择一个浏览器：</label>
    <input list="browsers" id="myBrowser" name="myBrowser" class="border border-slate-400"/>
    <datalist id="browsers">
      <option value="Chrome">
      <option value="Firefox">
      <option value="Internet Explorer">
      <option value="Opera">
      <option value="Safari">
      <option value="Microsoft Edge">
    </datalist>
</form>

### 提交和重置按钮

```html
<form action="register.php" method="post">
  <label for="foo">姓名：</label>
  <input type="text" name="name" id="foo" />
  <input type="submit" value="提交" />
  <input type="reset" value="重置" />
</form>
```

#### ↓ 预览

<form action="register.php" method="post" style="padding: 20px">
    <label for="name">姓名：</label>
    <input type="text" name="name" id="name" class="border border-slate-400">
    <input type="submit" value="提交">
    <input type="reset" value="重置">
</form>

`提交` 数据到服务器；`重置` 为默认值

## HTML input 标签 {.cols-2}

### Input 属性 {.row-span-2}

input 标签是一个空元素，用于标识从用户处获取特定类型字段信息。

```html {.wrap}
<input type="text" name="?" value="?" minlength="6" required />
```

---

| -   |                         |                                                                                                                               |
| --- | ----------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
|     | `type="…"`              | 输入数据的类型                                                                                                                |
|     | `value="…"`             | 默认值                                                                                                                        |
|     | `name="…"`              | 用于在 HTTP 请求中描述此数据                                                                                                  |
|     | `id="…"`                | 其他 HTML 元素的唯一标识符                                                                                                    |
|     | `readonly`              | 阻止用户修改                                                                                                                  |
|     | `disabled`              | 停止任何交互                                                                                                                  |
|     | `checked`               | 单选框或复选框是否选中                                                                                                        |
|     | `required`              | 必填项，参见 [required](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Attributes/required#example)                         |
|     | `placeholder="…"`       | 添加临时提示，参见 [::placeholder](https://developer.mozilla.org/zh-CN/docs/Web/CSS/::placeholder#examples)                     |
|     | `autocomplete="off"`    | 禁用自动完成                                                                                                                  |
|     | `autocapitalize="none"` | 禁用自动大写                                                                                                                  |
|     | `inputmode="…"`         | 显示特定键盘，参见 [inputmode](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Global_attributes/inputmode)                   |
|     | `list="…"`              | 关联的 [datalist](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/datalist) 的 id                                   |
|     | `maxlength="…"`         | 最大字符数                                                                                                                    |
|     | `minlength="…"`         | 最小字符数                                                                                                                    |
|     | `min="…"`               | range 和 number 类型的最小值                                                                                                  |
|     | `max="…"`               | range 和 number 类型的最大值                                                                                                  |
|     | `step="…"`              | range 和 number 类型中数字的增量                                                                                              |
|     | `pattern="…"`           | 指定一个[正则表达式](/regex)，参见 [pattern](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Attributes/pattern)             |
|     | `autofocus`             | 自动获取焦点                                                                                                                  |
|     | `spellcheck`            | 执行拼写检查                                                                                                                  |
|     | `multiple`              | 是否允许多个值，参见 [multiple](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Attributes/multiple)                         |
|     | `accept=""`             | [file](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/input/file) 上传控件中预期的文件类型                         |

{.left-text}

另请参见：
[\<input> 元素的属性 (Attributes for the \<input> element)](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/input#attributes)

### Input 类型

|                   |                                                                                                                                          |
| ----------------- | ---------------------------------------------------------------------------------------------------------------------------------------- |
| `type="checkbox"` | <input type="checkbox" class="border border-slate-400"> (复选框)                                                                         |
| `type="radio"`    | <input type="radio" class="border border-slate-400"> (单选按钮)                                                                          |
| `type="file"`     | <input type="file" class="border border-slate-400"> (文件)                                                                               |
| `type="hidden"`   | <input type="hidden" class="border border-slate-400"> (隐藏)                                                                             |
| `type="text"`     | <input type="text" class="border border-slate-400"> (文本)                                                                               |
| `type="password"` | <input type="password" class="border border-slate-400"> (密码)                                                                           |
| `type="image"`    | <input type="image" src="https://raw.githubusercontent.com/mdn/learning-area/master/html/forms/image-type-example/login.png" width="70"> (图像按钮) |
| `type="reset"`    | <input type="reset" class="border border-slate-400"> (重置按钮)                                                                          |
| `type="button"`   | <input type="button" class="border border-slate-400" value="按钮"> (按钮)                                                                |
| `type="submit"`   | <input type="submit" class="border border-slate-400"> (提交按钮)                                                                         |

#### HTML5 中的新 Input 类型

|                         |                                                                      |
| ----------------------- | -------------------------------------------------------------------- |
| `type="color"`          | <input type="color" value="#0FB881" class="border border-slate-400"> (颜色) |
| `type="date"`           | <input type="date" class="border border-slate-400"> (日期)           |
| `type="time"`           | <input type="time" class="border border-slate-400"> (时间)           |
| `type="month"`          | <input type="month" class="border border-slate-400"> (月份)          |
| `type="datetime-local"` | <input type="datetime-local" class="border border-slate-400"> (本地日期时间) |
| `type="week"`           | <input type="week" class="border border-slate-400"> (周)             |
| `type="email"`          | <input type="email" class="border border-slate-400"> (邮箱)          |
| `type="tel"`            | <input type="tel" class="border border-slate-400"> (电话)            |
| `type="url"`            | <input type="url" class="border border-slate-400"> (URL)             |
| `type="number"`         | <input type="number" class="border border-slate-400"> (数字)         |
| `type="search"`         | <input type="search" class="border border-slate-400"> (搜索)         |
| `type="range"`          | <input type="range" class="border border-slate-400"> (范围)          |

### Input CSS 选择器

|               |                           |
| ------------- | ------------------------- |
| `input:focus` | 当其获得键盘焦点时        |

参见：[Input 伪类](/css#input-pseudo-classes)

## HTML meta 标签 {.cols-2}

### Meta 标签 {.row-span-3}

meta 标签描述 HTML 文档中的元数据。它解释了关于 HTML 的附加材料。

```html
<meta charset="utf-8" />
```

```html
<!-- 标题 -->
<title>···</title>
<meta property="og:title" content="···" />
<meta name="twitter:title" content="···" />
```

---

```html
<!-- url -->
<link rel="canonical" href="https://···" />
<meta property="og:url" content="https://···" />
<meta name="twitter:url" content="https://···" />
```

---

```html
<!-- 描述 -->
<meta name="description" content="···" />
<meta property="og:description" content="···" />
<meta name="twitter:description" content="···" />
```

---

```html
<!-- 图像 -->
<meta property="og:image" content="https://···" />
<meta name="twitter:image" content="https://···" />
```

---

```html
<!-- ua -->
<meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1" />
```

---

```html
<!-- 视口 -->
<meta name="viewport" content="width=device-width" />
<meta name="viewport" content="width=1024" />
```

### Open Graph

```html
<meta property="og:type" content="website" />
<meta property="og:locale" content="zh_CN" />
<meta property="og:title" content="HTML 备忘单" />
<meta property="og:url" content="https://r3f.cn/html" />
<meta property="og:image" content="https://xxx.com/image.jpg" />
<meta property="og:site_name" content="你的网站名称" />
<meta property="og:description" content="此页面的描述" />
```

供 Facebook、Instagram、Pinterest、LinkedIn 等使用。

### Twitter Cards

```html
<meta name="twitter:card" content="summary" />
<meta name="twitter:site" content="@FechinLi" />
<meta name="twitter:title" content="HTML 备忘单" />
<meta name="twitter:url" content="https://r3f.cn/html" />
<meta name="twitter:description" content="此页面的描述" />
<meta name="twitter:image" content="https://xxx.com/image.jpg" />
```

参见：[Twitter Card 文档](https://developer.twitter.com/en/docs/tweets/optimize-with-cards/overview/summary)

### 地理标记

```html
<meta name="ICBM" content="45.416667,-75.7" />
<meta name="geo.position" content="45.416667;-75.7" />
<meta name="geo.region" content="ca-on" />
<meta name="geo.placename" content="渥太华" />
```

参见：[地理标记 (Geotagging)](https://zh.wikipedia.org/wiki/地理标记)

## 另请参见

- [HTML 4.01 规范](https://www.w3.org/TR/REC-html40/cover.html#minitoc) _(w3.org)_
