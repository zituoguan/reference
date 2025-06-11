---
title: React
date: 2023-11-17 10:12:25
background: bg-[#1289D8]
tags:
  - react
  - web
categories:
  - 编程
intro: |
  一份 React 速查表，包含最重要的概念、函数、方法等。为初学者准备的完整快速参考。
plugins:
  - copyCode
  - runCode
---

## 入门指南

### JSX

JSX 是一种 JavaScript 的语法扩展，它允许你在 JavaScript 文件中编写类似 HTML 的标记。

```javascript
let element = <h1>Hello, world!</h1>;

let emptyHeading = <h1 />;
```

### JSX 表达式

```javascript
let name = "Josh Perez";
let element = <h1>Hello, {name}</h1>;

function fullName(firstName, lastName) {
  return firstName + " " + lastName;
}
let element = <h1>Hello, {fullName("Julie", "Johnson")}</h1>;
```

### JSX 属性

```javascript
const element = <img src={user.avatarUrl} />;
const element = <button className="btn">Click me</button>;
```

### JSX 函数

```javascript
name() {
  return "Julie";
}

return (
  <h1>
    Hi {name()}!
  </h1>
)
```

### JSX 条件渲染 {.col-span-2}

```javascript
import React from "react";
function Weather(props) {
  if (props.temperature >= 20) {
    return (
      <p>
        It is {props.temperature}°C (Warm) in {props.city}
      </p>
    );
  } else {
    return (
      <p>
        It is {props.temperature}°C in {props.city}
      </p>
    );
  }
}

export default () => <Weather city="New York" temperature={24} />;
```

注意：组件必须总是返回一些东西。

## 组件

### 函数式组件

```javascript
import React from "react";

export default function UserProfile() {
  return (
    <div className="UserProfile">
      <div>Hello</div>
      <div>World</div>
    </div>
  );
}
```

注意：每个组件都需要一个根元素。

### 嵌入内部组件

```javascript
import React from "react";
import UserAvatar from "./UserAvatar";

export default function UserProfile() {
  return (
    <div className="UserProfile">
      <UserAvatar />
      <UserAvatar />
    </div>
  );
}
```

注意：假设 UserAvatar 在 UserAvatar.js 中声明。

### 嵌入外部组件

```javascript
import React from "react";
import ComponentName from "component-name";

export default function UserProfile() {
  return (
    <div className="UserProfile">
      <ComponentName />
    </div>
  );
}
```

注意：外部组件可以在 npmjs.com 上找到，并且需要先导入。

### 高级函数式组件

```javascript
import React from "react";

function Hello(props) {
  function fullName() {
    return `${props.firstName} ${props.lastName}`;
  }
  return <p>{fullName()}</p>;
}

export default () => <Hello firstName="Matt" lastName="Delac" />;
```

## 属性 {.cols-2}

### 向组件传递属性

<!-- prettier-ignore -->
```javascript
<Student
  firstName="Julie"
  lastName="Johnson"
  age={23}
  pro={true}
/>
```

### 从组件分配属性

```javascript
import React from "react";

export default function Student(props) {
  return (
    <h1>
      {props.firstName} {props.lastName} is {props.age}.
    </h1>
  );
}
```

## 状态 {.cols-1}

### React 状态

```javascript
import React, { useState } from "react";

export default function Hello(props) {
  let [name, setName] = useState("Julie");
  function updateName() {
    let newName = prompt("What is your name?");
    setName(newName);
  }

  return (
    <div>
      <h1>{name}</h1>
      <button onClick={updateName}>Update name</button>
    </div>
  );
}
```

## 事件 {.cols-1}

### 事件监听器

```javascript
import React from "react";

export default function Hello() {
  function handleClick(event) {
    event.preventDefault();
    alert("Hello World");
  }

  return (
    <a href="/" onClick={handleClick}>
      Say Hi
    </a>
  );
}
```

注意：最常见的事件监听器是用于链接/按钮的 onClick 和用于表单的 onSubmit。

## 循环 {.cols-2}

### 遍历数组

```javascript
let elements = ["one", "two", "three"];

return (
  <ul>
    {elements.map(function (value, index) {
      return <li key={index}>{value}</li>;
    })}
  </ul>
);
```

注意：map 循环中的每个列表项都需要一个具有唯一值的 key 属性，通常是索引。

### 遍历对象数组

```javascript
let elements = [
  {
    name: "one",
    value: 1,
  },
  {
    name: "two",
    value: 2,
  },
  {
    name: "three",
    value: 3,
  },
];
return (
  <ul>
    {elements.map(function (element, index) {
      return (
        <li key={index}>
          The value for {element.name} is {element.value}
        </li>
      );
    })}
  </ul>
);
```

注意：map 循环中的每个列表项都需要一个具有唯一值的 key 属性，通常是索引。

## 表单 {.cols-1}

### React 表单

```javascript
import React, { useState } from "react";

export default function LoginForm() {
  let [username, setUsername] = useState("");
  let [password, setPassword] = useState("");

  function handleSubmit(event) {
    event.preventDefault();
    alert(`Loging in with ${username} and ${password}`);
  }

  function updateUsername(event) {
    setUsername(event.target.value);
  }

  function updatePassword(event) {
    setPassword(event.target.value);
  }

  return (
    <form onSubmit={handleSubmit}>
      <input type="text" placeholder="Username" onChange={updateUsername} />
      <input type="password" placeholder="Password" onChange={updatePassword} />
      <input type="submit" value="Login" />
    </form>
  );
}
```

## CSS {.cols-1}

### React 组件中的 CSS

```javascript
import React from "react";
import "./Student.css";

export default function Student() {
  return <div className="Student">Julie Johnson</div>;
}
```

注意：然后你需要创建一个名为 Student.css 的 CSS 文件。

## AJAX {.cols-1}

### 使用 Axios 发送 AJAX 请求

```javascript
import React from "react";
import axios from "axios";

export default function Weather(props) {
  function handleResponse(response) {
    console.log(response);
  }

  if (notifications) {
    return <p>notifications</p>;
  } else {
    let url = `https://notifications.com`;
    axios.get(url).then(handleResponse);
    return <p>Loading notifications..</p>;
  }
}
```

注意：确保首先将 Axios 导入到你的项目中。

## Hooks (钩子) {.cols-2}

### useState Hook

```javascript
import React, { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}

