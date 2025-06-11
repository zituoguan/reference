---
title: Svelte
date: 2025-04-08 19:45:00
background: bg-[#FF3E00]
tags:
  - svelte
  - web
categories:
  - 编程
intro: |
  Svelte 速查表，包含最重要的概念、函数、响应式等等。为初学者准备的完整快速参考，已更新至 Svelte 5。
plugins:
  - copyCode
  - runCode
---

## 入门指南

### 基本语法

```js
<script>
  let name = 'world';
</script>

<h1>Hello {name}!</h1>
```

### 表达式

```js
<script>
  let firstName = "Zehan";
  let lastName = "Khan";

  function fullName() {
    return `${firstName} ${lastName}`;
  }
</script>

<h1>Hello {fullName()}!</h1>
```

### 属性

```js
<script>
  let avatarUrl = 'https://example.com/avatar.png';
</script>

<img src={avatarUrl} alt="Avatar" />
<button class="btn">Click me</button>
```

### 标记中的函数

```js
<script>
  function name() {
    return "Zehan";
  }
</script>

<h1>Hi {name()}!</h1>
```

### 条件渲染 {.col-span-2}

```js
<script>
  let temperature = 24;
  let city = "New York";
</script>

{#if temperature >= 20}
  <p>It is {temperature}°C (Warm) in {city}</p>
{:else}
  <p>It is {temperature}°C in {city}</p>
{/if}
```

注意：Svelte 组件必须始终返回一个根元素或内容。

## 组件

### 函数式组件

```js
<script>
  export let name = "User";
</script>

<div class="UserProfile">
  <div>Hello</div>
  <div>{name}</div>
</div>
```

### 嵌入内部组件

```js
<script>
  import UserAvatar from './UserAvatar.svelte';
</script>

<div class="UserProfile">
  <UserAvatar />
  <UserAvatar />
</div>
```

### 嵌入外部组件

```js
<script>
  import ComponentName from 'some-library';
</script>

<div class="UserProfile">
  <ComponentName />
</div>
```

注意：外部组件应首先通过 npm 安装。

### 高级函数式组件

```js
<script>
  export let firstName;
  export let lastName;

  function fullName() {
    return `${firstName} ${lastName}`;
  }
</script>

<p>{fullName()}</p>
```

## 属性 {.cols-2}

### 向组件传递属性

```js
<Student
  firstName="Zehan"
  lastName="Khan"
  age={23}
  pro={true}
/>
```

### 从组件分配属性

```js
<script>
  export let firstName;
  export let lastName;
  export let age;
</script>

<h1>{firstName} {lastName} is {age}.</h1>
```

## 状态 {.cols-1}

### 本地状态

```js
<script>
  let name = "Zehan";

  function updateName() {
    name = prompt("What is your name?") || name;
  }
</script>

<h1>{name}</h1>
<button on:click={updateName}>Update name</button>
```

## 事件 {.cols-1}

### 事件监听器

```js
<script>
  function handleClick(event) {
    event.preventDefault();
    alert("Hello World");
  }
</script>

<a href="#" on:click|preventDefault={handleClick}>
  Say Hi
</a>
```

注意：最常见的事件监听器是 `on:click` 和 `on:submit`。

## 循环 {.cols-2}

### 遍历数组

```js
<script>
  let elements = ["one", "two", "three"];
</script>

<ul>
  {#each elements as value, index}
    <li>{value}</li>
  {/each}
</ul>
```

### 遍历对象数组

```js
<script>
  let elements = [
    { name: "one", value: 1 },
    { name: "two", value: 2 },
    { name: "three", value: 3 }
  ];
</script>

<ul>
  {#each elements as element, index}
    <li>
      The value for {element.name} is {element.value}
    </li>
  {/each}
</ul>
```

## 表单 {.cols-1}

### 表单示例

```js
<script>
  let username = "";
  let password = "";

  function handleSubmit(event) {
    event.preventDefault();
    alert(`Logging in with ${username} and ${password}`);
  }
</script>

<form on:submit={handleSubmit}>
  <input type="text" placeholder="Username" bind:value={username} />
  <input type="password" placeholder="Password" bind:value={password} />
  <input type="submit" value="Login" />
</form>
```

## CSS {.cols-1}

### 作用域 CSS

```js
<style>
  .student {
    color: blue;
  }
</style>

<div class="student">Zehan Khan</div>
```

## 获取数据 {.cols-1}

### 使用 onMount 获取数据

```js
<script>
  import { onMount } from 'svelte';
  let notifications = [];
  let loading = true;

  onMount(async () => {
    const res = await fetch("https://notifications.com");
    notifications = await res.json();
    loading = false;
  });
</script>

{#if loading}
  <p>Loading notifications...</p>
{:else}
  <ul>
    {#each notifications as note}
      <li>{note.title}</li>
    {/each}
  </ul>
{/if}
```

注意：使用 `onMount` 处理副作用，如 API 调用。

## 生命周期钩子 {.cols-1}

### onMount
```js
<script>
  import { onMount } from 'svelte';

  onMount(() => {
    console.log('Component mounted');
  });
</script>
```

### beforeUpdate
```js
<script>
  import { beforeUpdate } from 'svelte';

  beforeUpdate(() => {
    console.log('Before component updates');
  });
</script>
```

### afterUpdate
```js
<script>
  import { afterUpdate } from 'svelte';

  afterUpdate(() => {
    console.log('After component updates');
  });
</script>
```

### onDestroy
```js
<script>
  import { onDestroy } from 'svelte';

  onDestroy(() => {
    console.log('Component destroyed');
  });
</script>
```
注意：Svelte 生命周期函数类似于 React Hooks，但它们是单独导入并直接在 `<script>` 块中使用的。


## 更多 Svelte 特性 {.cols-1}

### 派生存储 (Derived Store)

```js
// store.js
import { writable, derived } from 'svelte/store';

export const count = writable(0);
export const double = derived(count, $count => $count * 2);
```

```js
// App.svelte
<script>
  import { count, double } from './store.js';
</script>

<p>Count: {$count}</p>
<p>Double: {$double}</p>
```

### 可读存储 (Readable Store)

```js
import { readable } from 'svelte/store';

export const time = readable(new Date(), function start(set) {
  const interval = setInterval(() => {
    set(new Date());
  }, 1000);

  return function stop() {
    clearInterval(interval);
  };
});
```

### 响应式声明

```js
<script>
  let a = 2;
  let b = 3;
  $: sum = a + b;
</script>

<p>{sum}</p>
```

### 带副作用的响应式语句

```js
<script>
  let name = 'Zehan';

  $: console.log('Name changed to', name);
</script>
```

### 绑定到 DOM 属性

```js
<script>
  let text = '';
</script>

<textarea bind:value={text} />
<p>{text.length} characters</p>
```

### 绑定分组输入 (单选框, 复选框)

```js
<script>
  let selected = 'apple';
</script>

<label><input type="radio" bind:group={selected} value="apple" /> Apple</label>
<label><input type="radio" bind:group={selected} value="orange" /> Orange</label>
<p>Selected: {selected}</p>
```

### 类和样式指令

```js
<script>
  let isActive = true;
</script>

<div class:active={isActive}>Toggle me</div>
```

```js
<script>
  let size = 16;
</script>

<p style:font-size={`${size}px`}>Resizable text</p>
```

### Await 块

```js
<script>
  let userPromise = fetch('https://jsonplaceholder.typicode.com/users/1')
    .then(res => res.json());
</script>

{#await userPromise}
  <p>Loading...</p>
{:then user}
  <p>{user.name}</p>
{:catch error}
  <p>Error: {error.message}</p>
{/await}
```

### 使用 SvelteKit 进行 SSR (基本示例)

```js
// +page.server.js
export async function load({ fetch }) {
  const res = await fetch('/api/data');
  const data = await res.json();
  return { data };
}
```

```js
// +page.svelte
<script>
  export let data;
</script>

<h1>{data.title}</h1>
```

注意：需要 SvelteKit 设置才能实现 SSR 路由。
