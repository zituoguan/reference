---
title: jQuery
date: 2020-12-24 21:08:21
background: bg-[#2c63a2]
tags:
  - web
  - js
  - javascript
  - 库
categories:
  - 编程
intro: |
  这份 [jQuery](https://jquery.com/) 速查表对初学者和有经验的开发者来说都是一个很好的参考。
plugins:
  - tooltip
  - copyCode
  - runCode
---

## 入门指南

### 引入 jQuery

```html {.wrap}
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.5.1/jquery.min.js"></script>
```

#### 官方 CDN

```html {.wrap}
<script src="https://code.jquery.com/jquery-3.5.1.min.js" crossorigin="anonymous"></script>
```

### jQuery 语法

```javascript
$(selector).methodOrFunction();
```

#### 示例：

```javascript
$("#menu").on("click", function () {
  $(this).hide();
});

$("body").css("background", "red");
```

### jQuery 文档就绪

```javascript
$(document).ready(function () {
  // DOM 加载完成后运行。
  alert("DOM 已完全加载！");
});
```

```javascript
$(function () {
  // DOM 加载完成后运行。
  alert("DOM 已完全加载！");
});
```

## jQuery 选择器

### 示例 {.secondary}

```javascript
$("button").click(() => {
  $(":button").css("color", "red");
});
```

#### 组合选择器

```javascript
$("selector1, selector2 ...selectorn");
```

### 基础选择器

<!-- prettier-ignore -->
- [*](https://api.jquery.com/all-selector/){data-tooltip="选择所有元素。"}
- [.class](https://api.jquery.com/class-selector/){data-tooltip="选择所有具有给定类名的元素。"}
- [element](https://api.jquery.com/element-selector/){data-tooltip="选择所有具有给定标签名称的元素。"}
- [#id](https://api.jquery.com/id-selector/){data-tooltip="选择具有给定 id 属性的单个元素。"}
- [:hidden](https://api.jquery.com/hidden-selector/){data-tooltip="选择所有隐藏的元素。"}
- [:visible](https://api.jquery.com/visible-selector/){data-tooltip="选择所有可见的元素。"}
- [:contains()](https://api.jquery.com/contains-selector/){data-tooltip="选择所有包含指定文本的元素。"}
- [:empty](https://api.jquery.com/empty-selector/){data-tooltip="选择所有没有子元素（包括文本节点）的元素。"}
- [:has()](https://api.jquery.com/has-selector/){data-tooltip="选择包含至少一个与指定选择器匹配的元素的元素。"}
- [:parent](https://api.jquery.com/parent-selector/){data-tooltip="选择所有至少有一个子节点（元素或文本）的元素。"}
- [parent &gt; child](https://api.jquery.com/child-selector/){data-tooltip="选择由 parent 指定的元素的、由 child 指定的所有直接子元素。"}
- [ancestor descendant](https://api.jquery.com/descendant-selector/){data-tooltip="选择作为给定祖先元素后代的所有元素。"}
- [prev + next](https://api.jquery.com/next-adjacent-Selector/){data-tooltip="选择所有紧接在同级 prev 元素之后且匹配 next 的元素。"}
- [prev ~ siblings](https://api.jquery.com/next-siblings-selector/){data-tooltip="选择所有在 prev 元素之后、具有相同父元素且匹配筛选 siblings 选择器的同级元素。"}

{.marker-none .cols-3}

### 基本筛选器

<!-- prettier-ignore -->
- [:animated](https://api.jquery.com/animated-selector/){data-tooltip="选择在选择器运行时正处于动画过程中的所有元素。"}
- [:eq()](https://api.jquery.com/eq-selector/){data-tooltip="在匹配集合中选择索引为 n 的元素。"}
- [:even](https://api.jquery.com/even-selector/){data-tooltip="选择偶数索引的元素（从零开始）。另请参见 :odd。"}
- [:first](https://api.jquery.com/first-selector/){data-tooltip="选择第一个匹配的 DOM 元素。"}
- [:gt()](https://api.jquery.com/gt-selector/){data-tooltip="在匹配集合中选择索引大于指定索引的所有元素。"}
- [:header](https://api.jquery.com/header-selector/){data-tooltip="选择所有标题元素，如 h1、h2、h3 等。"}
- [:lang()](https://api.jquery.com/lang-selector/){data-tooltip="选择所有指定语言的元素。"}
- [:last](https://api.jquery.com/last-selector/){data-tooltip="选择最后一个匹配的元素。"}
- [:lt()](https://api.jquery.com/lt-selector/){data-tooltip="在匹配集合中选择索引小于指定索引的所有元素。"}
- [:not()](https://api.jquery.com/not-selector/){data-tooltip="选择所有与给定选择器不匹配的元素。"}
- [:odd](https://api.jquery.com/odd-selector/){data-tooltip="选择奇数索引的元素（从零开始）。另请参见 :even。"}
- [:root](https://api.jquery.com/root-selector/){data-tooltip="选择作为文档根的元素。"}
- [:target](https://api.jquery.com/target-selector/){data-tooltip="选择由文档 URI 的片段标识符指示的目标元素。"}

{.marker-none .cols-3}

### 属性选择器

<!-- prettier-ignore -->
- [[name|="value"]](https://api.jquery.com/attribute-contains-prefix-selector/){data-tooltip="选择具有指定属性且其值等于给定字符串或以该字符串后跟连字符 (-) 开头的元素。"}
- [[name*="value"]](https://api.jquery.com/attribute-contains-selector/){data-tooltip="选择具有指定属性且其值包含给定子字符串的元素。"}
- [[name~="value"]](https://api.jquery.com/attribute-contains-word-selector/){data-tooltip="选择具有指定属性且其值包含由空格分隔的给定单词的元素。"}
- [[name$="value"]](https://api.jquery.com/attribute-ends-with-selector/){data-tooltip="选择具有指定属性且其值以给定字符串精确结尾的元素。比较区分大小写。"}
- [[name="value"]](https://api.jquery.com/attribute-equals-selector/){data-tooltip="选择具有指定属性且其值精确等于特定值的元素。"}
- [[name!="value"]](https://api.jquery.com/attribute-not-equal-selector/){data-tooltip="选择不具有指定属性，或者具有指定属性但其值不等于特定值的元素。"}
- [[name^="value"]](https://api.jquery.com/attribute-starts-with-selector/){data-tooltip="选择具有指定属性且其值以给定字符串精确开头的元素。"}
- [[name]](https://api.jquery.com/has-attribute-selector/){data-tooltip="选择具有指定属性（任何值）的元素。"}
- [[name="value"][name2="value2"]](https://api.jquery.com/multiple-attribute-selector/){data-tooltip="匹配所有符合指定属性筛选器的元素。"} {.col-span-2}

{.marker-none .cols-2}

### 子元素筛选器

<!-- prettier-ignore -->
- [:first-child](https://api.jquery.com/first-child-selector/){data-tooltip="选择所有作为其父元素的第一个子元素的元素。"}
- [:first-of-type](https://api.jquery.com/first-of-type-selector/){data-tooltip="选择所有在同名同级元素中排在第一个的元素。"}
- [:last-child](https://api.jquery.com/last-child-selector/){data-tooltip="选择所有作为其父元素的最后一个子元素的元素。"}
- [:last-of-type](https://api.jquery.com/last-of-type-selector/){data-tooltip="选择所有在同名同级元素中排在最后一个的元素。"}
- [:nth-child()](https://api.jquery.com/nth-child-selector/){data-tooltip="选择所有作为其父元素的第 n 个子元素的元素。"}
- [:nth-last-child()](https://api.jquery.com/nth-last-child-selector/){data-tooltip="选择所有作为其父元素的第 n 个子元素，从最后一个元素开始倒数。"}
- [:nth-last-of-type()](https://api.jquery.com/nth-last-of-type-selector/){data-tooltip="选择所有相对于同名同级元素而言，作为其父元素的第 n 个子元素，从最后一个元素开始倒数。"}
- [:nth-of-type()](https://api.jquery.com/nth-of-type-selector/){data-tooltip="选择所有相对于同名同级元素而言，作为其父元素的第 n 个子元素。"}
- [:only-child](https://api.jquery.com/only-child-selector/){data-tooltip="选择所有作为其父元素的唯一子元素的元素。"}
- [:only-of-type()](https://api.jquery.com/only-of-type-selector/){data-tooltip="选择所有没有同名同级元素的元素。"}

{.marker-none .cols-2}

### 表单选择器

<!-- prettier-ignore -->
- [:button](https://api.jquery.com/button-selector/){data-tooltip="选择所有 button 元素和 type 为 button 的元素。"}
- [:checkbox](https://api.jquery.com/checkbox-selector/){data-tooltip="选择所有 type 为 checkbox 的元素。"}
- [:checked](https://api.jquery.com/checked-selector/){data-tooltip="匹配所有被选中或选定的元素。"}
- [:disabled](https://api.jquery.com/disabled-selector/){data-tooltip="选择所有被禁用的元素。"}
- [:enabled](https://api.jquery.com/enabled-selector/){data-tooltip="选择所有被启用的元素。"}
- [:focus](https://api.jquery.com/focus-selector/){data-tooltip="如果元素当前具有焦点，则选择该元素。"}
- [:file](https://api.jquery.com/file-selector/){data-tooltip="选择所有 type 为 file 的元素。"}
- [:image](https://api.jquery.com/image-selector/){data-tooltip="选择所有 type 为 image 的元素。"}
- [:input](https://api.jquery.com/input-selector/){data-tooltip="选择所有 input、textarea、select 和 button 元素。"}
- [:password](https://api.jquery.com/password-selector/){data-tooltip="选择所有 type 为 password 的元素。"}
- [:radio](https://api.jquery.com/radio-selector/){data-tooltip="选择所有 type 为 radio 的元素。"}
- [:reset](https://api.jquery.com/reset-selector/){data-tooltip="选择所有 type 为 reset 的元素。"}
- [:selected](https://api.jquery.com/selected-selector/){data-tooltip="选择所有被选定的元素。"}
- [:submit](https://api.jquery.com/submit-selector/){data-tooltip="选择所有 type 为 submit 的元素。"}
- [:text](https://api.jquery.com/text-selector/){data-tooltip="选择所有 type 为 text 的 input 元素。"}

{.marker-none .cols-3}

## jQuery 属性

### 示例 {.secondary .row-span-2}

```javascript
$("h2").css({
  color: "blue",
  backgroundColor: "gray",
  fontSize: "24px",
});
```

#### jQuery addClass

```javascript
$(".button").addClass("active");
```

#### jQuery removeClass

```javascript
$(".button").on("mouseleave", (evt) => {
  let e = evt.currentTarget;
  $(e).removeClass("active");
});
```

#### jQuery .toggleClass

```javascript
$(".choice").toggleClass("highlighted");
```

### 属性操作

<!-- prettier-ignore -->
- [.attr()](https://api.jquery.com/attr/){data-tooltip="获取匹配元素集合中第一个元素的属性值。"}
- [.prop()](https://api.jquery.com/prop/){data-tooltip="获取匹配元素集合中第一个元素的属性值。"}
- [.removeAttr()](https://api.jquery.com/removeAttr/){data-tooltip="从匹配元素集合中的每个元素中移除一个属性。"}
- [.removeProp()](https://api.jquery.com/removeProp/){data-tooltip="为匹配元素集合移除一个属性。"}
- [.val()](https://api.jquery.com/val/){data-tooltip="获取匹配元素集合中第一个元素的当前值。"}

{.marker-none .cols-2}

#### 数据

<!-- prettier-ignore -->
- [jQuery.data()](https://api.jquery.com/jQuery.data/){data-tooltip="存储与指定元素关联的任意数据。返回已设置的值。"}
- [.data()](https://api.jquery.com/data/){data-tooltip="存储与匹配元素关联的任意数据。"}
- [jQuery.hasData()](https://api.jquery.com/jQuery.hasData/){data-tooltip="确定元素是否有关联的 jQuery 数据。"}
- [jQuery.removeData()](https://api.jquery.com/jQuery.removeData/){data-tooltip="移除先前存储的数据片段。"}
- [.removeData()](https://api.jquery.com/removeData/){data-tooltip="移除先前存储的数据片段。"}

{.marker-none .cols-2}

### CSS 操作

<!-- prettier-ignore -->
- [.addClass()](https://api.jquery.com/addClass/){data-tooltip="向匹配元素集合中的每个元素添加指定的类。"}
- [.hasClass()](https://api.jquery.com/hasClass/){data-tooltip="确定匹配的元素中是否有任何元素被赋予了给定的类。"}
- [.removeClass()](https://api.jquery.com/removeClass/){data-tooltip="从匹配元素集合中的每个元素中移除单个类、多个类或所有类。"}
- [.toggleClass()](https://api.jquery.com/toggleClass/){data-tooltip="根据类的存在与否或 state 参数的值，从匹配元素集合中的每个元素添加或移除一个或多个类。"}
- [.css()](https://api.jquery.com/css/){data-tooltip="获取匹配元素集合中第一个元素的计算样式属性。"}
- [jQuery.cssHooks](https://api.jquery.com/jQuery.cssHooks/){data-tooltip="直接挂钩到 jQuery 以覆盖特定 CSS 属性的检索或设置方式、规范化 CSS 属性命名或创建自定义属性。"}
- [jQuery.cssNumber](https://api.jquery.com/jQuery.cssNumber/){data-tooltip="一个包含所有可以无单位使用的 CSS 属性的对象。.css() 方法使用此对象来查看是否可以向无单位值附加 px。"}
- [jQuery.escapeSelector()](https://api.jquery.com/jQuery.escapeSelector/){data-tooltip="转义 CSS 选择器中具有特殊含义的任何字符。"}

{.marker-none .cols-2}

### 尺寸

<!-- prettier-ignore -->
- [.height()](https://api.jquery.com/height/){data-tooltip="获取匹配元素集合中第一个元素的当前计算高度。"}
- [.innerHeight()](https://api.jquery.com/innerHeight/){data-tooltip="获取匹配元素集合中第一个元素的当前计算高度，包括内边距但不包括边框。"}
- [.innerWidth()](https://api.jquery.com/innerWidth/){data-tooltip="获取匹配元素集合中第一个元素的当前计算内部宽度，包括内边距但不包括边框。"}
- [.outerHeight()](https://api.jquery.com/outerHeight/){data-tooltip="获取匹配元素集合中第一个元素的当前计算外部高度（包括内边距、边框，可选地包括外边距）。"}
- [.outerWidth()](https://api.jquery.com/outerWidth/){data-tooltip="获取匹配元素集合中第一个元素的当前计算外部宽度（包括内边距、边框，可选地包括外边距）。"}
- [.width()](https://api.jquery.com/width/){data-tooltip="获取匹配元素集合中第一个元素的当前计算宽度。"}

{.marker-none .cols-2}

### 偏移

<!-- prettier-ignore -->
- [.offset()](https://api.jquery.com/offset/){data-tooltip="获取匹配元素集合中第一个元素相对于文档的当前坐标。"}
- [.offsetParent()](https://api.jquery.com/offsetParent/){data-tooltip="获取最近的已定位的祖先元素。"}
- [.position()](https://api.jquery.com/position/){data-tooltip="获取匹配元素集合中第一个元素相对于偏移父元素的当前坐标。"}
- [.scrollLeft()](https://api.jquery.com/scrollLeft/){data-tooltip="获取匹配元素集合中第一个元素的滚动条的当前水平位置。"}
- [.scrollTop()](https://api.jquery.com/scrollTop/){data-tooltip="获取匹配元素集合中第一个元素的滚动条的当前垂直位置，或为每个匹配元素设置滚动条的垂直位置。"}

{.marker-none .cols-2}

## jQuery DOM 操作

### 示例 {.secondary .row-span-3}

```javascript
/*<span>Span 元素。</span>*/
$("span").after("<p>段落。</p>");
/*<span>Span 元素。</span><p>段落。</p>*/

/*<span>Span 元素。</span>*/
$("<span>Span 元素。</span>").replaceAll("p");
/*<p>Span 元素。</p>*/

/*<span>这是一个 span 元素。</span>*/
$("span").wrap("<p></p>");
/*<p><span>这是一个 span 元素。</span></p>*/
```

### 复制

<!-- prettier-ignore -->
- [.clone()](https://api.jquery.com/clone/){data-tooltip="创建匹配元素集合的深拷贝。"}

{.marker-none .cols-3}

### DOM 插入（环绕）

<!-- prettier-ignore -->
- [.wrap()](https://api.jquery.com/wrap/){data-tooltip="在匹配元素集合中的每个元素周围包裹一个 HTML 结构。"}
- [.wrapAll()](https://api.jquery.com/wrapAll/){data-tooltip="在匹配元素集合中的所有元素周围包裹一个 HTML 结构。"}
- [.wrapInner()](https://api.jquery.com/wrapInner/){data-tooltip="在匹配元素集合中每个元素的内容周围包裹一个 HTML 结构。"}

{.marker-none .cols-3}

### DOM 插入（内部）

<!-- prettier-ignore -->
- [.append()](https://api.jquery.com/append/){data-tooltip="将参数指定的内容插入到匹配元素集合中每个元素的末尾。"}
- [.appendTo()](https://api.jquery.com/appendTo/){data-tooltip="将匹配元素集合中的每个元素插入到目标的末尾。"}
- [.html()](https://api.jquery.com/html/){data-tooltip="获取匹配元素集合中第一个元素的 HTML 内容。"}
- [.prepend()](https://api.jquery.com/prepend/){data-tooltip="将参数指定的内容插入到匹配元素集合中每个元素的开头。"}
- [.prependTo()](https://api.jquery.com/prependTo/){data-tooltip="将匹配元素集合中的每个元素插入到目标的开头。"}
- [.text()](https://api.jquery.com/text/){data-tooltip="获取匹配元素集合中每个元素（包括其后代）的组合文本内容。"}
{.marker-none .cols-3}

### DOM 插入（外部）

<!-- prettier-ignore -->
- [.after()](https://api.jquery.com/after/){data-tooltip="在匹配元素集合中的每个元素之后插入参数指定的内容。"}
- [.before()](https://api.jquery.com/before/){data-tooltip="在匹配元素集合中的每个元素之前插入参数指定的内容。"}
- [.insertAfter()](https://api.jquery.com/insertAfter/){data-tooltip="将匹配元素集合中的每个元素插入到目标之后。"}
- [.insertBefore()](https://api.jquery.com/insertBefore/){data-tooltip="将匹配元素集合中的每个元素插入到目标之前。"}

{.marker-none .cols-3}

### DOM 移除

<!-- prettier-ignore -->
- [.detach()](https://api.jquery.com/detach/){data-tooltip="从 DOM 中移除匹配的元素集合。"}
- [.empty()](https://api.jquery.com/empty/){data-tooltip="从 DOM 中移除匹配元素集合的所有子节点。"}
- [.remove()](https://api.jquery.com/remove/){data-tooltip="从 DOM 中移除匹配的元素集合。"}
- [.unwrap()](https://api.jquery.com/unwrap/){data-tooltip="从 DOM 中移除匹配元素集合的父元素，将匹配元素保留在原位。"}

{.marker-none .cols-3}

### DOM 替换

<!-- prettier-ignore -->
- [.replaceAll()](https://api.jquery.com/replaceAll/){data-tooltip="用匹配的元素集合替换每个目标元素。"}
- [.replaceWith()](https://api.jquery.com/replaceWith/){data-tooltip="用提供的新内容替换匹配元素集合中的每个元素，并返回被移除的元素集合。"}

{.marker-none .cols-3}

## jQuery 遍历

### 筛选

<!-- prettier-ignore -->
- [.eq()](https://api.jquery.com/eq/){data-tooltip="将匹配的元素集合缩减为指定索引处的元素。"}
- [.filter()](https://api.jquery.com/filter/){data-tooltip="将匹配的元素集合缩减为匹配选择器或通过函数测试的元素。"}
- [.first()](https://api.jquery.com/first/){data-tooltip="将匹配的元素集合缩减为集合中的第一个元素。"}
- [.has()](https://api.jquery.com/has/){data-tooltip="将匹配的元素集合缩减为具有匹配选择器或 DOM 元素的后代的元素。"}
- [.is()](https://api.jquery.com/is/){data-tooltip="根据选择器、元素或 jQuery 对象检查当前匹配的元素集合，如果至少有一个元素匹配给定的参数，则返回 true。"}
- [.last()](https://api.jquery.com/last/){data-tooltip="将匹配的元素集合缩减为集合中的最后一个元素。"}
- [.map()](https://api.jquery.com/map/){data-tooltip="将当前匹配集合中的每个元素传递给一个函数，生成一个包含返回值的新 jQuery 对象。"}
- [.not()](https://api.jquery.com/not/){data-tooltip="从匹配的元素集合中移除元素。"}
- [.slice()](https://api.jquery.com/slice/){data-tooltip="将匹配的元素集合缩减为由索引范围指定的子集。"}

{.marker-none .cols-3}

### 其他遍历方法

<!-- prettier-ignore -->
- [.add()](https://api.jquery.com/add/){data-tooltip="创建一个新的 jQuery 对象，其中包含添加到匹配元素集合中的元素。"}
- [.addBack()](https://api.jquery.com/addBack/){data-tooltip="将堆栈上的前一个元素集合添加到当前集合中，可选地通过选择器进行筛选。"}
- [.andSelf()](https://api.jquery.com/andSelf/){data-tooltip="将堆栈上的前一个元素集合添加到当前集合中。"}
- [.contents()](https://api.jquery.com/contents/){data-tooltip="获取匹配元素集合中每个元素的子元素，包括文本和注释节点。"}
- [.each()](https://api.jquery.com/each/){data-tooltip="遍历 jQuery 对象，为每个匹配的元素执行一个函数。"}
- [.end()](https://api.jquery.com/end/){data-tooltip="结束当前链中最近的筛选操作，并将匹配的元素集合返回到其先前的状态。"}

{.marker-none .cols-3}

### 树遍历

<!-- prettier-ignore -->
- [.children()](https://api.jquery.com/children/){data-tooltip="获取匹配元素集合中每个元素的子元素，可选地通过选择器进行筛选。"}
- [.closest()](https://api.jquery.com/closest/){data-tooltip="对于集合中的每个元素，通过测试元素本身并在 DOM 树中向上遍历其祖先来获取第一个匹配选择器的元素。"}
- [.find()](https://api.jquery.com/find/){data-tooltip="获取当前匹配元素集合中每个元素的后代，通过选择器、jQuery 对象或元素进行筛选。"}
- [.next()](https://api.jquery.com/next/){data-tooltip="获取匹配元素集合中每个元素的紧邻的下一个同级元素。如果提供了选择器，则仅当下一个同级元素匹配该选择器时才检索它。"}
- [.nextAll()](https://api.jquery.com/nextAll/){data-tooltip="获取匹配元素集合中每个元素的所有后续同级元素，可选地通过选择器进行筛选。"}
- [.nextUntil()](https://api.jquery.com/nextUntil/){data-tooltip="获取每个元素的所有后续同级元素，直到但不包括与传递的选择器、DOM 节点或 jQuery 对象匹配的元素。"}
- [.parent()](https://api.jquery.com/parent/){data-tooltip="获取当前匹配元素集合中每个元素的父元素，可选地通过选择器进行筛选。"}
- [.parents()](https://api.jquery.com/parents/){data-tooltip="获取当前匹配元素集合中每个元素的祖先元素，可选地通过选择器进行筛选。"}
- [.parentsUntil()](https://api.jquery.com/parentsUntil/){data-tooltip="获取当前匹配元素集合中每个元素的祖先元素，直到但不包括与选择器、DOM 节点或 jQuery 对象匹配的元素。"}
- [.prev()](https://api.jquery.com/prev/){data-tooltip="获取匹配元素集合中每个元素的紧邻的上一个同级元素。如果提供了选择器，则仅当上一个同级元素匹配该选择器时才检索它。"}
- [.prevAll()](https://api.jquery.com/prevAll/){data-tooltip="获取匹配元素集合中每个元素的所有先前同级元素，可选地通过选择器进行筛选。"}
- [.prevUntil()](https://api.jquery.com/prevUntil/){data-tooltip="获取每个元素的所有先前同级元素，直到但不包括与传递的选择器、DOM 节点或 jQuery 对象匹配的元素。"}
- [.siblings()](https://api.jquery.com/siblings/){data-tooltip="获取匹配元素集合中每个元素的同级元素，可选地通过选择器进行筛选。"}

{.marker-none .cols-3}

## jQuery 事件

### 示例 {.secondary .row-span-6}

```javascript
// 鼠标事件 'click'
$("#menu-button").on("click", () => {
  $("#menu").show();
});

// 键盘事件 'keyup'
$("#textbox").on("keyup", () => {
  $("#menu").show();
});

// 滚动事件 'scroll'
$("#menu-button").on("scroll", () => {
  $("#menu").show();
});
```

#### 事件对象

```javascript
$("#menu").on("click", (event) => {
  $(event.currentTarget).hide();
});
```

#### 方法链

```javascript
$("#menu-btn")
  .on("mouseenter", () => {
    $("#menu").show();
  })
  .on("mouseleave", () => {
    $("#menu").hide();
  });
```

#### 阻止事件

```javascript
$("p").click(function (event) {
  event.stopPropagation();
  // 执行某些操作
});
```

### 浏览器事件

<!-- prettier-ignore -->
- [.error()](https://api.jquery.com/error/){data-tooltip="将事件处理程序绑定到 error JavaScript 事件。"}
- [.resize()](https://api.jquery.com/resize/){data-tooltip="将事件处理程序绑定到 resize JavaScript 事件，或在元素上触发该事件。"}
- [.scroll()](https://api.jquery.com/scroll/){data-tooltip="将事件处理程序绑定到 scroll JavaScript 事件，或在元素上触发该事件。"}

{.marker-none .cols-3}

### 事件对象 {.row-span-6}

<!-- prettier-ignore -->
- [event.currentTarget](https://api.jquery.com/event.currentTarget/){data-tooltip="事件冒泡阶段中的当前 DOM 元素。"}
- [event.delegateTarget](https://api.jquery.com/event.delegateTarget/){data-tooltip="当前调用的 jQuery 事件处理程序附加到的元素。"}
- [event.data](https://api.jquery.com/event.data/){data-tooltip="当当前执行的处理程序被绑定时，传递给事件方法的可选数据对象。"}
- [event.isDefaultPrevented()](https://api.jquery.com/event.isDefaultPrevented/){data-tooltip="返回是否曾在此事件对象上调用过 event.preventDefault()。"}
- [event.isImmediatePropagationStopped()](https://api.jquery.com/event.isImmediatePropagationStopped/){data-tooltip="返回是否曾在此事件对象上调用过 event.stopImmediatePropagation()。"}
- [event.isPropagationStopped()](https://api.jquery.com/event.isPropagationStopped/){data-tooltip="返回是否曾在此事件对象上调用过 event.stopPropagation()。"}
- [event.metaKey](https://api.jquery.com/event.metaKey/){data-tooltip="指示事件触发时 META 键是否被按下。"}
- [event.namespace](https://api.jquery.com/event.namespace/){data-tooltip="事件触发时指定的命名空间。"}
- [event.pageX](https://api.jquery.com/event.pageX/){data-tooltip="鼠标相对于文档左边缘的位置。"}
- [event.pageY](https://api.jquery.com/event.pageY/){data-tooltip="鼠标相对于文档上边缘的位置。"}
- [event.preventDefault()](https://api.jquery.com/event.preventDefault/){data-tooltip="如果调用此方法，则不会触发事件的默认操作。"}
- [event.relatedTarget](https://api.jquery.com/event.relatedTarget/){data-tooltip="事件中涉及的另一个 DOM 元素（如果有）。"}
- [event.result](https://api.jquery.com/event.result/){data-tooltip="由此事件触发的事件处理程序返回的最后一个值，除非该值为 undefined。"}
- [event.stopImmediatePropagation()](https://api.jquery.com/event.stopImmediatePropagation/){data-tooltip="阻止其余处理程序的执行，并阻止事件在 DOM 树中冒泡。"}
- [event.stopPropagation()](https://api.jquery.com/event.stopPropagation/){data-tooltip="阻止事件在 DOM 树中冒泡，从而阻止任何父处理程序被通知该事件。"}
- [event.target](https://api.jquery.com/event.target/){data-tooltip="发起事件的 DOM 元素。"}
- [event.timeStamp](https://api.jquery.com/event.timeStamp/){data-tooltip="浏览器创建事件的时间与 1970 年 1 月 1 日之间的毫秒差。"}
- [event.type](https://api.jquery.com/event.type/){data-tooltip="描述事件的性质。"}
- [event.which](https://api.jquery.com/event.which/){data-tooltip="对于键盘或鼠标事件，此属性指示按下的特定键或按钮。"}

{.marker-none .cols-1}

### 文档加载

<!-- prettier-ignore -->
- [.load()](https://api.jquery.com/load-event/){data-tooltip="将事件处理程序绑定到 load JavaScript 事件。"}
- [.ready()](https://api.jquery.com/ready/){data-tooltip="指定 DOM 完全加载后要执行的函数。"}
- [.unload()](https://api.jquery.com/unload/){data-tooltip="将事件处理程序绑定到 unload JavaScript 事件。"}

{.marker-none .cols-3}

### 事件处理程序附加

<!-- prettier-ignore -->
- [.bind()](https://api.jquery.com/bind/){data-tooltip="为元素附加事件处理程序。"}
- [.delegate()](https://api.jquery.com/delegate/){data-tooltip="基于一组特定的根元素，为所有现在或将来匹配选择器的元素附加一个或多个事件的处理程序。"}
- [.die()](https://api.jquery.com/die/){data-tooltip="从元素中移除先前使用 .live() 附加的事件处理程序。"}
- [.live()](https://api.jquery.com/live/){data-tooltip="为所有现在和将来匹配当前选择器的元素附加事件处理程序。"}
- [.off()](https://api.jquery.com/off/){data-tooltip="移除事件处理程序。"}
- [.on()](https://api.jquery.com/on/){data-tooltip="为选定元素附加一个或多个事件的事件处理函数。"}
- [.one()](https://api.jquery.com/one/){data-tooltip="为元素附加事件处理程序。每个元素每种事件类型最多执行一次处理程序。"}
- [.trigger()](https://api.jquery.com/trigger/){data-tooltip="为给定事件类型执行附加到匹配元素的所有处理程序和行为。"}
- [.triggerHandler()](https://api.jquery.com/triggerHandler/){data-tooltip="执行附加到元素上的事件的所有处理程序。"}
- [.unbind()](https://api.jquery.com/unbind/){data-tooltip="从元素中移除先前附加的事件处理程序。"}
- [.undelegate()](https://api.jquery.com/undelegate/){data-tooltip="基于一组特定的根元素，从所有匹配当前选择器的元素的事件中移除处理程序。"}

{.marker-none .cols-3}

### 表单事件

<!-- prettier-ignore -->
- [.blur()](https://api.jquery.com/blur/){data-tooltip="将事件处理程序绑定到 blur JavaScript 事件，或在元素上触发该事件。"}
- [.change()](https://api.jquery.com/change/){data-tooltip="将事件处理程序绑定到 change JavaScript 事件，或在元素上触发该事件。"}
- [.focus()](https://api.jquery.com/focus/){data-tooltip="将事件处理程序绑定到 focus JavaScript 事件，或在元素上触发该事件。"}
- [.focusin()](https://api.jquery.com/focusin/){data-tooltip="将事件处理程序绑定到 focusin 事件。"}
- [.focusout()](https://api.jquery.com/focusout/){data-tooltip="将事件处理程序绑定到 focusout JavaScript 事件。"}
- [.select()](https://api.jquery.com/select/){data-tooltip="将事件处理程序绑定到 select JavaScript 事件，或在元素上触发该事件。"}
- [.submit()](https://api.jquery.com/submit/){data-tooltip="将事件处理程序绑定到 submit JavaScript 事件，或在元素上触发该事件。"}

{.marker-none .cols-3}

### 键盘事件

<!-- prettier-ignore -->
- [.keydown()](https://api.jquery.com/keydown/){data-tooltip="将事件处理程序绑定到 keydown JavaScript 事件，或在元素上触发该事件。"}
- [.keypress()](https://api.jquery.com/keypress/){data-tooltip="将事件处理程序绑定到 keypress JavaScript 事件，或在元素上触发该事件。"}
- [.keyup()](https://api.jquery.com/keyup/){data-tooltip="将事件处理程序绑定到 keyup JavaScript 事件，或在元素上触发该事件。"}
{.marker-none .cols-3}

### 鼠标事件

<!-- prettier-ignore -->
- [.click()](https://api.jquery.com/click/){data-tooltip="将事件处理程序绑定到 click JavaScript 事件，或在元素上触发该事件。"}
- [.contextMenu()](https://api.jquery.com/contextmenu/){data-tooltip="将事件处理程序绑定到 contextmenu JavaScript 事件，或在元素上触发该事件。"}
- [.dblclick()](https://api.jquery.com/dblclick/){data-tooltip="将事件处理程序绑定到 dblclick JavaScript 事件，或在元素上触发该事件。"}
- [.hover()](https://api.jquery.com/hover/){data-tooltip="为匹配的元素绑定两个处理程序，分别在鼠标指针进入和离开元素时执行。"}
- [.mousedown()](https://api.jquery.com/mousedown/){data-tooltip="将事件处理程序绑定到 mousedown JavaScript 事件，或在元素上触发该事件。"}
- [.mouseenter()](https://api.jquery.com/mouseenter/){data-tooltip="绑定一个事件处理程序，在鼠标进入元素时触发，或在元素上触发该处理程序。"}
- [.mouseleave()](https://api.jquery.com/mouseleave/){data-tooltip="绑定一个事件处理程序，在鼠标离开元素时触发，或在元素上触发该处理程序。"}
- [.mousemove()](https://api.jquery.com/mousemove/){data-tooltip="将事件处理程序绑定到 mousemove JavaScript 事件，或在元素上触发该事件。"}
- [.mouseout()](https://api.jquery.com/mouseout/){data-tooltip="将事件处理程序绑定到 mouseout JavaScript 事件，或在元素上触发该事件。"}
- [.mouseover()](https://api.jquery.com/mouseover/){data-tooltip="将事件处理程序绑定到 mouseover JavaScript 事件，或在元素上触发该事件。"}
- [.mouseup()](https://api.jquery.com/mouseup/){data-tooltip="将事件处理程序绑定到 mouseup JavaScript 事件，或在元素上触发该事件。"}
- [.toggle()](https://api.jquery.com/toggle-event/){data-tooltip="为匹配的元素绑定两个或多个处理程序，在交替点击时执行。"}

{.marker-none .cols-3}

## jQuery 效果

### 示例 {.secondary .row-span-2}

```javascript
$("#menu-button").on("click", () => {
  // $('#menu').fadeIn(400, 'swing')
  $("#menu").fadeIn();
});
```

#### fadeOut 效果

```javascript
$("#menu-button").on("click", () => {
  // $('#menu').fadeOut(400, 'swing')
  $("#menu").fadeOut();
});
```

### 基本效果

<!-- prettier-ignore -->
- [.hide()](https://api.jquery.com/hide/){data-tooltip="隐藏匹配的元素。"}
- [.show()](https://api.jquery.com/show/){data-tooltip="显示匹配的元素。"}
- [.toggle()](https://api.jquery.com/toggle/){data-tooltip="显示或隐藏匹配的元素。"}

{.marker-none .cols-3}

### 滑动效果

<!-- prettier-ignore -->
- [.slideDown()](https://api.jquery.com/slideDown/){data-tooltip="以滑动方式显示匹配的元素。"}
- [.slideToggle()](https://api.jquery.com/slideToggle/){data-tooltip="以滑动方式显示或隐藏匹配的元素。"}
- [.slideUp()](https://api.jquery.com/slideUp/){data-tooltip="以滑动方式隐藏匹配的元素。"}

{.marker-none .cols-3}

### 自定义效果

<!-- prettier-ignore -->
- [.animate()](https://api.jquery.com/animate/){data-tooltip="执行一组 CSS 属性的自定义动画。"}
- [.clearQueue()](https://api.jquery.com/clearQueue/){data-tooltip="从队列中移除所有尚未运行的项目。"}
- [.delay()](https://api.jquery.com/delay/){data-tooltip="设置一个计时器以延迟队列中后续项目的执行。"}
- [.dequeue()](https://api.jquery.com/dequeue/){data-tooltip="为匹配的元素执行队列中的下一个函数。"}
- [jQuery.dequeue()](https://api.jquery.com/jQuery.dequeue/){data-tooltip="为匹配的元素执行队列中的下一个函数。"}
- [.finish()](https://api.jquery.com/finish/){data-tooltip="停止当前正在运行的动画，移除所有排队的动画，并完成匹配元素的所有动画。"}
- [jQuery.fx.interval](https://api.jquery.com/jQuery.fx.interval/){data-tooltip="动画触发的速率（以毫秒为单位）。"}
- [jQuery.fx.off](https://api.jquery.com/jQuery.fx.off/){data-tooltip="全局禁用所有动画。"}
- [jQuery.speed](https://api.jquery.com/jQuery.speed/){data-tooltip="创建一个包含一组属性的对象，这些属性可用于自定义动画的定义。"}
- [.queue()](https://api.jquery.com/queue/){data-tooltip="显示将在匹配元素上执行的函数队列。"}
- [jQuery.queue()](https://api.jquery.com/jQuery.queue/){data-tooltip="显示将在匹配元素上执行的函数队列。"}
- [.stop()](https://api.jquery.com/stop/){data-tooltip="停止匹配元素上当前正在运行的动画。"}

{.marker-none .cols-3}

### 淡入淡出效果

<!-- prettier-ignore -->
- [.fadeIn()](https://api.jquery.com/fadeIn/){data-tooltip="通过将匹配元素淡化到不透明来显示它们。"}
- [.fadeOut()](https://api.jquery.com/fadeOut/){data-tooltip="通过将匹配元素淡化到透明来隐藏它们。"}
- [.fadeTo()](https://api.jquery.com/fadeTo/){data-tooltip="调整匹配元素的不透明度。"}
- [.fadeToggle()](https://api.jquery.com/fadeToggle/){data-tooltip="通过动画化其不透明度来显示或隐藏匹配的元素。"}

{.marker-none .cols-3}

## jQuery Ajax

### 示例 {.secondary .row-span-2}

```javascript
$.ajax({
  url: this.action,
  type: this.method,
  data: $(this).serialize(),
})
  .done(function (server_data) {
    console.log("成功" + server_data);
  })
  .fail(function (jqXHR, status, err) {
    console.log("失败" + err);
  });
```

### 全局 Ajax 事件处理程序

<!-- prettier-ignore -->
- [.ajaxComplete()](https://api.jquery.com/ajaxComplete/){data-tooltip="注册一个在 Ajax 请求完成时调用的处理程序。这是一个 AjaxEvent。"}
- [.ajaxError()](https://api.jquery.com/ajaxError/){data-tooltip="注册一个在 Ajax 请求完成并出现错误时调用的处理程序。这是一个 Ajax 事件。"}
- [.ajaxSend()](https://api.jquery.com/ajaxSend/){data-tooltip="附加一个在发送 Ajax 请求之前执行的函数。这是一个 Ajax 事件。"}
- [.ajaxStart()](https://api.jquery.com/ajaxStart/){data-tooltip="注册一个在第一个 Ajax 请求开始时调用的处理程序。这是一个 Ajax 事件。"}
- [.ajaxStop()](https://api.jquery.com/ajaxStop/){data-tooltip="注册一个在所有 Ajax 请求都已完成时调用的处理程序。这是一个 Ajax 事件。"}
- [.ajaxSuccess()](https://api.jquery.com/ajaxSuccess/){data-tooltip="附加一个在 Ajax 请求成功完成时执行的函数。这是一个 Ajax 事件。"}

{.marker-none .cols-2}

### 辅助函数

<!-- prettier-ignore -->
- [jQuery.param()](https://api.jquery.com/jQuery.param/){data-tooltip="创建一个数组、普通对象或 jQuery 对象的序列化表示，适用于 URL 查询字符串或 Ajax 请求。如果传递的是 jQuery 对象，它应包含具有 name/value 属性的输入元素。"}
- [.serialize()](https://api.jquery.com/serialize/){data-tooltip="将一组表单元素编码为用于提交的字符串。"}
- [.serializeArray()](https://api.jquery.com/serializeArray/){data-tooltip="将一组表单元素编码为名称和值的数组。"}

{.marker-none .cols-2}

### 底层接口

<!-- prettier-ignore -->
- [jQuery.ajax()](https://api.jquery.com/jQuery.ajax/){data-tooltip="执行异步 HTTP (Ajax) 请求。"}
- [jQuery.prefilter()](https://api.jquery.com/jQuery.ajaxPrefilter/){data-tooltip="在每个请求发送之前以及在 $.ajax() 处理它们之前，处理自定义 Ajax 选项或修改现有选项。"}
- [jQuery.ajaxSetup()](https://api.jquery.com/jQuery.ajaxSetup/){data-tooltip="为将来的 Ajax 请求设置默认值。不建议使用。"}
- [jQuery.ajaxTransport()](https://api.jquery.com/jQuery.ajaxTransport/){data-tooltip="创建一个处理 Ajax 数据实际传输的对象。"}

{.marker-none .cols-2}

### 简写方法

<!-- prettier-ignore -->
- [jQuery.get()](https://api.jquery.com/jQuery.get/){data-tooltip="使用 HTTP GET 请求从服务器加载数据。"}
- [jQuery.getJSON()](https://api.jquery.com/jQuery.getJSON/){data-tooltip="使用 GET HTTP 请求从服务器加载 JSON 编码的数据。"}
- [jQuery.getScript()](https://api.jquery.com/jQuery.getScript/){data-tooltip="使用 GET HTTP 请求从服务器加载 JavaScript 文件，然后执行它。"}
- [jQuery.post()](https://api.jquery.com/jQuery.post/){data-tooltip="使用 HTTP POST 请求向服务器发送数据。"}
- [.load()](https://api.jquery.com/load/){data-tooltip="从服务器加载数据并将返回的 HTML 放入匹配的元素中。"}

{.marker-none .cols-2}

## 其他

### jQuery 对象

<!-- prettier-ignore -->
- [jQuery()](https://api.jquery.com/jQuery/){data-tooltip="接受包含 CSS 选择器的字符串，然后用于匹配一组元素。"}
- [jQuery.noConflict()](https://api.jquery.com/jQuery.noConflict/){data-tooltip="放弃 jQuery 对 $ 变量的控制。"}
- [jQuery.sub()](https://api.jquery.com/jQuery.sub/){data-tooltip="创建一个 jQuery 的新副本，其属性和方法可以修改而不影响原始 jQuery 对象。"}
- [jQuery.holdReady()](https://api.jquery.com/jQuery.holdReady/){data-tooltip="暂停或释放 jQuery 的 ready 事件的执行。"}
- [jQuery.when()](https://api.jquery.com/jQuery.when/){data-tooltip="提供一种基于零个或多个 Thenable 对象（通常是表示异步事件的 Deferred 对象）执行回调函数的方法。"}

{.marker-none .cols-2}

### Deferred 对象 {.row-span-2}

<!-- prettier-ignore -->
- [jQuery.Deferred()](https://api.jquery.com/jQuery.Deferred/){data-tooltip="一个工厂函数，返回一个可链接的实用程序对象，该对象具有将多个回调注册到回调队列、调用回调队列以及中继任何同步或异步函数的成功或失败状态的方法。"}
- [deferred.always()](https://api.jquery.com/deferred.always/){data-tooltip="添加在 Deferred 对象被解决或拒绝时调用的处理程序。"}
- [deferred.done()](https://api.jquery.com/deferred.done/){data-tooltip="添加在 Deferred 对象被解决时调用的处理程序。"}
- [deferred.fail()](https://api.jquery.com/deferred.fail/){data-tooltip="添加在 Deferred 对象被拒绝时调用的处理程序。"}
- [deferred.isRejected()](https://api.jquery.com/deferred.isRejected/){data-tooltip="确定 Deferred 对象是否已被拒绝。"}
- [deferred.isResolved()](https://api.jquery.com/deferred.isResolved/){data-tooltip="确定 Deferred 对象是否已被解决。"}
- [deferred.notify()](https://api.jquery.com/deferred.notify/){data-tooltip="使用给定的参数调用 Deferred 对象上的 progressCallbacks。"}
- [deferred.notifyWith()](https://api.jquery.com/deferred.notifyWith/){data-tooltip="使用给定的上下文和参数调用 Deferred 对象上的 progressCallbacks。"}
- [deferred.pipe()](https://api.jquery.com/deferred.pipe/){data-tooltip="用于筛选和/或链接 Deferred 对象的实用方法。"}
- [deferred.progress()](https://api.jquery.com/deferred.progress/){data-tooltip="添加在 Deferred 对象生成进度通知时调用的处理程序。"}
- [deferred.promise()](https://api.jquery.com/deferred.promise/){data-tooltip="返回 Deferred 对象的 Promise 对象。"}
- [deferred.reject()](https://api.jquery.com/deferred.reject/){data-tooltip="拒绝 Deferred 对象并使用给定的参数调用任何 failCallbacks。"}
- [deferred.rejectWith()](https://api.jquery.com/deferred.rejectWith/){data-tooltip="拒绝 Deferred 对象并使用给定的上下文和参数调用任何 failCallbacks。"}
- [deferred.resolve()](https://api.jquery.com/deferred.resolve/){data-tooltip="解决 Deferred 对象并使用给定的参数调用任何 doneCallbacks。"}
- [deferred.resolveWith()](https://api.jquery.com/deferred.resolveWith/){data-tooltip="解决 Deferred 对象并使用给定的上下文和参数调用任何 doneCallbacks。"}
- [deferred.state()](https://api.jquery.com/deferred.state/){data-tooltip="确定 Deferred 对象的当前状态。"}
- [deferred.then()](https://api.jquery.com/deferred.then/){data-tooltip="添加在 Deferred 对象被解决、拒绝或仍在进行中时调用的处理程序。"}
- [.promise()](https://api.jquery.com/promise/){data-tooltip="返回一个 Promise 对象，用于观察绑定到集合的某种类型的所有操作（无论是否排队）何时完成。"}

{.marker-none .cols-2}

### 实用工具 {.row-span-3}

<!-- prettier-ignore -->
- [jQuery.boxModel](https://api.jquery.com/jQuery.boxModel/){data-tooltip="说明当前页面在用户浏览器中是否使用 W3C CSS 盒模型进行渲染。"}
- [jQuery.browser](https://api.jquery.com/jQuery.browser/){data-tooltip="包含从 navigator.userAgent 读取的用户代理标志。此属性在 jQuery 1.9 中已移除，仅通过 jQuery.migrate 插件可用。请尝试使用特性检测代替。"}
- [jQuery.contains()](https://api.jquery.com/jQuery.contains/){data-tooltip="检查一个 DOM 元素是否是另一个 DOM 元素的后代。"}
- [jQuery.each()](https://api.jquery.com/jQuery.each/){data-tooltip="一个通用的迭代器函数，可用于无缝迭代对象和数组。具有 length 属性的数组和类数组对象（例如函数的 arguments 对象）按数字索引从 0 到 length-1 进行迭代。其他对象通过其命名属性进行迭代。"}
- [jQuery.extend()](https://api.jquery.com/jQuery.extend/){data-tooltip="将两个或多个对象的内容合并到第一个对象中。"}
- [jQuery.globalEval()](https://api.jquery.com/jQuery.globalEval/){data-tooltip="全局执行一些 JavaScript 代码。"}
- [jQuery.grep()](https://api.jquery.com/jQuery.grep/){data-tooltip="查找满足筛选函数的数组元素。原始数组不受影响。"}
- [jQuery.inArray()](https://api.jquery.com/jQuery.inArray/){data-tooltip="在数组中搜索指定值并返回其索引（如果未找到则返回 -1）。"}
- [jQuery.isArray()](https://api.jquery.com/jQuery.isArray/){data-tooltip="确定参数是否为数组。"}
- [jQuery.isEmptyObject()](https://api.jquery.com/jQuery.isEmptyObject/){data-tooltip="检查对象是否为空（不包含可枚举属性）。"}
- [jQuery.isFunction()](https://api.jquery.com/jQuery.isFunction/){data-tooltip="确定其参数是否可作为函数调用。"}
- [jQuery.isNumeric()](https://api.jquery.com/jQuery.isNumeric/){data-tooltip="确定其参数是否表示 JavaScript 数字。"}
- [jQuery.isPlainObject()](https://api.jquery.com/jQuery.isPlainObject/){data-tooltip="检查对象是否为普通对象。"}
- [jQuery.isWindow()](https://api.jquery.com/jQuery.isWindow/){data-tooltip="确定参数是否为窗口。"}
- [jQuery.isXMLDoc()](https://api.jquery.com/jQuery.isXMLDoc/){data-tooltip="检查 DOM 节点是否在 XML 文档中（或者是 XML 文档）。"}
- [jQuery.makeArray()](https://api.jquery.com/jQuery.makeArray/){data-tooltip="将类数组对象转换为真正的 JavaScript 数组。"}
- [jQuery.map()](https://api.jquery.com/jQuery.map/){data-tooltip="将数组或对象中的所有项目转换为新的项目数组。"}
- [jQuery.merge()](https://api.jquery.com/jQuery.merge/){data-tooltip="将两个数组的内容合并到第一个数组中。"}
- [jQuery.noop()](https://api.jquery.com/jQuery.noop/){data-tooltip="一个空函数。"}
- [jQuery.now()](https://api.jquery.com/jQuery.now/){data-tooltip="返回表示当前时间的数字。"}
- [jQuery.parseHTML()](https://api.jquery.com/jQuery.parseHTML/){data-tooltip="将字符串解析为 DOM 节点数组。"}
- [jQuery.parseJSON()](https://api.jquery.com/jQuery.parseJSON/){data-tooltip="接受格式良好的 JSON 字符串并返回结果 JavaScript 值。"}
- [jQuery.parseXML()](https://api.jquery.com/jQuery.parseXML/){data-tooltip="将字符串解析为 XML 文档。"}
- [jQuery.proxy()](https://api.jquery.com/jQuery.proxy/){data-tooltip="接受一个函数并返回一个始终具有特定上下文的新函数。"}
- [jQuery.support](https://api.jquery.com/jQuery.support/){data-tooltip="表示不同浏览器特性或错误的属性集合。供 jQuery 内部使用；当内部不再需要某些特定属性时，可能会将其删除以提高页面启动性能。对于您自己项目的特性检测需求，我们强烈建议使用诸如 Modernizr 之类的外部库，而不是依赖 jQuery.support 中的属性。"}
- [jQuery.trim()](https://api.jquery.com/jQuery.trim/){data-tooltip="移除字符串开头和结尾的空白字符。"}
- [jQuery.type()](https://api.jquery.com/jQuery.type/){data-tooltip="确定对象的内部 JavaScript [[Class]]。"}
- [jQuery.unique()](https://api.jquery.com/jQuery.unique/){data-tooltip="对 DOM 元素数组进行原地排序，并移除重复项。请注意，这仅适用于 DOM 元素数组，不适用于字符串或数字。"}
- [jQuery.uniqueSort()](https://api.jquery.com/jQuery.uniqueSort/){data-tooltip="对 DOM 元素数组进行原地排序，并移除重复项。请注意，这仅适用于 DOM 元素数组，不适用于字符串或数字。"}

{.marker-none .cols-2}

### DOM 元素方法

<!-- prettier-ignore -->
- [.get()](https://api.jquery.com/get/){data-tooltip="检索 jQuery 对象匹配的元素之一。"}
- [.index()](https://api.jquery.com/index/){data-tooltip="从匹配的元素中搜索给定元素。"}
- [.size()](https://api.jquery.com/size/){data-tooltip="返回 jQuery 对象中元素的数量。"}
- [.toArray()](https://api.jquery.com/toArray/){data-tooltip="以数组形式检索 jQuery 集合中包含的所有元素。"}

{.marker-none .cols-2}

### 内部构件

<!-- prettier-ignore -->
- [.jquery](https://api.jquery.com/jquery-2/){data-tooltip="包含 jQuery 版本号的字符串。"}
- [.context](https://api.jquery.com/context/){data-tooltip="最初传递给 jQuery() 的 DOM 节点上下文；如果未传递，则上下文很可能是文档。"}
- [jQuery.error()](https://api.jquery.com/jQuery.error/){data-tooltip="接受一个字符串并抛出包含该字符串的异常。"}
- [.length](https://api.jquery.com/length/){data-tooltip="jQuery 对象中元素的数量。"}
- [.pushStack()](https://api.jquery.com/pushStack/){data-tooltip="将 DOM 元素集合添加到 jQuery 堆栈中。"}
- [.selector](https://api.jquery.com/selector/){data-tooltip="表示在创建原始集合时传递给 jQuery() 的选择器（如果有）。"}

{.marker-none .cols-2}

### Callbacks 对象

<!-- prettier-ignore -->
- [jQuery.Callbacks()](https://api.jquery.com/jQuery.Callbacks/){data-tooltip="一个多用途回调列表对象，提供了一种管理回调列表的强大方法。"}
- [callbacks.add()](https://api.jquery.com/callbacks.add/){data-tooltip="向回调列表添加一个回调或一组回调。"}
- [callbacks.disable()](https://api.jquery.com/callbacks.disable/){data-tooltip="禁用回调列表，使其不再执行任何操作。"}
- [callbacks.disabled()](https://api.jquery.com/callbacks.disabled/){data-tooltip="确定回调列表是否已被禁用。"}
- [callbacks.empty()](https://api.jquery.com/callbacks.empty/){data-tooltip="从列表中移除所有回调。"}
- [callbacks.fire()](https://api.jquery.com/callbacks.fire/){data-tooltip="使用给定的参数调用所有回调。"}
- [callbacks.fired()](https://api.jquery.com/callbacks.fired/){data-tooltip="确定回调是否至少已被调用过一次。"}
- [callbacks.fireWith()](https://api.jquery.com/callbacks.fireWith/){data-tooltip="使用给定的上下文和参数调用列表中的所有回调。"}
- [callbacks.has()](https://api.jquery.com/callbacks.has/){data-tooltip="确定列表是否附加了任何回调。如果提供了回调作为参数，则确定它是否在列表中。"}
- [callbacks.lock()](https://api.jquery.com/callbacks.lock/){data-tooltip="将回调列表锁定在其当前状态。"}
- [callbacks.locked()](https://api.jquery.com/callbacks.locked/){data-tooltip="确定回调列表是否已被锁定。"}
- [callbacks.remove()](https://api.jquery.com/callbacks.remove/){data-tooltip="从回调列表中移除一个回调或一组回调。"}

{.marker-none .cols-2}

