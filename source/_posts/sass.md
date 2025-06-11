---
title: Sass
date: 2020-12-20 22:15:43
background: bg-[#ba6993]
label: CSS
tags:
  - css
categories:
  - 编程
intro: |
  这是一个快速参考备忘单，列出了 [SASS](https://sass-lang.com) 最有用的功能。
plugins:
  - copyCode
  - runCode
---

## Sass 基础

### 简介

- [文档](https://sass-lang.com/documentation) _(sass-lang.com)_
- [X分钟学习Y](https://learnxinyminutes.com/docs/sass/) _(learnxinyminutes.com)_

### 变量

```scss
$defaultLinkColor: #46eac2;

a {
  color: $defaultLinkColor;
}
```

### 字符串插值

```scss
$wk: -webkit-;

.rounded-box {
  #{$wk}border-radius: 4px;
}
```

### 注释

```scss
/*
 块注释
 块注释
 块注释
*/

// 行注释
```

### Mixins (混合)

```scss
@mixin heading-font {
  font-family: sans-serif;
  font-weight: bold;
}
h1 {
  @include heading-font;
}
```

参见: [Mixins](#sass-mixins)

### 嵌套 {.row-span-2}

```scss
.markdown-body {
  a {
    color: blue;
    &:hover {
      color: red;
    }
  }
}
```

#### 属性嵌套

```scss
text: {
  // 类似于 text-align: center
  align: center;
  // 类似于 text-transform: uppercase
  transform: uppercase;
}
```

### Extend (继承)

```scss
.button {
    ···
}
```

```scss
.push-button {
  @extend .button;
}
```

### @import (导入)

```scss
@import "./other_sass_file";
@import "/code", "lists";

// 普通 CSS @imports
@import "theme.css";
@import url(theme);
```

`.sass` 或 `.scss` 扩展名是可选的。

## Sass Mixins (混合)

### 参数

```scss
@mixin font-size($n) {
  font-size: $n * 1.2em;
}
```

```scss
body {
  @include font-size(2);
}
```

### 默认值

```scss
@mixin pad($n: 10px) {
  padding: $n;
}
```

```scss
body {
  @include pad(15px);
}
```

### 默认变量

```scss
$default-padding: 10px;

@mixin pad($n: $default-padding) {
  padding: $n;
}

body {
  @include pad(15px);
}
```

## Sass 颜色函数 {.cols-2}

### rgba

```scss
rgb(100, 120, 140)
rgba(100, 120, 140, .5)
rgba($color, .5)
```

### 混合 (Mixing)

```scss
mix($a, $b, 10%)   // 10% a, 90% b
```

### 修改 HSLA

```scss
darken($color, 5%)    // 变暗
lighten($color, 5%)   // 变亮
```

```scss
saturate($color, 5%)    // 增加饱和度
desaturate($color, 5%)  // 降低饱和度
grayscale($color)       // 灰度
```

```scss
adjust-hue($color, 15deg) // 调整色相
complement($color)        // 补色，类似于 adjust-hue(_, 180deg)
invert($color)            // 反色
```

```scss
fade-in($color, .5)   // 淡入，也写作 opacify()
fade-out($color, .5)  // 淡出，也写作 transparentize()
rgba($color, .5)      // 设置 alpha 透明度为 .5
```

### 获取单个值

#### HSLA

```scss
hue($color)         // 色相 0deg..360deg
saturation($color)  // 饱和度 0%..100%
lightness($color)   // 亮度 0%..100%
alpha($color)       // 透明度 0..1 (也写作 opacity())
```

#### RGB

```scss
red($color)         // 红色值 0..255
green($color)       // 绿色值
blue($color)        // 蓝色值
```

参见: [hue()](http://sass-lang.com/documentation/Sass/Script/Functions.html#hue-instance_method),
[red()](http://sass-lang.com/documentation/Sass/Script/Functions.html#red-instance_method)

### 调整 (Adjustments)

```scss
// 按固定值更改
adjust-color($color, $blue: 5)
adjust-color($color, $lightness: -30%) // darken(_, 30%)
adjust-color($color, $alpha: -0.4)     // fade-out(_, .4)
adjust-color($color, $hue: 30deg)      // adjust-hue(_, 15deg)
```

```scss
// 按百分比更改
scale-color($color, $lightness: 50%)
```

```scss
// 完全更改一个属性
change-color($color, $hue: 180deg)
change-color($color, $blue: 250)
```

支持: `$red`, `$green`, `$blue`, `$hue`, `$saturation`, `$lightness`, `$alpha`

## Sass 其他函数 {.cols-2}

### 字符串

```scss
unquote('hello')  // 移除引号
quote(hello)      // 添加引号
```

```scss
to-upper-case(hello) // 转大写
to-lower-case(hello) // 转小写
```

```scss
str-length(hello world)    // 字符串长度
str-slice(hello, 2, 5)     // "ello" - 基于1的索引，而非基于0
str-insert("abcd", "X", 1) // "Xabcd"
```

### 单位

```scss
unit(3em)        // 'em'
unitless(100px)  // false
```

### 数字

```scss
floor(3.5) // 向下取整
ceil(3.5)  // 向上取整
round(3.5) // 四舍五入
abs(3.5)   // 绝对值
```

```scss
min(1, 2, 3) // 最小值
max(1, 2, 3) // 最大值
```

```scss
percentage(.5)   // 50%
random(3)        // 0..3 之间的随机数
```

### 其他

```scss
variable-exists(red)    // 检查 $red 是否存在
mixin-exists(red-text)  // 检查 @mixin red-text 是否存在
function-exists(redify) // 检查函数 redify 是否存在
```

```scss
global-variable-exists(red) // 检查全局变量 $red 是否存在
```

```scss
selector-append('.menu', 'li', 'a')   // .menu li a
selector-nest('.menu', '&:hover li')  // .menu:hover li
selector-extend(...)
selector-parse(...)
selector-replace(...)
selector-unify(...)
```

## Sass 特性检查 {.cols-2}

### 特性检查

```scss
feature-exists(global-variable-shadowing)
```

### 特性

- global-variable-shadowing (全局变量覆盖)
- extend-selector-pseudoclass (继承选择器伪类)
- units-level-3 (单位级别3)
- at-error (@error指令)

## Sass 循环

### For 循环

```scss
@for $i from 1 through 4 {
  .item-#{$i} {
    left: 20px * $i;
  }
}
```

### Each 循环 (简单)

```scss
$menu-items: home about contact;

@each $item in $menu-items {
  .photo-#{$item} {
    background: url("#{$item}.jpg");
  }
}
```

### Each 循环 (嵌套)

```scss
$backgrounds: (home, "home.jpg"), (about, "about.jpg");

@each $id, $image in $backgrounds {
  .photo-#{$id} {
    background: url($image);
  }
}
```

### While 循环

```scss
$i: 6;
@while $i > 0 {
  .item-#{$i} {
    width: 2em * $i;
  }
  $i: $i - 2;
}
```

## Sass 其他特性

### 条件语句 {.row-span-2}

```scss
@if $position == "left" {
  position: absolute;
  left: 0;
} @else if $position == "right" {
  position: absolute;
  right: 0;
} @else {
  position: static;
}
```

### 插值

```scss
.#{$klass} { ... }      // 类名
call($function-name)    // 函数

@media #{$tablet}
font: #{$size}/#{$line-height}
url("#{$background}.jpg")
```

### 列表 (Lists)

```scss
$list: (a b c);

nth($list, 1)  // 获取第n个元素，从1开始
length($list)  // 列表长度

@each $item in $list { ... } // 遍历列表
```

### 映射 (Maps) {.col-span-2}

```scss
$map: (key1: value1, key2: value2, key3: value3);

map-get($map, key1) // 获取映射中键的值
```
