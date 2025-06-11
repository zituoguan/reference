---
title: FastAPI  
date: 2025-06-07 18:40:00  
background: bg-[#059669]  
tags:
    - web
    - python
    - backend
categories:
    - 编程
intro: |
    一个 FastAPI 的简明速查表，FastAPI 是一个用于构建 API 的快速、现代的 Web 框架，使用 Python 3.7+。
plugins:
    - copyCode
---

## 快速入门 {.cols-3}

### 安装与运行

```bash
pip install fastapi uvicorn
uvicorn main:app --reload
```

### Hello World

```python
from fastapi import FastAPI
app = FastAPI()

@app.get("/")
def root():
        return {"message": "Hello FastAPI"}
```

### CLI 运行提示

```bash
uvicorn main:app --reload
```



## 路由与参数 {.cols-3}

### 路径参数

```python
@app.get("/items/{id}")
def read(id: int):
        return {"id": id}
```

### 查询参数

```python
@app.get("/search")
def find(q: str = "default"):
        return {"q": q}
```

### 可选查询参数

```python
@app.get("/filter")
def filter_data(limit: int = 10, active: bool = True):
        return {"limit": limit, "active": active}
```



## 请求体与验证 {.cols-3}

### 使用 Pydantic

```python
from pydantic import BaseModel

class Item(BaseModel):
        name: str
        price: float
```

### JSON 请求体

```python
@app.post("/items/")
def create(item: Item):
        return item
```

### 响应模型

```python
@app.post("/items/", response_model=Item)
def create(item: Item):
        return item
```



## 表单、文件、请求头 {.cols-3}

### 表单输入

```python
from fastapi import Form

@app.post("/login")
def login(user: str = Form(...)):
        return {"user": user}
```

### 文件上传

```python
from fastapi import UploadFile, File

@app.post("/upload")
def upload(f: UploadFile = File(...)):
        return {"filename": f.filename}
```

### 请求头 / Cookies

```python
from fastapi import Header, Cookie

@app.get("/info")
def info(ua: str = Header(None)):
        return {"UA": ua}
```



## 中间件与依赖注入 {.cols-2}

### 中间件

```python
@app.middleware("http")
async def log_req(req, call_next):
        res = await call_next(req)
        return res
```

### 依赖注入

```python
from fastapi import Depends

def auth(token: str = ""):
        if token != "xyz": raise HTTPException(401)
        return True

@app.get("/secure")
def secure(_: bool = Depends(auth)):
        return {"secure": True}
```



## 错误处理与 JSON API {.cols-2}

### HTTP 错误

```python
from fastapi import HTTPException

@app.get("/err")
def error():
        raise HTTPException(404, "Not Found")
```

### JSON API

```python
from fastapi import FastAPI

@app.get("/json")
def get_data():
        return {"status": "ok"}
```



## 模板与静态文件 {.cols-2}

### 挂载静态文件

```python
from fastapi.staticfiles import StaticFiles
app.mount("/static", StaticFiles(directory="static"), name="static")
```

### Jinja2 支持

```python
from fastapi.templating import Jinja2Templates
templates = Jinja2Templates("templates")
```



## 路由与项目结构 {.cols-2}

### 路由 (蓝图)

```python
from fastapi import APIRouter
router = APIRouter()

@router.get("/")
def admin():
        return {"admin": True}

app.include_router(router, prefix="/admin")
```

### 文件夹布局

```bash
project/
├── main.py
├── static/
├── templates/
├── routers/
│   └── admin.py
└── models/
```



## 文档与状态码 {.cols-2}

### 内置文档

* Swagger: `/docs`
* ReDoc: `/redoc`

### 自定义状态码

```python
from fastapi import status

@app.post("/create", status_code=status.HTTP_201_CREATED)
def create():
        return {"msg": "Created"}
```


