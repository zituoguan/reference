---
title: ES6
date: 2023-01-08 18:26:55
background: bg-[#edc545]
tags:
  - config
  - format
categories:
  - 编程
intro: |
  一份关于 ES2015、ES2016、ES2017、ES2018 及更高版本中 JavaScript 新增功能的快速参考备忘单
plugins:
  - copyCode
  - runCode
---

## 入门

### 块级作用域 {.row-span-2}

#### Let

```js{2,4}
function fn () {
  let x = 0
  if (true) {
    let x = 1 // 只在这个 `if` 内部有效
  }
}
```

#### Const

```js
const a = 1;
```

`let` 是新的 `var`。常量 (`const`) 的工作方式与 `let` 类似，但不能被重新赋值。参见：
[Let 和 const](https://babeljs.io/learn-es2015/#let--const)

### 模板字符串 {.row-span-2}

#### 插值

```js
const message = `Hello ${name}`;
```

#### 多行字符串

```js
const str = `
hello
the world
`;
```

模板和多行字符串。参见：[模板字符串](https://babeljs.io/learn-es2015/#template-strings)

### 二进制和八进制字面量

```js
let bin = 0b1010010;
let oct = 0o755;
```

参见：[二进制和八进制字面量](https://babeljs.io/learn-es2015/#binary-and-octal-literals)

### 指数运算符

```js {1}
const byte = 2 ** 8;
```

等同于：Math.pow(2, 8)

### 新增库

#### 新的字符串方法

```js
"hello".repeat(3);
"hello".includes("ll");
"hello".startsWith("he");
"hello".padStart(8); // "hello"
"hello".padEnd(8); // "hello"
"hello".padEnd(8, "!"); // hello!!!
"\u1E9B\u0323".normalize("NFC");
```

#### 新的 Number 方法

```js
Number.EPSILON;
Number.isInteger(Infinity); // false
Number.isNaN("NaN"); // false
```

#### 新的 Math 方法

```js
Math.acosh(3); // 1.762747174039086
Math.hypot(3, 4); // 5
Math.imul(Math.pow(2, 32) - 1, Math.pow(2, 32) - 2); // 2
```

#### 新的 Array 方法

```js
//返回一个真正的数组
Array.from(document.querySelectorAll("*"));
//类似于 new Array(...)，但没有特殊的单参数行为
Array.of(1, 2, 3);
```

参见：[新增库](https://babeljs.io/learn-es2015/#math--number--string--object-apis)

### 类

```js
class Circle extends Shape {
```

#### 构造函数

```js {1}
constructor (radius) {
  this.radius = radius
}
```

#### 方法

```js {1}
getArea () {
  return Math.PI *2 *this.radius
}
```

#### 调用超类方法

```js {2}
expand(n) {
  return super.expand(n) *Math.PI
}
```

#### 静态方法

```js {1}
static createFromDiameter(diameter) {
  return new Circle(diameter /2)
}
```

原型的语法糖。参见：[类](https://babeljs.io/learn-es2015/#classes)

### 私有类

JavaScript 默认字段是公共的 (`public`)，如果需要表示私有，可以使用 (`#`)

```js
class Dog {
  #name;
  constructor(name) {
    this.#name = name;
  }
  printName() {
    // 只有私有字段可以在类内部调用
    console.log(`Your name is ${this.#name}`);
  }
}

const dog = new Dog("putty");
//console.log(this.#name)
//私有标识符不允许在类主体之外使用。
dog.printName();
```

#### 静态私有类

```js
class ClassWithPrivate {
  static #privateStaticField;
  static #privateStaticFieldWithInitializer = 42;

  static #privateStaticMethod() {
    // …
  }
}
```

## Promises

### 创建 Promise

```js {1}
new Promise((resolve, reject) => {
  if (ok) {
    resolve(result);
  } else {
    reject(error);
  }
});
```

用于异步编程。参见：[Promises](https://babeljs.io/learn-es2015/#promises)

### 使用 Promises

```js{2,3}
promise
  .then((result) => { ··· })
  .catch((error) => { ··· })
```

### 在 finally 中使用 Promises

```js {4}
promise
  .then((result) => { ··· })
  .catch((error) => { ··· })
  .finally(() => {
    /* 独立于成功/错误逻辑 */
  })
```

当 promise 被 fulfilled 或 rejected 时，处理程序会被调用

### Promise 函数

```js
Promise.all(···)
Promise.race(···)
Promise.reject(···)
Promise.resolve(···)
```

### Async-await

```js{2,3}
async function run () {
  const user = await getUser()
  const tweets = await getTweets(user)
  return [user, tweets]
}
```

`async` 函数是使用函数的另一种方式。参见：
[Async 函数](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/async_function)

## 解构

### 解构赋值

#### 数组

```js {1}
const [first, last] = ["Nikola", "Tesla"];
```

#### 对象

```js {1}
let { title, author } = {
  title: "The Silkworm",
  author: "R. Galbraith",
};
```

支持匹配数组和对象。参见：[解构](https://babeljs.io/learn-es2015/#destructuring)

### 默认值

```js
const scores = [22, 33];
const [math = 50, sci = 50, arts = 50] = scores;
```

---

```js
//结果:
//math === 22, sci === 33, arts === 50
```

解构数组或对象时可以分配默认值

### 函数参数

```js {1}
function greet({ name, greeting }) {
  console.log(`${greeting}, ${name}!`);
}
```

---

```js
greet({ name: "Larry", greeting: "Ahoy" });
```

对象和数组的解构也可以在函数参数中完成

### 默认值

```js {1}
function greet({ name = "Rauno" } = {}) {
  console.log(`Hi ${name}!`);
}
```

---

```js
greet(); // Hi Rauno!
greet({ name: "Larry" }); // Hi Larry!
```

### 重命名键

```js {1}
function printCoordinates({ left: x, top: y }) {
  console.log(`x: ${x}, y: ${y}`);
}
```

---

```js
printCoordinates({ left: 25, top: 90 });
```

此示例将 `x` 赋值为 `left` 键的值

### 循环

```js {1}
for (let {title, artist} of songs) {
  ···
}
```

赋值表达式也适用于循环

### 对象解构

```js {1}
const { id, ...detail } = song;
```

使用 `rest(...)` 运算符单独提取一些键，其余键则在对象中

## 展开运算符 {.cols-2}

### 对象扩展

#### 使用对象扩展

```js {2}
const options = {
  ...defaults,
  visible: true,
};
```

#### 不使用对象扩展

```js
const options = Object.assign({}, defaults, { visible: true });
```

对象展开运算符允许您从其他对象构建新对象。参见：
[对象展开](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Spread_syntax)

### 数组扩展

#### 使用数组扩展

```js{2,3}
const users = [
  ...admins,
  ...editors,
  'rstacruz'
]
```

#### 不使用数组扩展

```js
const users = admins.concat(editors).concat(["rstacruz"]);
```

展开运算符允许您以相同的方式构建新数组。参见：
[展开运算符](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Spread_syntax)

## 函数

### 函数参数 {.row-span-3}

#### 默认参数

```js {1}
function greet(name = "Jerry") {
  return `Hello ${name}`;
}
```

#### Rest 参数

```js {1}
function fn(x, ...y) {
  // y 是一个数组
  return x * y.length;
}
```

#### 扩展

```js {1}
fn(...[1, 2, 3]);
//等同于 fn(1, 2, 3)
```

默认 (default)、rest、展开 (extension)。参见：
[函数参数](https://babeljs.io/learn-es2015/#default--rest--spread)

### 箭头函数 {.row-span-3}

#### 箭头函数

```js {1}
setTimeout(() => {
  ···
})
```

#### 带参数

```js {1}
readFile('text.txt', (err, data) => {
  ...
})
```

#### 隐式返回

```js{1,4,5,6}
arr.map(n => n*2)
//没有花括号 = 隐式返回
//等同于: arr.map(function (n) { return n*2 })
arr.map(n => ({
  result: n*2
}))
//隐式返回对象需要在对象周围加上括号
```

类似于函数，但保留 `this`。参见：[箭头函数](https://babeljs.io/learn-es2015/#arrows-and-lexical-this)

### 参数设置默认值

```js
function log(x, y = "World") {
  console.log(x, y);
}

log("Hello"); // Hello World
log("Hello", "China"); // Hello China
log("Hello", ""); // Hello
```

### 与解构赋值默认值结合使用

```js
function foo({ x, y = 5 } = {}) {
  console.log(x, y);
}

foo(); // undefined 5
```

### name 属性

```js
function foo() {}
foo.name; // "foo"
```

### length 属性

```js
function foo(a, b) {}
foo.length; // 2
```

## 对象

### 简写语法

```js
module.exports = { hello, bye };
```

等同于：

```js
module.exports = {
  hello: hello,
  bye: bye,
};
```

参见：[增强的对象字面量](https://babeljs.io/learn-es2015/#enhanced-object-literals)

### 方法

```js {2}
const App = {
  start() {
    console.log("running");
  },
};
//等同于: App = { start: function () {···} }
```

参见：[增强的对象字面量](https://babeljs.io/learn-es2015/#enhanced-object-literals)

### Getters 和 setters

```js{2,5}
const App = {
  get closed () {
    return this.status === 'closed'
  },
  set closed (value) {
    this.status = value ? 'closed' : 'open'
  }
}
```

参见：[增强的对象字面量](https://babeljs.io/learn-es2015/#enhanced-object-literals)

### 计算属性名

```js {3}
let event = "click";
let handlers = {
  [`on${event}`]: true,
};
//等同于: handlers = { 'onclick': true }
```

参见：[增强的对象字面量](https://babeljs.io/learn-es2015/#enhanced-object-literals)

### 提取值

```js{3,5}
const fatherJS = { age: 57, name: "Zhang San" }
Object.values(fatherJS)
//[57, "Zhang San"]
Object.entries(fatherJS)
//[["age", 57], ["name", "Zhang San"]]
```

## 模块 module

### 导入 import

```js
import "helpers";
//即: require('···')
```

---

```js
import Express from "express";
//即: const Express = require('···').default || require('···')
```

---

```js
import { indent } from "helpers";
//即: const indent = require('···').indent
```

---

```js
import * as Helpers from "helpers";
//即: const Helpers = require('···')
```

---

```js
import { indentSpaces as indent } from "helpers";
//即: const indent = require('···').indentSpaces
```

`import` 是新的 `require()`。参见：[模块导入](https://babeljs.io/learn-es2015/#modules)

### 导出 export

```js
export default function () { ··· }
//即: module.exports.default = ···
```

---

```js
export function mymethod () { ··· }
//即: module.exports.mymethod = ···
```

---

```js
export const pi = 3.14159;
//即: module.exports.pi = ···
```

---

```js
const firstName = "Michael";
const lastName = "Jackson";
const year = 1958;
export { firstName, lastName, year };
```

---

```js
export * from "lib/math";
```

`export` 是新的 `module.exports`。参见：[模块导出](https://babeljs.io/learn-es2015/#modules)

### `as` 关键字重命名

```js{2,8,12-14}
import {
  lastName as surname // 导入重命名
} from './profile.js';

function v1() { ... }
function v2() { ... }

export { v1 as default };
//等同于 export default v1;

export {
  v1 as streamV1, // 导出重命名
  v2 as streamV2, // 导出重命名
  v2 as streamLatestVersion // 导出重命名
};
```

### 动态加载模块

```js
button.addEventListener("click", (event) => {
  import("./dialogBox.js")
    .then((dialogBox) => {
      dialogBox.open();
    })
    .catch((error) => {
      /*错误处理 */
    });
});
```

[ES2020 提案](https://github.com/tc39/proposal-dynamic-import) 引入了 `import()` 函数

### import() 允许动态生成模块路径

```js
const main = document.querySelector("main");

import(`./modules/${someVariable}.js`)
  .then((module) => {
    module.loadPageInto(main);
  })
  .catch((err) => {
    main.textContent = err.message;
  });
```

### import.meta

[ES2020](https://github.com/tc39/proposal-import-meta) 为 `import` 命令添加了一个元属性 `import.meta`，
它返回当前模块的元信息

```js
new URL("data.txt", import.meta.url);
```

在 Node.js 环境中，`import.meta.url` 总是返回一个本地路径，即 `file:URL` 协议的字符串，
例如 `file:/// home/user/foo.js`

### 导入断言 {.col-span-2}

#### 静态导入

```js
import json from "./package.json" assert { type: "json" };
//导入 json 文件中的所有对象
```

#### 动态导入

```js
const json = await import("./package.json", { assert: { type: "json" } });
```

## 生成器

### 生成器函数

```js
function* idMaker() {
  let id = 0;
  while (true) {
    yield id++;
  }
}
```

---

```js
let gen = idMaker();
gen.next().value; // → 0
gen.next().value; // → 1
gen.next().value; // → 2
```

这很复杂。参见：[生成器](https://babeljs.io/learn-es2015/#generators)

### For..of + 迭代器 {.row-span-2}

```js
let fibonacci = {
  [Symbol.iterator]() {
    let pre = 0,
      cur = 1;
    return {
      next() {
        [pre, cur] = [cur, pre + cur];
        return { done: false, value: cur };
      },
    };
  },
};

for (var n of fibonacci) {
  // 在 1000 处截断序列
  if (n > 1000) break;
  console.log(n);
}
```

用于迭代生成器和数组。参见：[For..of 迭代](https://babeljs.io/learn-es2015/#iterators--forof)

### 与 Iterator 接口的关系

```js
var gen = {};
gen[Symbol.iterator] = function* () {
  yield 1;
  yield 2;
  yield 3;
};

[...gen]; // => [1, 2, 3]
```

`Generator` 函数被赋值给 `Symbol.iterator` 属性，因此 `gen` 对象具有 `Iterator`
接口，可以通过 `...` 运算符进行遍历

### Symbol.iterator 属性

```js
function* gen() {
  /*一些代码 */
}
var g = gen();

g[Symbol.iterator]() === g; // true
```

`gen` 是一个 `Generator` 函数，调用它会生成一个遍历器对象 `g`。它的 `Symbol.iterator` 属性，
也是一个迭代器对象生成函数，执行后返回自身

## 另见

- [学习 ES2015](https://babeljs.io/docs/en/learn/)_(babeljs.io)_
- [ECMAScript 6 特性概览](https://github.com/lukehoban/es6features#readme) _(github.com)_

