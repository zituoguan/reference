---
title: Flask  
date: 2025-06-07 19:05:00  
background: bg-[#3598db]  
tags:
    - web
    - python
    - backend
categories:
    - 编程
intro: |
    一份 Flask 的简明速查表，Flask 是一个轻量级的 Python WSGI Web 应用框架。
plugins:
    - copyCode
---

## 快速入门 {.cols-3}

### 安装 Flask

```bash
pip install flask
```

### Hello World

```python
from flask import Flask
app = Flask(__name__)

@app.route("/")
def hello():
        return "Hello, World!"

app.run(debug=True)
```

### Flask CLI

```bash
export FLASK_APP=app.py
flask run
```



## 应用配置与环境 {.cols-3}

### 应用对象

```python
from flask import Flask
app = Flask(__name__)
```

### 配置

```python
app.config["DEBUG"] = True
app.config.from_pyfile("config.py")
```

### 常用配置项

| 键          | 描述          |
|  | -- |
| `DEBUG`      | 启用调试模式    |
| `SECRET_KEY` | 用于会话/Cookies |
| `ENV`        | 设置为 'development' |



## 路由与方法 {.cols-3}

### 基本路由

```python
@app.route("/")
def home():
        return "Home"
```

### 方法

```python
@app.route("/login", methods=["GET", "POST"])
def login():
        return "Login"
```

### 动态路由

```python
@app.route("/user/<name>")
def user(name):
        return f"User: {name}"
```



## 请求与响应 {.cols-3}

### 请求对象

```python
from flask import request

@app.route("/data", methods=["POST"])
def data():
        return request.json
```

### 请求属性

* `request.args`: 查询参数
* `request.form`: 表单数据
* `request.json`: JSON 主体

### 自定义响应

```python
from flask import make_response

@app.route("/custom")
def custom():
        res = make_response("Custom", 200)
        res.headers["X-Test"] = "True"
        return res
```



## 模板与静态文件 {.cols-3}

### 渲染模板

```python
from flask import render_template

@app.route("/")
def page():
        return render_template("index.html", name="Flask")
```

### Jinja 语法

```html
<h1>Hello {{ name }}</h1>
{% if name %}<p>Hi!</p>{% endif %}
```

### 静态文件

```html
<link href="{{ url_for('static', filename='style.css') }}">
```



## 会话与 Cookies {.cols-2}

### 使用会话

```python
from flask import session
app.secret_key = "secret"

@app.route("/login")
def login():
        session["user"] = "admin"
        return "Logged in"
```

### 访问 Cookies

```python
from flask import request, make_response

@app.route("/cookie")
def cookie():
        resp = make_response("Set cookie")
        resp.set_cookie("site", "Flask")
        return resp
```



## JSON API 与中间件 {.cols-2}

### JSON 响应

```python
from flask import jsonify

@app.route("/api")
def api():
        return jsonify(message="Hello")
```

### 中间件

```python
@app.before_request
def before():
        print("Before")

@app.after_request
def after(res):
        print("After")
        return res
```



## 错误处理与蓝图 {.cols-2}

### 错误处理

```python
@app.errorhandler(404)
def not_found(e):
        return "Page not found", 404
```

### 蓝图

```python
from flask import Blueprint

admin = Blueprint("admin", __name__, url_prefix="/admin")

@admin.route("/")
def dash():
        return "Admin"

app.register_blueprint(admin)
```



## 项目结构 {.cols-2}

### 文件结构

```bash
project/
├── app.py
├── templates/
│   └── index.html
├── static/
│   └── style.css
└── config.py
```

### 运行服务器

```bash
python app.py
# 或使用 CLI
export FLASK_APP=app.py
flask run
```

