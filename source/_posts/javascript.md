---
title: JavaScript 教程
date: 2020-12-24 17:12:25
background: bg-[#ebd94e]
tags:
  - js
  - web
categories:
  - 编程
intro: |
  一份 JavaScript 速查表，包含最重要的概念、函数、方法等。为初学者准备的完整快速参考。
plugins:
  - copyCode
  - runCode
---

## 入门指南

### 简介

JavaScript 是一种轻量级的解释型编程语言。

- [JSON 速查表](/json) _(r3f.cn)_
- [JavaScript 中的正则表达式](/regex#regex-in-javascript) _(r3f.cn)_

### 控制台

```javascript
// => Hello world!
console.log("Hello world!");

// => Hello r3f.cn
console.warn("hello %s", "r3f.cn");

// 将错误消息打印到 stderr
console.error(new Error("Oops!"));
```

### 数字

```javascript
let amount = 6;
let price = 4.99;
```

### 变量

```javascript
let x = null;
let name = "Tammy";
const found = false;

// => Tammy, false, null
console.log(name, found, x);

var a;
console.log(a); // => undefined
```

### 字符串

```javascript
let single = "Wheres my bandit hat?";
let double = "Wheres my bandit hat?";

// => 21
console.log(single.length);
```

### 算术运算符

```javascript
5 + 5 = 10     // 加法
10 - 5 = 5     // 减法
5 * 10 = 50    // 乘法
10 / 5 = 2     // 除法
10 % 5 = 0     // 取模
```

### 注释

```javascript
// 这一行表示注释

/*
以下配置必须在
部署前更改。
*/
```

### 赋值运算符

```javascript
let number = 100;

// 两个语句都会加 10
number = number + 10;
number += 10;

console.log(number);
// => 120
```

### 字符串插值

```javascript
let age = 7;

// 字符串连接
"Tommy is " + age + " years old.";

// 字符串插值
`Tommy is ${age} years old.`;
```

### let 关键字

```javascript
let count;
console.log(count); // => undefined
count = 10;
console.log(count); // => 10
```

### const 关键字

```javascript
const numberOfColumns = 4;

// TypeError: Assignment to constant... (类型错误：给常量赋值...)
numberOfColumns = 8;
```

## JavaScript 条件语句

### if 语句

```javascript
const isMailSent = true;

if (isMailSent) {
  console.log("邮件已发送给收件人");
}
```

### 三元运算符

```javascript
var x = 1;

// => true
result = x == 1 ? true : false;
```

### 运算符 {.row-span-2}

```javascript
true || false; // true
10 > 5 || 10 > 20; // true
false || false; // false
10 > 100 || 10 > 20; // false
```

#### 逻辑运算符 &&

```javascript
true && true; // true
1 > 2 && 2 > 1; // false
true && false; // false
4 === 4 && 3 > 1; // true
```

#### 比较运算符

```javascript
1 > 3; // false
3 > 1; // true
250 >= 250; // true
1 === 1; // true
1 === 2; // false
1 === "1"; // false
```

#### 逻辑运算符 !

```javascript
let lateToWork = true;
let oppositeValue = !lateToWork;

// => false
console.log(oppositeValue);
```

#### 空值合并运算符 ??

```javascript
null ?? "I win"; //  'I win'
undefined ?? "Me too"; //  'Me too'

false ?? "I lose"; //  false
0 ?? "I lose again"; //  0
"" ?? "Damn it"; //  ''
```

### else if

```javascript
const size = 10;

if (size > 100) {
  console.log("大");
} else if (size > 20) {
  console.log("中");
} else if (size > 4) {
  console.log("小");
} else {
  console.log("微小");
}
// 输出: 小
```

### switch 语句

```javascript
const food = "salad";

switch (food) {
  case "oyster":
    console.log("大海的味道");
    break;
  case "pizza":
    console.log("美味的披萨");
    break;
  default:
    console.log("祝您用餐愉快");
}
```

### == vs ===

```javascript
0 == false; // true
0 === false; // false, 类型不同
1 == "1"; // true,  自动类型转换
1 === "1"; // false, 类型不同
null == undefined; // true
null === undefined; // false
"0" == false; // true
"0" === false; // false
```

`==` 只检查值，`===` 检查值和类型。

## JavaScript 函数

### 函数

```javascript
// 定义函数:
function sum(num1, num2) {
  return num1 + num2;
}

// 调用函数:
sum(3, 6); // 9
```

### 匿名函数

```javascript
// 命名函数
function rocketToMars() {
  return "BOOM!";
}

// 匿名函数
const rocketToMars = function () {
  return "BOOM!";
};
```

### 箭头函数 (ES6) {.row-span-2}

#### 带两个参数

```javascript
const sum = (param1, param2) => {
  return param1 + param2;
};
console.log(sum(2, 5)); // => 7
```

#### 不带参数

```javascript
const printHello = () => {
  console.log("hello");
};
printHello(); // => hello
```

#### 带单个参数

```javascript
const checkWeight = (weight) => {
  console.log(`Weight : ${weight}`);
};
checkWeight(25); // => Weight : 25
```

#### 简洁箭头函数

```javascript
const multiply = (a, b) => a * b;
// => 60
console.log(multiply(2, 30));
```

[箭头函数](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions) 从 ES2015 开始可用。

### return 关键字

```javascript
// 带 return
function sum(num1, num2) {
  return num1 + num2;
}

// 函数不输出和
function sum(num1, num2) {
  num1 + num2;
}
```

### 调用函数

```javascript
// 定义函数
function sum(num1, num2) {
  return num1 + num2;
}

// 调用函数
sum(2, 4); // 6
```

### 函数表达式

```javascript
const dog = function () {
  return "Woof!";
};
```

### 函数参数

```javascript
// 参数是 name
function sayHello(name) {
  return `Hello, ${name}!`;
}
```

### 函数声明

```javascript
function add(num1, num2) {
  return num1 + num2;
}
```

## JavaScript 作用域

### 作用域

```javascript
function myFunction() {
  var pizzaName = "Margarita";
  // 这里的代码可以使用 pizzaName
}

// 这里的代码不能使用 pizzaName
```

### 块级作用域变量

```javascript
const isLoggedIn = true;

if (isLoggedIn == true) {
  const statusMessage = "Logged in.";
}

// Uncaught ReferenceError... (未捕获的引用错误...)
console.log(statusMessage);
```

### 全局变量

```javascript
// 全局声明的变量
const color = "blue";

function printColor() {
  console.log(color);
}

printColor(); // => blue
```

### let vs var

```javascript
for (let i = 0; i < 3; i++) {
  // 这是 'let' 的最大作用域
  // i 可访问 ✔️
}
// i 不可访问 ❌
```

---

```javascript
for (var i = 0; i < 3; i++) {
  // i 可访问 ✔️
}
// i 可访问 ✔️
```

`var` 的作用域是最近的函数块，而 `let` 的作用域是最近的封闭块。

### 带闭包的循环

```javascript{.wrap}
// 打印三次 3，不是我们想要的。
for (var i = 0; i < 3; i++) {
  setTimeout(_ => console.log(i), 10);
}
```

---

```javascript{.wrap}
// 按预期打印 0, 1 和 2。
for (let j = 0; j < 3; j++) {
  setTimeout(_ => console.log(j), 10);
}
```

使用 `let` 时变量有自己的副本，使用 `var` 时变量共享副本。

## JavaScript 数组

### 数组

```javascript
const fruits = ["apple", "orange", "banana"];

// 不同数据类型
const data = [1, "chicken", false];
```

### 属性 .length

```javascript
const numbers = [1, 2, 3, 4];

numbers.length; // 4
```

### 索引

```javascript
// 访问数组元素
const myArray = [100, 200, 300];

console.log(myArray[0]); // 100
console.log(myArray[1]); // 200
```

### 可变方法表

|           | 添加 | 移除 | 开头 | 末尾 |
| :-------- | :--: | :----: | :---: | :--: |
| `push`    |  ✔   |        |       |  ✔   |
| `pop`     |      |   ✔    |       |  ✔   |
| `unshift` |  ✔   |        |   ✔   |      |
| `shift`   |      |   ✔    |   ✔   |      |

{.show-header}

### Array.push()

```javascript
// 添加单个元素:
const cart = ["apple", "orange"];
cart.push("pear");

// 添加多个元素:
const numbers = [1, 2];
numbers.push(3, 4, 5);
```

向数组末尾添加项并返回新的数组长度。

### Array.pop()

```javascript
const fruits = ["apple", "orange", "banana"];

const fruit = fruits.pop(); // 'banana'
console.log(fruits); // ["apple", "orange"]
```

从数组末尾移除一项并返回移除的项。

### Array.shift()

```javascript
let cats = ["Bob", "Willy", "Mini"];

cats.shift(); // ['Willy', 'Mini']
```

从数组开头移除一项并返回移除的项。

### Array.unshift()

```javascript
let cats = ["Bob"];

// => ['Willy', 'Bob']
cats.unshift("Willy");

// => ['Puff', 'George', 'Willy', 'Bob']
cats.unshift("Puff", "George");
```

向数组开头添加项并返回新的数组长度。

### Array.concat()

```javascript
const numbers = [3, 2, 1];
const newFirstNumber = 4;

// => [ 4, 3, 2, 1 ]
[newFirstNumber].concat(numbers);

// => [ 3, 2, 1, 4 ]
numbers.concat(newFirstNumber);
```

如果你想避免修改原始数组，可以使用 concat。

## JavaScript Set

### 创建 Set

```javascript
// 空 Set 对象
const emptySet = new Set();

// 带值的 Set 对象
const setObj = new Set([1, true, "hi"]);
```

### 添加

```javascript
const emptySet = new Set();

// 添加值
emptySet.add("a"); // 'a'
emptySet.add(1); // 'a', 1
emptySet.add(true); // 'a', 1, true
emptySet.add("a"); // 'a', 1, true (Set 中元素唯一)
```

### 删除

```javascript
const emptySet = new Set([1, true, "a"]);

// 删除值
emptySet.delete("a"); // 1, true
emptySet.delete(true); // 1
emptySet.delete(1); //
```

### 检查是否存在

```javascript
const setObj = new Set([1, true, "a"]);

// 返回 true 或 false
setObj.has("a"); // true
setObj.has(1); // true
setObj.has(false); // false
```

### 清空

```javascript
const setObj = new Set([1, true, "a"]);

// 清空 set
console.log(setObj); // 1, true, 'a'
setObj.clear(); //
```

### 大小

```javascript
const setObj = new Set([1, true, "a"]);

consoloe.log(setObj.size); // 3
```

### ForEach 遍历

```javascript
const setObj = new Set([1, true, "a"]);

setObj.forEach(function (value) {
  console.log(value);
});

// 1
// true
// 'a'
```

## JavaScript 循环

### While 循环

```javascript
while (condition) {
  // 要执行的代码块
}

let i = 0;
while (i < 5) {
  console.log(i);
  i++;
}
```

### 反向循环

```javascript
const fruits = ["apple", "orange", "banana"];

for (let i = fruits.length - 1; i >= 0; i--) {
  console.log(`${i}. ${fruits[i]}`);
}

// => 2. banana
// => 1. orange
// => 0. apple
```

### Do…While 语句

```javascript
x = 0;
i = 0;

do {
  x = x + i;
  console.log(x);
  i++;
} while (i < 5);
// => 0 1 3 6 10
```

### For 循环

```javascript
for (let i = 0; i < 4; i += 1) {
  console.log(i);
}

// => 0, 1, 2, 3
```

### 遍历数组

```javascript
for (let i = 0; i < array.length; i++) {
  console.log(array[i]);
}

// => 数组中的每一项
```

### Break

```javascript
for (let i = 0; i < 99; i += 1) {
  if (i > 5) {
    break;
  }
  console.log(i);
}
// => 0 1 2 3 4 5
```

### Continue

```javascript
for (i = 0; i < 10; i++) {
  if (i === 3) {
    continue;
  }
  text += "The number is " + i + "<br>";
}
```

### 嵌套循环

```javascript
for (let i = 0; i < 2; i += 1) {
  for (let j = 0; j < 3; j += 1) {
    console.log(`${i}-${j}`);
  }
}
```

### for...in 循环

```javascript
const fruits = ["apple", "orange", "banana"];

for (let index in fruits) {
  console.log(index);
}
// => 0
// => 1
// => 2
```

### for...of 循环

```javascript
const fruits = ["apple", "orange", "banana"];

for (let fruit of fruits) {
  console.log(fruit);
}
// => apple
// => orange
// => banana
```

## JavaScript 迭代器 {.cols-2}

### 赋值给变量的函数

```javascript
let plusFive = (number) => {
  return number + 5;
};
// f 被赋值为 plusFive
let f = plusFive;

plusFive(3); // 8
// 因为 f 的值是一个函数，所以它可以被调用。
f(9); // 14
```

### 回调函数

```javascript
const isEven = (n) => {
  return n % 2 == 0;
};

let printMsg = (evenFunc, num) => {
  const isNumEven = evenFunc(num);
  console.log(`${num} 是偶数: ${isNumEven}.`);
};

// 将 isEven 作为回调函数传入
printMsg(isEven, 4);
// => 4 是偶数: True.
```

### Array.reduce()

```javascript
const numbers = [1, 2, 3, 4];

const sum = numbers.reduce((accumulator, curVal) => {
  return accumulator + curVal;
});

console.log(sum); // 10
```

### Array.map()

```javascript
const members = ["Taylor", "Donald", "Don", "Natasha", "Bobby"];

const announcements = members.map((member) => {
  return member + " 加入了比赛。";
});

console.log(announcements);
```

### Array.forEach()

```javascript
const numbers = [28, 77, 45, 99, 27];

numbers.forEach((number) => {
  console.log(number);
});
```

### Array.filter()

```javascript
const randomNumbers = [4, 11, 42, 14, 39];
const filteredArray = randomNumbers.filter((n) => {
  return n > 5;
});
```

## JavaScript 对象 {.cols-2}

### 访问属性

```javascript
const apple = {
  color: "Green",
  price: { bulk: "$3/kg", smallQty: "$4/kg" },
};
console.log(apple.color); // => Green
console.log(apple.price.bulk); // => $3/kg
```

### 命名属性

```javascript
// 无效键名的示例
const trainSchedule = {
  // 无效，因为单词之间有空格。
  platform num: 10,
  // 表达式不能作为键。
  40 - 10 + 2: 30,
  // + 号无效，除非用引号括起来。
  +compartment: 'C'
}
```

### 不存在的属性

```javascript
const classElection = {
  date: "January 12",
};

console.log(classElection.place); // undefined
```

### 可变性 {.row-span-2}

```javascript
const student = {
  name: "Sheldon",
  score: 100,
  grade: "A",
};

console.log(student);
// { name: 'Sheldon', score: 100, grade: 'A' }

delete student.score;
student.grade = "F";
console.log(student);
// { name: 'Sheldon', grade: 'F' }

student = {};
// TypeError: Assignment to constant variable. (类型错误：给常量赋值。)
```

### 赋值简写语法

```javascript
const person = {
  name: "Tom",
  age: "22",
};
const { name, age } = person;
console.log(name); // 'Tom'
console.log(age); // '22'
```

### delete 运算符

```javascript
const person = {
  firstName: "Matilda",
  age: 27,
  hobby: "knitting",
  goal: "learning JavaScript",
};

delete person.hobby; // 或者 delete person[hobby];

console.log(person);
/*
{
  firstName: "Matilda"
  age: 27
  goal: "learning JavaScript"
}
*/
```

### 对象作为参数

```javascript
const origNum = 8;
const origObj = { color: "blue" };

const changeItUp = (num, obj) => {
  num = 7;
  obj.color = "red";
};

changeItUp(origNum, origObj);

// 将输出 8，因为整数是按值传递的。
console.log(origNum);

// 将输出 'red'，因为对象是按引用传递的，
// 因此是可变的。
console.log(origObj.color);
```

### 对象创建简写

```javascript
const activity = "Surfing";
const beach = { activity };
console.log(beach); // { activity: 'Surfing' }
```

### this 关键字

```javascript
const cat = {
  name: "Pipey",
  age: 8,
  whatName() {
    return this.name;
  },
};
console.log(cat.whatName()); // => Pipey
```

### 工厂函数

```javascript
// 一个工厂函数，接受 'name'、
// 'age' 和 'breed' 参数来返回
// 一个自定义的 dog 对象。
const dogFactory = (name, age, breed) => {
  return {
    name: name,
    age: age,
    breed: breed,
    bark() {
      console.log("Woof!");
    },
  };
};
```

### 对象方法

```javascript
const engine = {
  // 方法简写，带一个参数
  start(adverb) {
    console.log(`引擎 ${adverb} 启动了...`);
  },
  // 匿名箭头函数表达式，不带参数
  sputter: () => {
    console.log("引擎 sputtering...");
  },
};

engine.start("noisily");
engine.sputter();
```

### Getters 和 Setters

```javascript
const myCat = {
  _name: "Dottie",
  get name() {
    return this._name;
  },
  set name(newName) {
    this._name = newName;
  },
};

// 引用调用 getter
console.log(myCat.name);

// 赋值调用 setter
myCat.name = "Yankee";
```

## JavaScript 类

### 静态方法

```javascript
class Dog {
  constructor(name) {
    this._name = name;
  }

  introduce() {
    console.log("This is " + this._name + " !");
  }

  // 静态方法
  static bark() {
    console.log("Woof!");
  }
}

const myDog = new Dog("Buster");
myDog.introduce();

// 调用静态方法
Dog.bark();
```

### 类

```javascript
class Song {
  constructor() {
    this.title;
    this.author;
  }

  play() {
    console.log("歌曲正在播放!");
  }
}

const mySong = new Song();
mySong.play();
```

### 类构造函数

```javascript
class Song {
  constructor(title, artist) {
    this.title = title;
    this.artist = artist;
  }
}

const mySong = new Song("Bohemian Rhapsody", "Queen");
console.log(mySong.title);
```

### 类方法

```javascript
class Song {
  play() {
    console.log("正在播放!");
  }

  stop() {
    console.log("正在停止!");
  }
}
```

### extends

```javascript
// 父类
class Media {
  constructor(info) {
    this.publishDate = info.publishDate;
    this.name = info.name;
  }
}

// 子类
class Song extends Media {
  constructor(songData) {
    super(songData);
    this.artist = songData.artist;
  }
}

const mySong = new Song({
  artist: "Queen",
  name: "Bohemian Rhapsody",
  publishDate: 1975,
});
```

## JavaScript 模块 {.cols-2}

### 导出

```javascript
// myMath.js

// 默认导出
export default function add(x, y) {
  return x + y;
}

// 普通导出
export function subtract(x, y) {
  return x - y;
}

// 多个导出
function multiply(x, y) {
  return x * y;
}
function duplicate(x) {
  return x * 2;
}
export { multiply, duplicate };
```

### 导入

```javascript
// main.js
import add, { subtract, multiply, duplicate } from './myMath.js';

console.log(add(6, 2)); // 8
console.log(subtract(6, 2)) // 4
console.log(multiply(6, 2)); // 12
console.log(duplicate(5)) // 10

// index.html
<script type="module" src="main.js"></script>
```

### 导出模块 (Node.js)

```javascript
// myMath.js

function add(x, y) {
  return x + y;
}
function subtract(x, y) {
  return x - y;
}
function multiply(x, y) {
  return x * y;
}
function duplicate(x) {
  return x * 2;
}

// Node.js 中的多个导出
module.exports = {
  add,
  subtract,
  multiply,
  duplicate,
};
```

### 导入模块 (Node.js)

```javascript
// main.js
const myMath = require("./myMath.js");

console.log(myMath.add(6, 2)); // 8
console.log(myMath.subtract(6, 2)); // 4
console.log(myMath.multiply(6, 2)); // 12
console.log(myMath.duplicate(5)); // 10
```

## JavaScript Promises {.cols-2}

### Promise 状态 {.row-span-2}

```javascript
const promise = new Promise((resolve, reject) => {
  const res = true;
  // 异步操作。
  if (res) {
    resolve("已解决!");
  } else {
    reject(Error("错误"));
  }
});

promise.then(
  (res) => console.log(res),
  (err) => console.error(err),
);
```

### 执行器函数

```javascript
const executorFn = (resolve, reject) => {
  resolve("已解决!");
};

const promise = new Promise(executorFn);
```

### setTimeout()

```javascript
const loginAlert = () => {
  console.log("登录");
};

setTimeout(loginAlert, 6000);
```

### .then() 方法

```javascript
const promise = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve("结果");
  }, 200);
});

promise.then(
  (res) => {
    console.log(res);
  },
  (err) => {
    console.error(err);
  },
);
```

### Promise.catch()

```javascript
const promise = new Promise((resolve, reject) => {
  setTimeout(() => {
    reject(Error("Promise 无条件拒绝。"));
  }, 1000);
});

promise.then((res) => {
  console.log(value);
});

promise.catch((err) => {
  console.error(err);
});
```

### Promise.all()

```javascript
const promise1 = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve(3);
  }, 300);
});
const promise2 = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve(2);
  }, 200);
});

Promise.all([promise1, promise2]).then((res) => {
  console.log(res[0]);
  console.log(res[1]);
});
```

### 避免嵌套 Promise 和 .then()

```javascript
const promise = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve("*");
  }, 1000);
});

const twoStars = (star) => {
  return star + star;
};

const oneDot = (star) => {
  return star + ".";
};

const print = (val) => {
  console.log(val);
};

// 将它们链接在一起
promise.then(twoStars).then(oneDot).then(print);
```

### 创建 Promise

```javascript
const executorFn = (resolve, reject) => {
  console.log("Promise 的执行器函数!");
};

const promise = new Promise(executorFn);
```

### 链接多个 .then()

```javascript
const promise = new Promise((resolve) => setTimeout(() => resolve("dAlan"), 100));

promise
  .then((res) => {
    return res === "Alan" ? Promise.resolve("Hey Alan!") : Promise.reject("你是谁?");
  })
  .then(
    (res) => {
      console.log(res);
    },
    (err) => {
      console.error(err);
    },
  );
```

### 使用 Promise 模拟 http 请求

```javascript
const mock = (success, timeout = 1000) => {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      if (success) {
        resolve({ status: 200, data: {} });
      } else {
        reject({ message: "错误" });
      }
    }, timeout);
  });
};
const someEvent = async () => {
  try {
    await mock(true, 1000);
  } catch (e) {
    console.log(e.message);
  }
};
```

## JavaScript Async-Await {.cols-2}

### 异步

```javascript
function helloWorld() {
  return new Promise((resolve) => {
    setTimeout(() => {
      resolve("Hello World!");
    }, 2000);
  });
}

const msg = async function () {
  //异步函数表达式
  const msg = await helloWorld();
  console.log("消息:", msg);
};

const msg1 = async () => {
  //异步箭头函数
  const msg = await helloWorld();
  console.log("消息:", msg);
};

msg(); // 消息: Hello World! <-- 2 秒后
msg1(); // 消息: Hello World! <-- 2 秒后
```

### 解析 Promises

```javascript
let pro1 = Promise.resolve(5);
let pro2 = 44;
let pro3 = new Promise(function (resolve, reject) {
  setTimeout(resolve, 100, "foo");
});

Promise.all([pro1, pro2, pro3]).then(function (values) {
  console.log(values);
});
// 预期 => Array [5, 44, "foo"]
```

### Async Await Promises

```javascript
function helloWorld() {
  return new Promise((resolve) => {
    setTimeout(() => {
      resolve("Hello World!");
    }, 2000);
  });
}

async function msg() {
  const msg = await helloWorld();
  console.log("消息:", msg);
}

msg(); // 消息: Hello World! <-- 2 秒后
```

### 错误处理

```javascript
let json = '{ "age": 30 }'; // 不完整的数据

try {
  let user = JSON.parse(json); // <-- 没有错误
  console.log(user.name); // 没有 name!
} catch (e) {
  console.error("无效的 JSON 数据!");
}
```

### Async await 运算符

```javascript
function helloWorld() {
  return new Promise((resolve) => {
    setTimeout(() => {
      resolve("Hello World!");
    }, 2000);
  });
}

async function msg() {
  const msg = await helloWorld();
  console.log("消息:", msg);
}

msg(); // 消息: Hello World! <-- 2 秒后
```

## JavaScript 请求

### JSON

```json
const jsonObj = {
  "name": "Rick",
  "id": "11A",
  "level": 4
};
```

另请参阅: [JSON 速查表](/json)

### XMLHttpRequest

```javascript
const xhr = new XMLHttpRequest();
xhr.open("GET", "mysite.com/getjson");
```

`XMLHttpRequest` 是一个浏览器级别的 API，它使客户端能够通过 JavaScript 编写数据传输脚本，它不是 JavaScript 语言的一部分。

### GET

```javascript
const req = new XMLHttpRequest();
req.responseType = "json";
req.open("GET", "/getdata?id=65");
req.onload = () => {
  console.log(xhr.response);
};

req.send();
```

### POST {.row-span-2}

```javascript
const data = {
  fish: "Salmon",
  weight: "1.5 KG",
  units: 5,
};
const xhr = new XMLHttpRequest();
xhr.open("POST", "/inventory/add");
xhr.responseType = "json";
xhr.send(JSON.stringify(data));

xhr.onload = () => {
  console.log(xhr.response);
};
```

### fetch api {.row-span-2}

```javascript
fetch(url, {
    method: 'POST',
    headers: {
      'Content-type': 'application/json',
      'apikey': apiKey
    },
    body: data
  }).then(response => {
    if (response.ok) {
      return response.json();
    }
    throw new Error('请求失败!');
  }, networkError => {
    console.log(networkError.message)
  })
}
```

### JSON 格式化

```javascript
fetch("url-that-returns-JSON") // 获取返回 JSON 的 URL
  .then((response) => response.json())
  .then((jsonResponse) => {
    console.log(jsonResponse);
  });
```

### fetch api 的 promise url 参数

```javascript
fetch('url')
.then(
  response  => {
    console.log(response);
  },
 rejection => {
    console.error(rejection.message);
);
```

### Fetch API 函数

```javascript
fetch("https://api-xxx.com/endpoint", {
  method: "POST",
  body: JSON.stringify({ id: "200" }),
})
  .then(
    (response) => {
      if (response.ok) {
        return response.json();
      }
      throw new Error("请求失败!");
    },
    (networkError) => {
      console.log(networkError.message);
    },
  )
  .then((jsonResponse) => {
    console.log(jsonResponse);
  });
```

### async await 语法 {.col-span-2}

```javascript
const getSuggestions = async () => {
  const wordQuery = inputField.value;
  const endpoint = `${url}${queryParams}${wordQuery}`;
  try {
    const response = await fetch(endpoint, { cache: "no-cache" }); // 不使用缓存
    if (response.ok) {
      const jsonResponse = await response.json();
    }
  } catch (error) {
    console.log(error);
  }
};
```
