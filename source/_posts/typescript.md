---
title: TypeScript
date: 2024-05-28 22:12:25
background: bg-[#4476c0]
tags:
  - ts
  - web
categories:
  - 编程
intro: |
  一份 TypeScript 速查表，包含最重要的概念、函数、方法等。为初学者准备的完整快速参考。
plugins:
  - copyCode
  - runCode
---

## 入门指南

### 安装编译器

```shell
npm install typescript --save-dev
npm tsc
```

## 基本数据类型

### 基本类型

```ts
let isDone: boolean = false;
let age: number = 30;
let userName: string = "John";
let list: number[] = [1, 2, 3];
let tuple: [string, number] = ["hello", 10];
let notSure: any = 4;
notSure = "maybe a string instead"; // 也许是一个字符串
```

### 枚举 (enums)

```ts
enum Color {
  Red,
  Green,
  Blue,
}
let c: Color = Color.Green;
```

### 接口 (interface)

```ts
interface Person {
  firstName: string;
  lastName: string;
  age?: number; // 可选属性
}

function greet(person: Person) {
  return "Hello, " + person.firstName + " " + person.lastName;
}
```

### 函数 (Functions)

```ts
function add(x: number, y: number): number {
  return x + y;
}

let myAdd = function (x: number, y: number): number {
  return x + y;
};

let myArrowAdd = (x: number, y: number): number => x + y;

function buildName(firstName: string, lastName = "Smith") {
  return firstName + " " + lastName;
}

function buildFullName(firstName: string, ...restOfName: string[]) {
  return firstName + " " + restOfName.join(" ");
}
```

### 类 (Classes)

```ts
class Greeter {
  greeting: string;
  constructor(message: string) {
    this.greeting = message;
  }
  greet() {
    return "Hello, " + this.greeting;
  }
}

let greeter = new Greeter("world");
```

### 继承 (Inheritance)

```ts
class Animal {
  move(distance: number = 0) {
    console.log(`Animal moved ${distance} meters.`);
  }
}

class Dog extends Animal {
  bark() {
    console.log("Woof! Woof!");
  }
}

const dog = new Dog();
dog.bark();
dog.move(10);
dog.bark();
```

### 泛型 (Generics)

```ts
function identity<T>(arg: T): T {
  return arg;
}

let output1 = identity<string>("myString");
let output2 = identity<number>(42);
```

### 类型断言 (Type Assertions)

```ts
let someValue: any = "this is a string";
let strLength: number = (<string>someValue).length;
// 或者
let strLength2: number = (someValue as string).length;
```

## 模块 (Modules)

### 导出 (Export)

```ts
export interface StringValidator {
  isAcceptable(s: string): boolean;
}

export class ZipCodeValidator implements StringValidator {
  isAcceptable(s: string) {
    return s.length === 5;
  }
}
```

### 导入 (Import)

```ts
import { ZipCodeValidator } from "./ZipCodeValidator";

let myValidator = new ZipCodeValidator();
```

### 命名空间 (Namespaces)

```ts
namespace Validation {
  export interface StringValidator {
    isAcceptable(s: string): boolean;
  }

  export class LettersOnlyValidator implements StringValidator {
    isAcceptable(s: string) {
      return /^[A-Za-z]+$/.test(s);
    }
  }
}

let validator = new Validation.LettersOnlyValidator();
```

## 联合类型和交叉类型 (Union and Intersection Types)

### 联合类型 (Union Types)

```ts
function padLeft(value: string, padding: string | number) {
  if (typeof padding === "number") {
    return Array(padding + 1).join(" ") + value;
  }
  if (typeof padding === "string") {
    return padding + value;
  }
  throw new Error(`Expected string or number, got '${padding}'.`);
}
```

### 交叉类型 (Intersection Types)

```ts
interface ErrorHandling {
  success: boolean;
  error?: { message: string };
}

interface ArtworksData {
  artworks: { title: string }[];
}

type ArtworksResponse = ArtworksData & ErrorHandling;

const response: ArtworksResponse = {
  success: true,
  artworks: [{ title: "Mona Lisa" }],
};
```

## 工具类型 (Utility Types)

### Partial

```ts
interface User {
  id: number;
  name: string;
  age: number;
}

let partialUser: Partial<User> = {
  name: "Alice",
};
```

### Readonly

```ts
let readonlyUser: Readonly<User> = {
  id: 1,
  name: "Bob",
  age: 25,
};

// readonlyUser.age = 26; // 错误：无法重新分配只读属性
```

### Pick

```ts
type UserName = Pick<User, "name">;

let userName: UserName = {
  name: "Charlie",
};
```

### Omit

```ts
type UserWithoutAge = Omit<User, "age">;

let userWithoutAge: UserWithoutAge = {
  id: 2,
  name: "Dave",
};
```

## 装饰器 (Decorators)

### 类装饰器 (Class Decorator)

```ts
function sealed(constructor: Function) {
  Object.seal(constructor);
  Object.seal(constructor.prototype);
}

@sealed
class Greeter {
  greeting: string;
  constructor(message: string) {
    this.greeting = message;
  }
  greet() {
    return "Hello, " + this.greeting;
  }
}
```

### 方法装饰器 (Method Decorator)

```ts
function enumerable(value: boolean) {
  return function (target: any, propertyKey: string, descriptor: PropertyDescriptor) {
    descriptor.enumerable = value;
  };
}

class Greeter {
  greeting: string;
  constructor(message: string) {
    this.greeting = message;
  }

  @enumerable(false)
  greet() {
    return "Hello, " + this.greeting;
  }
}
```

### 异步/等待 (Async/Await)

```ts
async function fetchData(url: string) {
  let response = await fetch(url);
  let data = await response.json();
  return data;
}
```

## 另请阅读

- [TypeScript](https://www.typescriptlang.org/docs/)
