---
title: CSS 3 速查表
date: 2020-12-25 20:22:47
background: bg-[#3473b5]
tags:
  - web
  - css
  - 样式
categories:
  - 编程
intro: |
  这是一个 CSS 精华的快速参考备忘单，列出了选择器语法、属性、单位和其他有用的信息片段。
plugins:
  - copyCode
  - runCode
---

## 入门指南

### 简介 {.row-span-3}

CSS 功能丰富，不仅仅是简单地布局页面。

#### 外部样式表

```html {.wrap}
<link href="./path/to/stylesheet/style.css" rel="stylesheet" type="text/css" />
```

#### 内部样式表

```html
<style>
  body {
    background-color: linen;
  }
</style>
```

#### 内联样式

```html {.wrap}
<h2 style="text-align: center;">居中文本</h2>

<p style="color: blue; font-size: 18px;">蓝色，18磅文本</p>
```

### 添加类

```html
<div class="classname"></div>
<div class="class1 ... classn"></div>
```

一个元素支持多个类。

### !important

```css
.post-title {
  color: blue !important;
}
```

覆盖所有先前的样式规则。

### 选择器

```css
h1 {
}
#job-title {
}
div.hero {
}
div > p {
}
```

参见：[选择器](#css-selectors)

### 文本颜色

```css
color: #2a2aff;
color: green;
color: rgb(34, 12, 64, 0.6);
color: hsla(30 100% 50% / 0.6);
```

参见：[颜色](#css-colors)

### 背景

```css
background-color: blue;
background-image: url("nyan-cat.gif");
background-image: url("../image.png");
```

参见：[背景](#css-backgrounds)

### 字体

```css
.page-title {
  font-weight: bold;
  font-size: 30px;
  font-family: "Courier New";
}
```

参见：[字体](#css-fonts)

### 定位

```css
.box {
  position: relative;
  top: 20px;
  left: 20px;
}
```

另请参阅：[Position](https://learn-the-web.algonquindesign.ca/topics/css-layout-cheat-sheet/)

### 动画

```css
animation: 300ms linear 0s infinite;

animation: bounce 300ms linear infinite;
```

参见：[动画](#css-animation)

### 注释

```css
/* 这是单行注释 */

/* 这是
   多行注释 */
```

### Flex 布局

```css
div {
  display: flex;
  justify-content: center;
}
div {
  display: flex;
  justify-content: flex-start;
}
```

参见：[Flexbox](#css-flexbox) | [Flex 技巧](#css-flexbox-tricks)

### Grid 布局

```css
#container {
  display: grid;
  grid: repeat(2, 60px) / auto-flow 80px;
}

#container > div {
  background-color: #8ca0ff;
  width: 50px;
  height: 50px;
}
```

参见：[Grid 布局](#css-grid-layout)

### 变量和计数器

```css
counter-set: subsection;
counter-increment: subsection;
counter-reset: subsection 0;

:root {
  --bg-color: brown;
}
element {
  background-color: var(--bg-color);
}
```

参见：[动态内容](#css-dynamic-content)

## CSS 选择器

### 示例 {.row-span-2}

#### 分组选择器

```css
h1,
h2 {
  color: red;
}
```

#### 链式选择器

```css
h3.section-heading {
  color: blue;
}
```

#### 属性选择器

```css
div[attribute="SomeValue"] {
  background-color: red;
}
```

#### 首子元素选择器

```css
p:first-child {
  font-weight: bold;
}
```

#### 无子元素选择器

```css
.box:empty {
  background: lime;
  height: 80px;
  width: 80px;
}
```

### 基本选择器

|              |                             |
| ------------ | --------------------------- |
| `*`          | 所有元素                    |
| `div`        | 所有 div 标签               |
| `.classname` | 所有带此类的元素            |
| `#idname`    | 带此 ID 的元素              |
| `div,p`      | 所有 div 和 p 标签          |
| `#idname *`  | `#idname` 内的所有元素      |

另请参阅：[类型](https://developer.mozilla.org/en-US/docs/Web/CSS/Type_selectors) /
[类](https://developer.mozilla.org/en-US/docs/Web/CSS/Class_selectors) /
[ID](https://developer.mozilla.org/en-US/docs/Web/CSS/ID_selectors) /
[通用](https://developer.mozilla.org/en-US/docs/Web/CSS/Universal_selectors) 选择器

### 组合器

| 选择器          | 描述                                  |
| --------------- | ------------------------------------- |
| `div.classname` | 具有特定类名的 Div                    |
| `div#idname`    | 具有特定 ID 的 Div                    |
| `div p`         | div 内的段落                          |
| `div > p`       | 所有 p 标签<br>_div 内一层深_          |
| `div + p`       | 紧跟 div 后的 P 标签                  |
| `div ~ p`       | div 之后的所有同级 P 标签             |

另请参阅：[相邻兄弟](https://developer.mozilla.org/en-US/docs/Web/CSS/Adjacent_sibling_combinator) /
[后续兄弟](https://developer.mozilla.org/en-US/docs/Web/CSS/General_sibling_combinator) /
[子代](https://developer.mozilla.org/en-US/docs/Web/CSS/Child_combinator) 选择器

### 属性选择器

|                      |                                    |
| -------------------- | ---------------------------------- |
| `a[target]`          | 带有 <yel>target</yel> 属性        |
| `a[target="_blank"]` | 在新标签页中打开                   |
| `a[href^="/index"]`  | 以 <yel>/index</yel> 开头           |
| `[class|="chair"]`   | 以 <yel>chair</yel> 开头            |
| `[class*="chair"]`   | 包含 <yel>chair</yel>              |
| `[title~="chair"]`   | 包含单词 <yel>chair</yel>          |
| `a[href$=".doc"]`    | 以 <yel>.doc</yel> 结尾            |
| `[type="button"]`    | 指定类型                           |

另请参阅：[属性选择器](https://developer.mozilla.org/en-US/docs/Web/CSS/Attribute_selectors)

### 用户行为伪类

|              |                         |
| ------------ | ----------------------- |
| `a:link    ` | 正常状态的链接          |
| `a:active  ` | 点击状态的链接          |
| `a:hover   ` | 鼠标悬停的链接          |
| `a:visited ` | 已访问的链接            |

### 伪类

|                   |                                                                                         |
| ----------------- | --------------------------------------------------------------------------------------- |
| `p::after`        | 在 p 之后添加内容                                                                       |
| `p::before`       | 在 p 之前添加内容                                                                       |
| `p::first-letter` | p 中的首字母                                                                            |
| `p::first-line`   | p 中的首行                                                                              |
| `::selection`     | 用户选中的部分                                                                          |
| `::placeholder`   | [占位符](https://developer.mozilla.org/en-US/docs/Web/CSS/::placeholder) 属性           |
| `:root`           | 文档根元素                                                                              |
| `:target`         | 高亮活动锚点                                                                            |
| `div:empty`       | 没有子元素的元素                                                                        |
| `p:lang(en)`      | 具有 en 语言属性的 P                                                                    |
| `:not(span)`      | 不是 span 的元素                                                                        |

### 输入伪类

|                       |                                                                                             |
| --------------------- | ------------------------------------------------------------------------------------------- |
| `input:checked`       | 选中的输入                                                                                  |
| `input:disabled`      | 禁用的输入                                                                                  |
| `input:enabled`       | 启用的输入                                                                                  |
| `input:focus`         | 输入框获得焦点                                                                              |
| `input:in-range`      | 值在范围内                                                                                  |
| `input:out-of-range`  | 输入值超出范围                                                                              |
| `input:valid`         | 具有有效值的输入                                                                            |
| `input:invalid`       | 具有无效值的输入                                                                            |
| `input:optional`      | 没有 required 属性                                                                        |
| `input:required`      | 具有 required 属性的输入                                                                    |
| `input:read-only`     | 具有 readonly 属性                                                                        |
| `input:read-write`    | 没有 readonly 属性                                                                        |
| `input:indeterminate` | 处于[不确定](https://developer.mozilla.org/en-US/docs/Web/CSS/:indeterminate)状态           |

### 结构伪类

|                         |                            |
| ----------------------- | -------------------------- |
| `p:first-child`         | 首个子元素                 |
| `p:last-child`          | 末尾子元素                 |
| `p:first-of-type`       | 某种类型的首个             |
| `p:last-of-type`        | 某种类型的末尾             |
| `p:nth-child(2)`        | 其父元素的第二个子元素     |
| `p:nth-child(3n42)`     | Nth-child (an + b) 公式    |
| `p:nth-last-child(2)`   | 从后往前数的第二个子元素   |
| `p:nth-of-type(2)`      | 其父元素的第二个 p 元素    |
| `p:nth-last-of-type(2)` | ...从后往前数              |
| `p:only-of-type`        | 其父元素的唯一此类元素     |
| `p:only-child`          | 其父元素的唯一子元素       |

## CSS 字体

### 属性 {.row-span-3}

| 属性              | 描述                          |
| ----------------- | ----------------------------- |
| `font-family:`    | <字体> <字体N>                |
| `font-size:`      | <大小>                        |
| `letter-spacing:` | <大小>                        |
| `line-height:`    | <数字>                        |

| `font-weight:` | <数字> / bold / normal | | `font-style:` | italic / normal | | `text-decoration:` | underline / none |

| `text-align:` | left / right<br>center / justify | | `text-transform:` | capitalize / uppercase / lowercase |
{.left-text}

另请参阅：[字体](https://developer.mozilla.org/en-US/docs/Web/CSS/font)

### 简写 {.secondary .col-span-2}

|         | 样式     | 字重   | 大小 (必需)     |     | 行高        | 字体族 (必需)     |
| ------- | -------- | ------ | --------------- | --- | ----------- | ----------------- |
| `font:` | `italic` | `400`  | `14px`          | `/` | `1.5`       | `sans-serif`      |
|         | 样式     | 字重   | 大小 (必需)     |     | 行高        | 字体族 (必需)     |

### 示例

```css
font-family: Arial, sans-serif;
font-size: 12pt;
letter-spacing: 0.02em;
```

### 大小写转换 {.row-span-2}

```css
/* Hello */
text-transform: capitalize;

/* HELLO */
text-transform: uppercase;

/* hello */
text-transform: lowercase;
```

### @font-face

```css
@font-face {
  font-family: "Glegoo";
  src: url("../Glegoo.woff");
}
```

## CSS 颜色

### 命名颜色

```css
color: red;
color: orange;
color: tan;
color: rebeccapurple;
```

### 十六进制颜色

```css
color: #090;
color: #009900;
color: #090a;
color: #009900aa;
```

### rgb() 颜色

```css
color: rgb(34, 12, 64, 0.6);
color: rgba(34, 12, 64, 0.6);
color: rgb(34 12 64 / 0.6);
color: rgba(34 12 64 / 0.3);
color: rgb(34 12 64 / 60%);
color: rgba(34.6 12 64 / 30%);
```

### HSL 颜色

```css
color: hsl(30, 100%, 50%, 0.6);
color: hsla(30, 100%, 50%, 0.6);
color: hsl(30 100% 50% / 0.6);
color: hsla(30 100% 50% / 0.6);
color: hsl(30 100% 50% / 60%);
color: hsla(30.2 100% 50% / 60%);
```

### 其他

```css
color: inherit;
color: initial;
color: unset;
color: transparent;

color: currentcolor; /* keyword */
```

## CSS 背景

### 属性 {.row-span-2}

| 属性          | 描述                       |
| ------------- | -------------------------- |
| `background:` | _(简写)_                   |

| `background-color:` | 参见：[颜色](#css-colors) | | `background-image:` | url(...) | | `background-position:` | left/center/right<br/>top/center/bottom | | `background-size:` | cover X Y | | `background-clip:` | border-box<br/>padding-box<br/>content-box | | `background-repeat:` | no-repeat<br/>repeat-x<br/>repeat-y | | `background-attachment:` | scroll/fixed/local |
{.left-text}

### 简写 {.secondary .col-span-2}

|               | 颜色   | 图像         | 位置X    | 位置Y    |     | 大小           | 重复        | 附件       |
| ------------- | ------ | ------------ | --------- | --------- | --- | -------------- | ----------- | ---------- |
| `background:` | `#ff0` | `url(a.jpg)` | `left`    | `top`     | `/` | `100px` `auto` | `no-repeat` | `fixed;`   |
| `background:` | `#abc` | `url(b.png)` | `center`  | `center`  | `/` | `cover`        | `repeat-x`  | `local;`   |
|               | 颜色   | 图像         | 位置X     | 位置Y     |     | 大小           | 重复        | 附件..     |

### 示例 {.col-span-2}

```css {.wrap}
background: url(img_man.jpg) no-repeat center;

background:
  url(img_flwr.gif) right bottom no-repeat,
  url(paper.gif) left top repeat;

background: rgb(2, 0, 36);
background: linear-gradient(90deg, rgba(2, 0, 36, 1) 0%, rgba(13, 232, 230, 1) 35%, rgba(0, 212, 255, 1) 100%);
```

## CSS 盒模型

### 最大/最小值

```css
.column {
  max-width: 200px;
  width: 500px;
}
```

另请参阅：[max-width](https://developer.mozilla.org/en-US/docs/Web/CSS/max-width) /
[min-width](https://developer.mozilla.org/en-US/docs/Web/CSS/min-width) /
[max-height](https://developer.mozilla.org/en-US/docs/Web/CSS/max-height) /
[min-height](https://developer.mozilla.org/en-US/docs/Web/CSS/min-height)

### 外边距 / 内边距

```css
.block-one {
  margin: 20px;
  padding: 10px;
}
```

另请参阅：[外边距](https://developer.mozilla.org/en-US/docs/Web/CSS/margin) /
[内边距](https://developer.mozilla.org/en-US/docs/Web/CSS/padding)

### Box-sizing

```css
.container {
  box-sizing: border-box;
}
```

另请参阅：[Box-sizing](https://developer.mozilla.org/en-US/docs/Web/CSS/Box-sizing)

### 可见性

```css
.invisible-elements {
  visibility: hidden;
}
```

另请参阅：[可见性](https://developer.mozilla.org/en-US/docs/Web/CSS/visibility)

### Auto 关键字

```css
div {
  margin: auto;
}
```

另请参阅：[外边距](https://developer.mozilla.org/en-US/docs/Web/CSS/margin)

### 溢出

```css
.small-block {
  overflow: scroll;
}
```

另请参阅：[溢出](https://developer.mozilla.org/en-US/docs/Web/CSS/overflow)

## CSS 动画 {.cols-5}

### 简写 {.col-span-5 .secondary}

|              | 名称     | 持续时间 | 时间函数        | 延迟    | 次数       | 方向                | 填充模式  | 播放状态   |
| ------------ | -------- | -------- | --------------- | ------- | ---------- | ------------------- | --------- | ---------- |
| `animation:` | `bounce` | `300ms`  | `linear`        | `100ms` | `infinite` | `alternate-reverse` | `both`    | `reverse`  |
|              | 名称     | 持续时间 | 时间函数        | 延迟    | 次数       | 方向                | 填充模式  | 播放状态   |

### 属性 {.row-span-2 .col-span-2}

| 属性                         | 值                                                     |
| ---------------------------- | ------------------------------------------------------ |
| `animation:`                 | _(简写)_                                               |
| `animation-name:`            | <名称>                                                 |
| `animation-duration:`        | <时间>ms                                               |
| `animation-timing-function:` | ease / linear / ease-in / ease-out / ease-in-out       |
| `animation-delay:`           | <时间>ms                                               |
| `animation-iteration-count:` | infinite / <数字>                                      |
| `animation-direction:`       | normal / reverse / alternate / alternate-reverse       |
| `animation-fill-mode:`       | none / forwards / backwards / both / initial / inherit |
| `animation-play-state:`      | normal / reverse / alternate / alternate-reverse       |

{.left-text}

另请参阅：[动画](https://developer.mozilla.org/en-US/docs/Web/CSS/animation)

### 示例 {.col-span-3}

```css
/* @keyframes duration | timing-function | delay |
   iteration-count | direction | fill-mode | play-state | name */
animation: 3s ease-in 1s 2 reverse both paused slidein;

/* @keyframes duration | timing-function | delay | name */
animation: 3s linear 1s slidein;

/* @keyframes duration | name */
animation: 3s slidein;

animation: 4s linear 0s infinite alternate move_eye;
animation: bounce 300ms linear 0s infinite normal;
animation: bounce 300ms linear infinite;
animation: bounce 300ms linear infinite alternate-reverse;
animation: bounce 300ms linear 2s infinite alternate-reverse forwards normal;
```

### Javascript 事件 {.col-span-3}

```js
.one('webkitAnimationEnd oanimationend msAnimationEnd animationend')
```

## CSS Flexbox {.cols-2}

### 简单示例

```css
.container {
  display: flex;
}
```

```css
.container > div {
  flex: 1 1 auto;
}
```

### 容器 {.row-span-2}

.container {

```css
display: flex;
display: inline-flex;
```

```css
flex-direction: row; /* 从左到右 - 默认 */
flex-direction: row-reverse; /* 从右到左 */
flex-direction: column; /* 从上到下 */
flex-direction: column-reverse; /* 从下到上 */
```

```css
flex-wrap: nowrap; /* 单行 */
flex-wrap: wrap; /* 多行 */
```

```css
align-items: flex-start; /* 垂直对齐到顶部 */
align-items: flex-end; /* 垂直对齐到底部 */
align-items: center; /* 垂直居中对齐 */
align-items: stretch; /* 所有项目等高 (默认) */
```

```css
justify-content: flex-start; /* [xxx        ] */
justify-content: center; /* [    xxx    ] */
justify-content: flex-end; /* [        xxx] */
justify-content: space-between; /* [x    x    x] */
justify-content: space-around; /* [ x   x   x ] */
justify-content: space-evenly; /* [  x  x  x  ] */
```

}

### 子项

.container > div {

```css
/* 如下所示：*/
flex: 1 0 auto;

/* 等同于：*/
flex-grow: 1;
flex-shrink: 0;
flex-basis: auto;
```

```css
order: 1;
```

```css
align-self: flex-start; /* 左对齐 */
margin-left: auto; /* 右对齐 */
```

}

## CSS Flexbox 技巧

### 垂直居中

```css
.container {
  display: flex;
}

.container > div {
  width: 100px;
  height: 100px;
  margin: auto;
}
```

### 垂直居中 (2)

```css
.container {
  display: flex;

  /* 垂直 */
  align-items: center;

  /* 水平 */
  justify-content: center;
}
```

### 重新排序

```css
.container > .top {
  order: 1;
}

.container > .bottom {
  order: 2;
}
```

### 移动端布局

```css
.container {
  display: flex;
  flex-direction: column;
}

.container > .top {
  flex: 0 0 100px;
}

.container > .content {
  flex: 1 0 auto;
}
```

一个固定高度的顶部栏和一个动态高度的内容区域。

### 表格样式 {.col-span-2}

```css
.container {
  display: flex;
}

/* 这里的 'px' 值仅为建议的百分比 */
.container > .checkbox {
  flex: 1 0 20px;
}
.container > .subject {
  flex: 1 0 400px;
}
.container > .date {
  flex: 1 0 120px;
}
```

这将创建具有不同宽度但会根据情况相应调整大小的列。

### 垂直对齐

```css
.container {
  align-items: center;
}
```

垂直居中所有项目。

### 左右对齐 {.col-span-2}

```css
.menu > .left {
  align-self: flex-start;
}
.menu > .right {
  align-self: flex-end;
}
```

## CSS Grid 布局

### 网格模板列

```css
#grid-container {
  display: grid;
  width: 100px;
  grid-template-columns: 20px 20% 60%;
}
```

### fr 相对单位

```css
.grid {
  display: grid;
  width: 100px;
  grid-template-columns: 1fr 60px 1fr;
}
```

### 网格间距

```css
/*行间距为 20px*/
/*列间距为 10px*/
#grid-container {
  display: grid;
  grid-gap: 20px 10px;
}
```

### CSS 块级网格

```css
#grid-container {
  display: block;
}
```

### CSS grid-row

CSS 语法：

- grid-row: grid-row-start / grid-row-end;

#### 示例

```css
.item {
  grid-row: 1 / span 2;
}
```

### CSS 内联级网格

```css
#grid-container {
  display: inline-grid;
}
```

### minmax() 函数

```css {.wrap}
.grid {
  display: grid;
  grid-template-columns: 100px minmax(100px, 500px) 100px;
}
```

### grid-row-start 和 grid-row-end

CSS 语法：

- grid-row-start: auto|row-line;<br>
- grid-row-end: auto|row-line|span n;

#### 示例

```css
grid-row-start: 2;
grid-row-end: span 2;
```

### CSS grid-row-gap

```css
grid-row-gap: length;
```

任何合法的长度值，如 px 或 %。0 是默认值

### CSS grid-area

```css
.item1 {
  grid-area: 2 / 1 / span 2 / span 3;
}
```

### Justify Items (对齐网格项 - 主轴)

```css
#container {
  display: grid;
  justify-items: center;
  grid-template-columns: 1fr;
  grid-template-rows: 1fr 1fr 1fr;
  grid-gap: 10px;
}
```

### CSS grid-template-areas

```css
.item {
  grid-area: nav;
}
.grid-container {
  display: grid;
  grid-template-areas:
    "nav nav . ."
    "nav nav . .";
}
```

### Justify Self (对齐单个网格项 - 主轴)

```css
#grid-container {
  display: grid;
  justify-items: start;
}

.grid-items {
  justify-self: end;
}
```

网格项位于行的右侧（末端）。

### Align Items (对齐网格项 - 交叉轴)

```css
#container {
  display: grid;
  align-items: start;
  grid-template-columns: 1fr;
  grid-template-rows: 1fr 1fr 1fr;
  grid-gap: 10px;
}
```

## CSS 动态内容

### 变量

定义 CSS 变量

```css
:root {
  --first-color: #16f;
  --second-color: #ff7;
}
```

变量用法

```css
#firstParagraph {
  background-color: var(--first-color);
  color: var(--second-color);
}
```

另请参阅：[CSS 变量](https://developer.mozilla.org/en-US/docs/Web/CSS/--*)

### 计数器

```css
/* 设置 "my-counter" 为 0 */
counter-set: my-counter;
```

```css
/* "my-counter" 增加 1 */
counter-increment: my-counter;
```

```css
/* "my-counter" 减少 1 */
counter-increment: my-counter -1;
```

```css
/* 重置 "my-counter" 为 0 */
counter-reset: my-counter;
```

另请参阅：[计数器设置](https://developer.mozilla.org/en-US/docs/Web/CSS/counter-set)

### 使用计数器

```css
body {
  counter-reset: section;
}

h3::before {
  counter-increment: section;
  content: "Section." counter(section);
}
```

```css
ol {
  counter-reset: section;
  list-marker-type: none;
}

li::before {
  counter-increment: section;
  content: counters(section, ".") " ";
}
```

## Css 3 技巧

### 平滑滚动条

```css
html {
  scroll-behavior: smooth;
}
```

[点击我](#css-getting-started)，页面将平滑滚动到“入门指南”

## 现代 CSS

### 容器查询 (大小)

```css
.element-wrap {
  container: element / inline-size;
}
@container element (min-inline-size: 300px) {
  .element {
    display: flex;
    gap: 1rem;
  }
}
```

### 容器查询 (样式)

```css
.container {
  --variant: 1;

  &.variant2 {
    --variant: 2;
  }
}

@container style(--variant: 1) {
  button {
  } /* 你不能直接为 .container 设置样式，但可以选择其内部元素 */
  .other-things {
  }
}

@container style(--variant: 2) {
  button {
  }
  .whatever {
  }
}
```

### 容器单位

- 单位包括 cqw (“容器查询宽度”),
- cqh (“容器查询高度”),
- cqi (“容器查询内联尺寸”),
- cqb (“容器查询块级尺寸”),
- cqmin (cqi 和 cqb 中的较小者),
- 以及 cqmax (cqi 和 cqb 中的较大者)

```css
.card {
  padding: 5cqi;
  font-size: 4cqi;
  border: 1cqi solid brown;
  height: 100%;
}

h2 {
  font-size: 10cqi;
  margin-block: 0 3cqi;
}
```

### :has() 伪选择器

```css
figure:has(figcaption) {
  border: 1px solid black;
  padding: 0.5rem;
}
```

### 嵌套

```css
.cards {
  .card {
    & .card-description {
      color: blue;
    }
    & .card-title {
      color: red;
    }
  }
}
```

### 作用域

```css
@scope {
  :scope {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 1rem;
    padding: 1rem;
    border: 1px solid black;
  }
  .card {
    padding: 1rem;
    border: 1px solid black;
    background: lightgray;
    h2 {
      margin: 0 0 1rem 0;
    }
  }
}
```

### 层叠层

```css
/* 指定层叠中应用样式的顺序 */
@layer legacyCard, newCard;

/* 假设你有很多样式 */
@layer newCard {
  .card {
    background-color: red;
  }
}
@layer legacyCard {
  .card {
    background-color: green;
  }
}
```

### 逻辑属性

```css
button {
  background-color: #4caf50;
  border: none;
  color: white;
  padding: 0.5rem 1.5rem;
  text-decoration: none;
  font: inherit;
  border-radius: 4px;
  .icon {
    position: relative;
    top: 0.125em;
    fill: white;
    width: 1em;
    aspect-ratio: 1;
    margin-inline-end: 0.25rem;
  }
}
```

### P3 颜色

```html
<div class="container">
  <div class="swatch">
    <style contenteditable>
      @scope {
        :scope {
          background-color: color(display-p3 1 0.5 0);
        }
      }
    </style>
  </div>
  <div class="swatch">
    <style contenteditable>
      @scope {
        :scope {
          background-color: oklch(61.88% 0.286 342.4);
        }
      }
    </style>
  </div>
  <div class="swatch">
    <style contenteditable>
      @scope {
        :scope {
          background-color: oklab(0.73 0.15 0.16);
        }
      }
    </style>
  </div>

  <div class="swatch">
    <style contenteditable>
      @scope {
        :scope {
          background-image: linear-gradient(to right in oklch, red, blue);
        }
      }
    </style>
  </div>

  <div class="swatch">
    <style contenteditable>
      @scope {
        :scope {
          background-image: linear-gradient(to right in oklab, red, blue);
        }
      }
    </style>
  </div>

  <div class="swatch">
    <style contenteditable>
      @scope {
        :scope {
          background-image: linear-gradient(to right in srgb, red, blue);
        }
      }
    </style>
  </div>
</div>
```

### 颜色混合

```css
.swatch {
  color: white;
  width: 100px;
  aspect-ratio: 1;
  display: grid;
  place-items: center;
  text-align: center;

  &:nth-child(1) {
    background-color: var(--bg);
  }
  &:nth-child(2) {
    background-color: color-mix(in oklch, var(--bg), black 30%);
  }
  &:nth-child(3) {
    background-color: color-mix(in oklch, var(--bg), white 30%);
  }
}
```

### 外边距裁剪

```css
.container {
  /* 防止元素末尾出现“多余”外边距 */
  margin-trim: block-end;

  /* 类似这样的元素可能是罪魁祸首，但也可能是任何元素 */
  > p {
    margin-block-end: 1rem;
  }
}
```

### 文本换行

```css
.balance {
  text-wrap: balance;
}
.pretty {
  text-wrap: pretty;
}

html {
  font-family: system-ui, sans-serif;
}

main {
  max-inline-size: 60ch;
  margin-inline: auto;
}
```

### 子网格

```css
.grid {
  display: grid;
  grid-template-columns: repeat(9, 1fr);
  grid-template-rows: repeat(4, minmax(100px, auto));
}

.item {
  display: grid;
  grid-column: 2 / 7;
  grid-row: 2 / 4;
  grid-template-columns: subgrid;
  grid-template-rows: repeat(3, 80px);
}

.subitem {
  grid-column: 3 / 6;
  grid-row: 1 / 3;
}
```

## 另请参阅 {.cols-1}

- [frontendmasters.com ](https://frontendmasters.com/blog/what-you-need-to-know-about-modern-css-spring-2024-edition/)
- [CSS 选择器备忘单](https://frontend30.com/css-selectors-cheatsheet/) _(frontend30.com)_
- [MDN: 使用 CSS flexbox](https://developer.mozilla.org/en-US/docs/Web/Guide/CSS/Flexible_boxes)
- [终极 flexbox 备忘单](http://www.sketchingwithcss.com/samplechapter/cheatsheet.html)
- [GRID: 简单的可视化备忘单](http://grid.malven.co/)
- [CSS Tricks: Grid 完全指南](https://css-tricks.com/snippets/css/complete-guide-grid/)
- [浏览器支持](https://caniuse.com/#feat=css-grid)