export default Counter;
```

注意：useState Hook 是一个内置的 React Hook，它允许函数式组件管理本地状态。它提供了一种在函数式组件内声明状态变量并更新它们的方法。示例代码演示了如何使用它。

### 多个状态变量声明

```javascript
import React, { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);
  const [name, setName] = useState("");
  const [isCompleted, setIsCompleted] = useState(false);

  const handleIncrement = () => {
    setCount(count + 1);
  };

  const handleNameChange = (event) => {
    setName(event.target.value);
  };

  const toggleCompletion = () => {
    setIsCompleted(!isCompleted);
  };

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={handleIncrement}>Increment</button>

      <input type="text" value={name} onChange={handleNameChange} placeholder="Enter your name" />

      <label>
        <input type="checkbox" checked={isCompleted} onChange={toggleCompletion} />
        Completed
      </label>
    </div>
  );
}

export default Counter;
```

注意：你可以通过在函数式组件中多次调用 useState Hook 来声明多个状态变量。每次调用 useState 都会管理一个独立的状态片段。

### 输入状态管理

```javascript
import { useState } from "react";

function FormExample() {
  const [formData, setFormData] = useState({ name: "", email: "", message: "" });

  const handleChange = (event) => {
    const { name, value } = event.target;
    setFormData((prevFormData) => ({ ...prevFormData, [name]: value }));
  };

  const handleSubmit = (event) => {
    event.preventDefault();
    alert(`Name: ${formData.name}, Email: ${formData.email}, Message: ${formData.message}`);
  };

  return (
    <form onSubmit={handleSubmit}>
      <label htmlFor="name">Name:</label>
      <input type="text" id="name" name="name" value={formData.name} onChange={handleChange} />

      <label htmlFor="email">Email:</label>
      <input type="email" id="email" name="email" value={formData.email} onChange={handleChange} />

      <label htmlFor="message">Message:</label>
      <textarea id="message" name="message" value={formData.message} onChange={handleChange} />

      <button type="submit">Submit</button>
    </form>
  );
}

export default FormExample;
```

### useEffect Hook

```javascript
import React, { useState, useEffect } from "react";

function Timer() {
  const [seconds, setSeconds] = useState(0);

  useEffect(() => {
    const interval = setInterval(() => {
      setSeconds((prevSeconds) => prevSeconds + 1);
    }, 1000);

    return () => clearInterval(interval);
  }, []);

  return <div>Seconds: {seconds}</div>;
}

export default Timer;
```

注意：React 中的 useEffect Hook 用于在函数式组件中执行副作用。它允许你根据组件生命周期事件（如挂载、更新和卸载）执行代码。

### 使用 useEffect 获取 API 数据

```javascript
import React, { useState, useEffect } from "react";
import axios from "axios";

function UserList() {
  const [users, setUsers] = useState([]);

  useEffect(() => {
    axios
      .get("https://jsonplaceholder.typicode.com/users")
      .then((response) => {
        setUsers(response.data);
      })
      .catch((error) => {
        console.error("Error fetching users:", error);
      });
  }, []);

  return (
    <div>
      <h2>User List</h2>
      <ul>
        {users.map((user) => (
          <li key={user.id}>{user.name}</li>
        ))}
      </ul>
    </div>
  );
}

export default UserList;
```

注意：确保首先将 Axios 导入到你的项目中。

### 创建自定义 Hook useLocalStorage

```javascript
import { useState, useEffect } from "react";

function useLocalStorage(key, initialValue) {
  const [value, setValue] = useState(() => {
    const storedValue = localStorage.getItem(key);
    return storedValue !== null ? JSON.parse(storedValue) : initialValue;
  });

  useEffect(() => {
    localStorage.setItem(key, JSON.stringify(value));
  }, [key, value]);

  return [value, setValue];
}

export default useLocalStorage;
```

注意：自定义 Hook 是 React 中的可复用函数，它们包含跨多个组件共享的逻辑。它们允许你将有状态逻辑从组件中提取到独立函数中。

### 在类组件中创建 Refs

```javascript
import React, { Component } from "react";

class MyComponent extends Component {
  constructor(props) {
    super(props);
    this.myRef = React.createRef();
  }

  componentDidMount() {
    console.log(this.myRef.current); // Access the DOM element
  }

  render() {
    return <div ref={this.myRef}>Hello, world!</div>;
  }
}

export default MyComponent;
```

### 在函数式组件中使用 Refs

```javascript
import React, { useRef, useEffect } from "react";

function MyComponent() {
  const myRef = useRef(null);

  useEffect(() => {
    console.log(myRef.current); // Access the DOM element
  }, []);

  return <div ref={myRef}>Hello, world!</div>;
}

export default MyComponent;
```

### 回调 Refs

```javascript
import React, { Component } from "react";

class MyComponent extends Component {
  constructor(props) {
    super(props);
    this.myRef = null;
    this.setRef = (element) => {
      this.myRef = element;
    };
  }

  componentDidMount() {
    console.log(this.myRef); // Access the DOM element
  }

  render() {
    return <div ref={this.setRef}>Hello, world!</div>;
  }
}

export default MyComponent;
```

### Refs 转发

```javascript
import React from "react";

const FancyButton = React.forwardRef((props, ref) => (
  <button ref={ref} className="FancyButton">
    {props.children}
  </button>
));

// Usage
const ref = React.createRef();
<FancyButton ref={ref}>Click me!</FancyButton>;
```

### 使用 Refs 访问 DOM 元素

```javascript
import React, { useRef, useEffect } from "react";

function FocusInput() {
  const inputRef = useRef(null);

  useEffect(() => {
    // Focus the input element when the component mounts
    inputRef.current.focus();
  }, []);

  return <input ref={inputRef} type="text" />;
}

export default FocusInput;
```
注意：Refs 通常用于直接访问和操作 DOM 元素。这是一个使用 ref 来聚焦输入元素的示例。

### 使用 Refs 管理焦点

```javascript
import React, { useRef } from "react";

function Form() {
  const firstInputRef = useRef(null);
  const secondInputRef = useRef(null);

  const handleKeyDown = (e) => {
    if (e.key === "Enter") {
      secondInputRef.current.focus();
    }
  };

  return (
    <div>
      <input ref={firstInputRef} type="text" onKeyDown={handleKeyDown} />
      <input ref={secondInputRef} type="text" />
    </div>
  );
}

export default Form;
```
注意：你也可以使用 refs 来管理多个元素之间的焦点。
