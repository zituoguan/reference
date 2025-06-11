---
title: Django
date: 2024-05-15 10:12:25
background: bg-[#214a35]
label: Python
tags:
    - python
    - web
categories:
    - 编程
intro: |
    一份 Django 速查表。
plugins:
    - copyCode
---

## 入门指南

### 启动一个新的 Django 项目

{.row-span-2}

```python
# 创建并访问项目文件夹
~$  mkdir project_name
~$  cd project_name

# 创建 Python 虚拟环境
~$  python3 -m venv venv

# 激活虚拟环境
~$  source venv/bin/activate

# 如果你想停用虚拟环境
~$  deactivate

# 安装 django (~= 等同于 4.2.*)
~$  pip install django~=4.2.0

# 新建 django 项目 (在 project_name 文件夹内)
~$  django-admin startproject config

# 创建应用 (在 project_name 文件夹内)
~$  python manage.py startapp app_name
```

### 数据库迁移 (Migration):

<small>Django 使用这些命令为应用中存在的每个模型创建数据库表：</small>

Makemigrations: 在 app_name/migrations 目录下创建一个文件，其中包含要创建的数据库结构。

```python
~$  python manage.py makemigrations
```

Migrate: 将读取迁移文件并创建实际的数据库和表。

```python
~$  python manage.py migrate
```

### 为认证/管理面板创建超级用户

```python
~$  python manage.py createsuperuser
```

### 启动服务器

```python
~$  python manage.py runserver  => 例如 http://127.0.0.1:8000
```

### 依赖管理 (Requirements)

```python
# 创建一个包含所有项目依赖的 requirements 文件
~$  pip freeze > requirements.txt

# 安装项目依赖 (如果 requirements 文件存在)
~$  pip install -r requirements.txt
```

### 其他命令

```python
# Django shell (直接运行项目代码)
~$ python manage.py shell

# 在 shell 中运行的代码示例:
 >>> from app_name.models import User
 >>> user1 = User.objects.first()

# 为生产环境准备静态文件夹
~$ python manage.py collectstatic

# 从应用 blog 中获取所有数据并导出为 json
~$ python manage.py dumpdata blog > myapp.json

# 将 json 文件中的所有数据导入到应用数据表中
~$ python manage.py loaddata myapp.json

# 创建或更新翻译的消息文件，运行此命令
~$ django-admin makemessages -l de
# 更新消息文件
~$ django-admin compilemessages
```

## 项目配置 {.cols-1}

### 配置设置

##### 项目基础模板目录和应用模板目录：

- 创建文件夹 project/templates
- 创建文件夹 appfolder/templates/appname

##### 在基础根目录和应用中分别创建静态文件夹：

- project_name\static\root
- app_name\static\app_name

```python
# 将应用添加到 settings.py
INSTALLED_APPS = [
                 … ,
                 'app_name.apps.App_nameConfig',
 ]

# 模板目录配置
# 项目模板 settings.py:
        TEMPLATES = [
                { …
                     'DIRS': [BASE_DIR / 'templates'],
                … }

# 静态文件夹:
STATIC_URL = '/static/'
STATICFILES_DIRS = [ BASE_DIR / 'static' ]
STATIC_ROOT = 'static_root'
# 媒体文件夹:
MEDIA_URL = '/media/'
STATICFILES_DIRS = (
        (BASE_DIR / 'static'),
)
MEDIA_ROOT = BASE_DIR / 'media'

# 使用 PostgresSQL
# pip install psycopg2
# settings.py
DATABASE = {
        'default': {
                'ENGINE': 'django.db.backends.postgresql',
                'NAME': 'blog',
                'USER': 'admin',
                'PASSWORD': '123456',
                'HOST': 'localhost',
                'PORT': '5432'
                }
        }

TIME_INPUT_FORMATS = [
        '%H:%M:%S',     # '14:30:59'
        '%H:%M',        # '14:30'
]

DATE_FORMAT = "Y/M/d"

# 翻译区域设置
LANGUAGES = [
        ('en', 'English'), # 英语
        ('de', 'German'),  # 德语
]

LOCALE_PATHS = (
        BASE_DIR / 'locale',
)

# CK Editor 配置
CKEDITOR_UPLOAD_PATH = 'uploads/'
CKEDITOR_RESTRICT_BY_USER = True
CKEDITOR_BROWSE_SHOW_DIRS = True
CKEDITOR_ALLOW_NONIMGE_FILES = True
CKEDITOR_IMAGE_BACKEND = "pillow"
CKEDITOR_CONFIGS = {
        'default': {
                'toolbar': 'full',
        }}

# SSL
# 如果你有 SSL 证书
SECURE_SSL_REDIRECT = True
# cookies 将仅通过 HTTPS 连接发送
SESSION_COOKIE_SECURE = True
CSRF_COOKIE_SECURE = True
```

## 数据模型

### 创建数据模型 {.col-span-2}

<small>这些模型可以通过迁移命令创建为数据库表</small>

```python
# models.py
# id 字段由 Django 自动为每个模型创建，因此下面未显示
from django.db import models

class Customer(models.Model)
        name = models.Charfield('Customer', max_length=120) # 客户
        age = models.IntegerField() # 年龄
        note = models.TextField(blank=True, null = True) # 备注
        email = models.EmailField(max_length=255, blank=True, null=True) # 邮箱
        credit = models.FloatField(blank=True) # 信用额度
        is_active = models.BooleanField(default=True) # 是否激活
        created_at = models.DateTimeField(auto_now_add=True) # 创建时间
        updated_at = models.DateTimeField(auto_now=True) # 更新时间
        img = models.ImageField(upload_to ='uploads/') # 图片
        # 选择字段 (返回的值, 显示的值)
        TYPE_CHOICES = (
                ('Customer', _('Customer')), # 客户
                ('Supplier', _('Supplier')), # 供应商
                ('Student', _('Student')),   # 学生
        )
        type = models.CharField(choices=TYPE_CHOICES) # 类型

        class Meta:
                verbose_name = "Customer" # 客户
                verbose_name_plural = "Customers" # 客户 (复数)

        # 模型的字符串表示
        def __str__(self):
                return self.name

        # 指向网站上资源或页面的 URL
        def get_absolute_url(self):
                return reverse("customer_detail", kwargs={"pk": self.pk})
```

#### 我们也可以使用此方法定义 ChoiceField 的值。

```python
    class Customer(models.Model)
        class TypeList(models.IntegerChoices):
                customer = (1, _('Customer')) # 客户
                supplier = (2, _('Supplier')) # 供应商
                student = (3, _('Student'))   # 学生
        .
        .
        .
        type = models.CharField(choices=TypeList.choices, default=1)
```

#### 要在模板中访问 ChoiceField 的值，我们需要在模板中执行以下操作：

- 在 Django 模板中，您可以使用 "`get_FOO_display()`" 方法，该方法将返回字段的可读别名，其中 `'FOO'` 是字段的名称。
- 如果选项存储在变量 `CHOICES` 中，并且存储所选选项的模型字段是 `'type'`，那么您可以直接使用

```html
<!-- 这里，X 是模型实例 -->
{{ X.get_type_display }}

<!-- 您甚至可以使用此方法显示其翻译。 -->
{% trans X.get_type_display %}
```

#### 模型之间的关系

```python
# 一对多：(如果实体尚未声明，请使用双引号) 例如 "Supplier"
supplier = models.ForeignKey(Supplier, blank=True, null=True, on_delete=models.CASCADE,related_name="supplierother")

# on_delete 可以设置为 models.CASCADE, models.SET_DEFAULT 或 models.SET_NULL
# related_name 属性指定从 supplier 模型返回到您的模型的反向关系的名称

# 多对多：
tags = models.ManyToManyField(Tag, blank=True)

# 一对一
User = models.OneToOneField(User, on_delete=models.CASCADE)

# 覆盖 save 方法
def save(self, (*args, **kwargs):
        if not self.slug:
                self.slug = slugify(self.title)
        super().save(*args, **kwargs)
```

## 查询 (Lookup)

### 字段查询 {.col-span-2}

在 Django 中，`field__lookuptype` 语法用于在查询中对字段执行查找。`field` 表示要执行查找的字段名称，`lookuptype` 表示要执行的查找类型。

例如，假设您有一个名为 `Book` 的模型，其中有一个名为 `title` 的字段。您可以使用 `field__lookuptype` 语法对 `title` 字段执行不同类型的查找。

以下是一些示例：

```python

# 1. 精确匹配查询:
Book.objects.filter(title__exact='Python Tricks')
# 2. 不区分大小写查询:
Book.objects.filter(title__iexact='python tricks')
# 3. 包含查询:
Book.objects.filter(title__contains='Python')
# 4. 以...开头查询:
Book.objects.filter(title__startswith='Python')
# 5. 以...结尾查询:
Book.objects.filter(title__endswith='Tricks')
```

### 字段查询参考

| 关键字         | 描述                                       |
| -------------- | :----------------------------------------------- |
| `contains`     | 包含短语                                     |
| `icontains`    | 与 contains 相同，但不区分大小写             |
| `date`         | 匹配日期                                     |
| `day`          | 匹配日期 (月份中的天，1-31) (用于日期)        |
| `endswith`     | 以...结尾                                      |
| `iendswith`    | 与 endswith 相同，但不区分大小写             |
| `exact`        | 精确匹配                                     |
| `iexact`       | 与 exact 相同，但不区分大小写                |
| `in`           | 匹配其中一个值                                 |
| `isnull`       | 匹配 NULL 值                                  |
| `gt`           | 大于                                         |
| `gte`          | 大于或等于                                   |
| `hour`         | 匹配小时 (用于日期时间)                        |
| `lt`           | 小于                                         |
| `lte`          | 小于或等于                                   |
| `minute`       | 匹配分钟 (用于日期时间)                        |
| `month`        | 匹配月份 (用于日期)                            |
| `quarter`      | 匹配年份的季度 (1-4) (用于日期)                |
| `range`        | 匹配范围                                     |
| `regex`        | 匹配正则表达式                               |
| `iregex`       | 与 regex 相同，但不区分大小写                |
| `second`       | 匹配秒 (用于日期时间)                          |
| `startswith`   | 以...开头                                      |
| `istartswith`  | 与 startswith 相同，但不区分大小写           |
| `time`         | 匹配时间 (用于日期时间)                        |
| `week`         | 匹配周数 (1-53) (用于日期)                     |
| `week_day`     | 匹配星期几 (1-7) 1 是星期日                  |
| `iso_week_day` | 匹配 ISO 8601 星期几 (1-7) 1 是星期一        |
| `year`         | 匹配年份 (用于日期)                            |
| `iso_year`     | 匹配 ISO 8601 年份 (用于日期)                  |

### 管理面板 {.col-span-2}

每个 Django 项目都带有一个管理面板，可以通过 /admin URL 打开 (例如：localhost:8000/admin)<br> 要在管理面板中显示模型，请在 app_name/admin.py 文件中注册模型<br> 对于每个模型，您可以指定要使用的字段</small>

```python
from django.contrib import admin
from app_name.models import Blog

# 自定义模型管理 (admin.py):
@admin.register(Blog)   # 注册应用
class BlogAdmin(admin.ModelAdmin)
        fields = ("title", "description") # 用于添加/编辑/显示页面的字段
        list_display = ("title", "description") # 在搜索页面中显示的字段
        list_display_links = ("title",) # 在搜索页面中将作为链接的字段
        ordering = ("date_created",) # 搜索页面中允许的排序
        search_fields = ("title", "description") # 搜索页面中允许的搜索字段
        list_filter =("title",) # 定义出现在右侧边栏的列表过滤器
```

### 路由

Django 路由信息存储在 project_folder/urls.py 文件中

```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
        path('admin/', admin.site.urls), # 预先创建的管理 URL 路由
        path('', include('app_name.urls')) # 包含您的应用 URL
]
```

`include()` 方法允许链接到在您的应用文件夹中创建的另一个 urls.py 文件 (app_name/urls.py)

```python
from django.urls import path
from app_name import views

urlpatterns = [
        path('posts', views.index, name='posts.index'),
        path('posts/create/', views.create, name='posts.create'),
        path('posts/<int:id>/', views.show, name='posts.show'),
        path('posts/<int:id>/edit/', views.edit, name='posts.edit'),
        path('posts/<int:id>/delete/', views.delete, name='posts.delete'),
        path('posts/<int:id>/<int:state>/', views.status, name='posts.status'), # 两个参数
]
```

## 静态路由和自定义管理面板 {.cols-1}

### 自定义管理面板

管理面板的页眉和标题 & 自定义 `404`、`500` 和 `503` 模板

```python
# 添加到 project/urls.py
from django.contrib import admin
from django.conf import settings
from django.conf.urls.static import static

urlpatterns = [  ...  ]

if settings.DEBUG == True:
        urlpatterns += static(settings.STATIC_URL, document_root=settings.STATIC_ROOT)
        urlpatterns += static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)

# 自定义管理面板页眉和标题
admin.site.site_header = _('Administrator Control Panel') # 管理员控制面板
admin.site.site_title = _('Administrator Control Panel')  # 管理员控制面板
admin.site.index_title = _('Wellcome to Control Panel') # 欢迎来到控制面板

# 自定义 404 模板页面
handler404 = 'app_name.views.handler404'
handler500 = 'app_name.views.handler500'
handler503 = 'app_name.views.handler503'
```

## 视图 (Views) {.cols-1}

### 基于函数的视图

```python
# views.py
from django.shortcuts import render, redirect
from app_name.models import Post
from app_name.forms import PostForm

def index(request):
        # 获取所有帖子
        posts = Post.objects.all()

        # 使用上下文渲染应用模板
        return render(request, 'appfolder/index.html', {'posts': posts})

def show(request, id):
        post = Post.objects.get(id=id)
        return render(request, 'appfolder/show.html', {'post': post})

def create(request):
        form = PostForm(request.POST or None, request.FILES or None)
        # 当表单包含图像或文件字段时，我们应该使用 request.FILES
        if form.is_valid():
                # 可选地，我们可以使用 form.cleaned_data['first_name'] 访问表单数据
                post = form.save(commit=False)
                post.user = request.user
                post.save()
                return redirect('/posts')

        return render(request, 'appfolder/create.html', {'form': form})

def edit(request, id):
        post = Post.objects.get(id=id)
        form = PostForm(request.POST or None, request.FILES or None, instance=post)
        if form.is_valid():
                form.save()
                return redirect('/posts')

        return render(request, 'appfolder/edit.html', {'form': form})

def delete(request, id):
        post = Post.objects.get(id=id)
        post.delete()
        return redirect('/posts')

def status(request, id, state):
        post = Post.objects.get(id=id, state=state)
        return redirect('appfolder/status.html', {'post': post})
```

### 基于类的视图

```python
from django.views.generic import TemplateView, ListView, DetailView, CreateView, UpdateView, DeleteView

class LandingPageView(TemplateView):
        template_name = 'landing.html'

        # 可选：更改上下文数据字典
        def get_context_data(self, **kwargs):
                context = super().get_context_data(**kwargs)
                context['title'] = 'Landing Page' # 着陆页
                return context


class PostsListView(ListView):
        queryset = Post.objects.all()
        # 可选
        # context_object_name = "posts" (默认: post_list)
        # template_name = 'posts.html' (默认: posts/post_list.html)


class PostsDetailView(DetailView):
        model = Post # 模板中的对象变量
        # 可选
        # template_name = 'post.html' (默认: posts/post_detail.html)


class PostsCreateView(CreateView):
        form_class = PostForm
        template_name = 'posts/post_create.html' # 没有默认值

        def get_success_url(self):
                return reverse('posts-list')

        # 可选：覆盖表单数据 (保存前)
        def form_valid(self, form):
                if self.request.user.is_authenticated:
                        form.instance.author = self.request.user # 注意：这里原文是 from.instance.author，应该是 form.instance.author
                return super().form_valid(form)


class PostsUpdateView(UpdateView):
        model = Post
        form_class = PostForm
        template_name = 'posts/post_update.html'

        def get_success_url(self):
                return reverse('post-list')

        # 可选：更改上下文数据字典
        def get_context_data(self, **kwargs):
                context = super().get_context_data(**kwargs)
                context['submit_text'] = 'Update' # 更新
                return context


class PostsDeleteView(DeleteView):
        model = Post
        template_name = 'posts/post_delete.html'
        success_url = reverse_lazy('posts-list')

# Urls.py 路由声明
path('<int:pk>/update/', PostsUpdateView.as_view(), name='post-update')
```

## 模板 (Templates)

### 基本模板

模板存储在 `project_folder/templates` 或您的 <code>app_folder/templates/app_name/\*.html</code> 中

```html
<!-- 继承自另一个模板 -->
<!-- 可以为不同的模板使用 HTML 的相同部分 -->
{% extends 'base.html' %}

<!-- 父模板中定义的一部分，在子模板中被替换 -->
{% block contents %} {% endblock contents %}

<!-- 包含模板 -->
{% include 'partials/header.html' %}
<!-- 包含带有一个或多个参数的模板 -->
{% include 'body.html' with key1=value1 key2=value2 %}

<!-- 模板中的 If 语句 -->
{% if user.username = 'Mike' %}
<p>你好管理员</p>
{% elif user.username = 'john' %}
<p>你好 John Doe</p>
{% else %}
<p>你好用户</p>
{% endif %}

<!-- 模板中的 for 循环 -->
{% for product in products %}
<p>行: {{ forloop.counter }} # 起始索引 1 {{ forloop.counter0 }} # 起始索引 0</p>
<p>产品名称是 {{ product.name }}</p>
<p></p>
<p>产品价格是 {{ product.price }}</p>
<p>
    {% endfor %}

    <!-- 访问模板中的变量 -->
    {{ var_name }}

    <!-- 模板变量格式化 -->
    {{ title | lower }} {{ blog.post | truncatewords:50 }} {{ order.date | date:"D M Y" }} {{ list_items | slice:":3" }} {{
    total | default:"nil" }}

    <!-- 当前路径 (例如 posts/1/show) -->
    {{ request.path }}

    <!-- 按名称生成带参数的 URL -->
    {% url 'posts.delete' id=post.id %}

    <!-- 在模板中使用 static： -->
    {% load static %} {% static 'css/main.css' %}

    <!-- 在模板中定义变量 -->
    {% with name="World" %}
    <html>
        <div>你好 {{ name }}!</div>
    </html>
    {% endwith %}

    <!-- 模板翻译文本 -->
    {% load i18n %}
    <title>{% trans "This is the title." %}</title> <!-- 这是标题。 -->
    <!-- 在模板中使用变量翻译 -->
    <title>{% trans object.title %}</title>

    <!-- 在模板中定义列表 -->
    <input type="number" {% if product.unit in 'kg,milligram,milliliter' %} step="0.01" {% else %} step="1" {% endif %}>

    <!-- 在 Django 模板中安全地将数据传递给 JavaScript： -->
    <!--+ 对于简单值使用 data 属性 -->
    <script data-username="{{ username }}">
        const data = document.currentScript.dataset;
        const username = data.username;
    </script>

    <!-- + 单独的脚本文件：对于单独的脚本文件可以使用 document.currentScript -->
    <script src="{% static 'index.js' %}" data-username="{{ username }}"></script>

    <!-- + 大小写转换 -->
    <script src="{% static 'index.js' %}" data-full-name="{{ full_name }}"></script>
    <!--  在 JavaScript 中以 fullName 读取： -->
    <script>
        const data = document.currentScript.dataset;
        const fullName = data.fullName;
    </script>

    <!-- + 非字符串类型 -->
    <script src="{% static 'index.js' %}" data-follower-count="{{ follower_count }}"></script>

    <!--  使用 parseInt() 将此值从字符串转换： -->
    <script>
        const data = document.currentScript.dataset;
        const followerCount = parseInt(data.followerCount, 10);
    </script>

    <!-- + 没有限制：一个 <script> 可以有任意数量的 data 属性： -->
    <script
        src="{% static 'index.js' %}"
        defer
        data-settings-url="{% url 'settings' %}"
        data-configuration-url="{% url 'configuration' %}"
        data-options-url="{% url 'options' %}"
        data-preferences-url="{% url 'preferences' %}"
        data-setup-url="{% url 'setup' %}"
    ></script>
</p>
```

### 自定义模板标签和过滤器

例如，如果您的自定义标签/过滤器位于名为 `basetags.py` 的文件中，您的应用布局可能如下所示：

```
app_name/
└─── templatetags/
         └─── basetags.py
         __init__.py
         models.py
         views.py
```

- 在您的模板中，您将使用以下内容：

```html
{% load basetags %}
```

- 该模块必须包含一个名为 `register` 的模块级变量，它是一个 `template.Library` 实例，所有标签和过滤器都在其中注册。因此，在模块的顶部附近，放置以下内容：

### 编写自定义模板过滤器

自定义过滤器是接受一个或两个参数的 Python 函数：变量的值 (输入) – 不一定是字符串。参数的值 – 这可以有一个默认值，或者完全省略。例如，在过滤器 `{{ var|foo:"bar" }}` 中，过滤器 `foo` 将传递变量 `var` 和参数 `"bar"`。

`Library.filter()` 方法接受两个参数：过滤器的名称 – 一个字符串。编译函数 – 一个 Python 函数 (而不是作为字符串的函数名称)。您可以改用 `register.filter()` 作为装饰器：

```python
# basetags.py
from django import template

register = template.Library()

@register.filter(name="cut")
def cut(value, arg):
        """从给定字符串中移除所有 arg 的值"""
        return value.replace(arg, "")

# 大多数过滤器不接受参数。在这种情况下，请从函数中省略参数
@register.filter()
def lower(value): # 只有一个参数。
        """将字符串转换为全小写"""
        return value.lower()


@register.simple_tag
def to_class_name(object):
        return str(object.__class__.__name__)

# 模板
# 以下是如何在模板中使用该过滤器的示例：
{{ somevariable | cut:"0" }}

# 将 simple tag 的结果放入变量中
{% to_class_name object as objectmodel %}
<p>模型类名: {{ objectmodel }}</p>
```

## 上下文处理器 (Context Processor) {.cols-1}

### 创建自定义上下文处理器

在任何地方创建一个 `context_processors.py` 文件

```
project_name
└───app_name
        ├───...
        └───context_processors.py
```

在 `context_processors.py` 中创建一个函数，该函数接受一个 `HttpRequest` 对象作为参数并返回一个字典。

上下文处理器只是一个接受 `HttpRequest` 对象作为参数并返回字典的函数。像这样：

```python
# app_name/context_processors.py
def site_email(request):
        return { 'site_email' : 'example@gmail.com' }
```

3. 将此添加到 `settings.py` 中的 `context_processors` 设置中 (出于安全原因，放在底部)

```python
 TEMPLATES = [
        { …
                'OPTIONS': {
                    'context_processors': [
                        …
                            'app_name.context_processors.site_email',
                            # 新的上下文处理器在这里
                        …
                    ],
        … },

# 现在可以在整个站点的每个 Django 模板中访问 'site_email' 模板变量。
```

## 模型管理器和查询集 (Querysets)

### 模型管理器

模型管理器允许模型数据库的读写操作

```python
# 一行创建并保存
Article.objects.create(name='Item 1', price=19.95)

# 读取所有
Article.objects.all()

# 创建
user = User.objects.first()
article = Article(user=user, name='Item 1', price=19.95)

# 保存
article.save()

# 读取一个
Article.objects.get(id=1)

# Select Related (避免 n+1 查询)
posts = Post.objects.select_related('user', 'category').all()

# 读取或渲染 404 未找到页面
from django.shortcuts import get_object_or_404
article = get_object_or_404(Article, id=512)

# 过滤
Article.objects.filter(model='dyson', name__icontains='dyson') # __icontains 不区分大小写包含
Article.objects.filter(year__gt=2016) # __gt = 大于
Article.objects.filter(year__lt=2001) # __lt = 小于

# 根据关系子模型字段过滤
Article.objects.get(user__username='mike')

# 排序
Article.objects.order_by('name')     # 升序
Article.objects.order_by('-name')   # 降序

# 切片返回第一个
Article.objects.all().order_by('name')[0]

# 切片返回最后一个
Article.objects.all().order_by('-name')[0]

# 切片限制/偏移
Article.objects.all().order_by('name')[1:10] # 原文是 1..10，Python 切片语法是 [1:10]

# 更新
article = Article.objects.first()
article.name = 'new name'
article.save()

# 一行更新
Article.objects.filter(id=4).update(name='new name')

# 删除
article = Article.objects.first()
article.delete()

# 一行删除
Article.objects.get(id=1).delete() # 原文是 article.objects.get(id=1).delete()，应该是 Article.objects.get(id=1).delete()

# 删除所有
Article.objects.all().delete()

# 设置外键字段值
model1 = Model(name='dyson')
article.model = model1

# 获取外键值
article1.model.name
model1.article_set.all()

# 添加多对多关系
article1.tags.add(tag1)
article1.tags.all()
tag1.article_set.all() # 原文是 tag1.articles_set.all()，Django 默认反向名称是 modelname_set
```

## 表单 (Form)

### 表单创建 {.col-span-2}

在 HTML 中，表单是 `<form>...</form>` 内的一组元素，允许访问者执行诸如输入文本、选择选项、操作对象或控件等操作，然后将该信息发送回服务器。

```python
# app_name/forms.py
from django import forms
class ArticleForm(forms.Form):
        name = forms.CharField(max_length=100) # 名称，原文 Charfield，应为 CharField
        description = forms.CharField(blank=True, null = True) # 描述，原文 Charfield，应为 CharField


# 模型表单
from django.forms import ModelForm
from app_name.models import Article
class ArticleForm(ModelForm):
        class Meta:
                model = Article
                fields = ['name', 'description', 'price'] # 使用 '__all__' 表示所有字段
                widgets = {
                        'name': forms.TextInput(attrs={'class': 'form-control'}),
                }
                labels = {
                        'name': 'First Name', # 姓
                }
                error_messages = {
                        'name': {'required': 'This field is required',}, # 此字段是必填项
                        }
                help_texts = {
                'name': 'Enter Your First Name', # 输入您的姓
                }
```

```html
<!-- 在模板中渲染表单 -->
<form method="post" action="" novalidate> <!-- 原文 method="“post”" action="“”" -->
    {% csrf_token %} {{ form }}
    <button type="submit">提交</button>
</form>
```

- 注意：如果表单包含文件字段，您的表单必须包含 `enctype="multipart/form-data"`，例如：

```html
<form action="" method="post" enctype="multipart/form-data">
        {% csrf_token %}
        {{ form.as_p }}
        <button type="submit">{% trans 'Submit' %}</button> <!-- 提交 -->
</form>
```

##### 一个用于优秀的 django-crispy-forms 的 Tailwind CSS 模板包。

```bash
pip install crispy-tailwind
```

```python
# settings.py
INSTALLED_APPS = (
        ...
        "crispy_forms",
        "crispy_tailwind",
        ...
)
CRISPY_ALLOWED_TEMPLATE_PACKS = 'tailwind'
CRISPY_TEMPLATE_PACK = 'tailwind'
```

```html
<!-- 模板用法 -->
{% load tailwind_filters %} {{ form|crispy }}
```

### 表单验证

```python
# forms.py
from django.core.exceptions import ValidationError

# 字段验证
def clean_first_name(self):
        data = self.cleaned_data['first_name']
        if data == 'Mike': # 原文 data = 'Mike'，应为 data == 'Mike'
                raise ValidationError('Your name must not be Mike') # 您的名字不能是 Mike
        return data

# 表单验证
def clean(self):
        first_name = self.cleaned_data['first_name']
        last_name = self.cleaned_data['last_name']
        if first_name + last_name == 'MikeTaylor': # 原文 first_name + last_name = 'MikeTaylor'，应为 ==
                raise ValidationError('Your name must not be Mike Taylor') # 您的名字不能是 Mike Taylor
```

## Flash 消息 {.cols-1}

### 显示消息

```python
# 消息标签
# debug, info, success, warning 和 error

messages.success(request, 'Login successful') # 登录成功
messages.error(request, 'Login error')       # 登录错误
```

```html
<!-- 在模板中显示 flash 消息 -->
{% if messages %}
    {% for message in messages %}
        <div class="alert alert-{{ message.tags }}"> <!-- 原文 {% message %} {% message.tags %}，通常这样使用 -->
            {{ message }}
        </div>
    {% endfor %}
{% endif %}
```

## 用户模型

### 预创建

用户模型 (预创建)

```python
# 获取对 Django 预创建用户模型的引用
from django.contrib.auth import get_user_model

User = get_user_model()

# 或者如果您想自定义用户模型
from django.contrib.auth.models import AbstractUser

class User(AbstractUser):
        # 添加自定义字段和方法
        pass # 原文没有 pass，添加以使其成为有效的类定义

# 要让 Django 使用该模型，请转到 settings.py 并添加：AUTH_USER_MODEL = 'app_name.User'
```

## 认证 (Authentication)

### 认证：LoginView

```python
# LoginView 已由 Django 预创建
from django.contrib.auth.views import LoginView

# 添加一个 URL 以访问该视图
path('login/', LoginView.as_view(), name='login')

# 默认情况下，LoginView 将尝试打开名为 'registration/login.html' 的模板并向其发送登录表单。
```

```html
<!-- 在 registration/login.html 下创建模板 -->
{% extends "base.html" %} {% block content %}
<form method="post">
    {% csrf_token %} {{ form }}
    <button type="submit">登录</button>
</form>
{% endblock content %}

<!-- 当用户单击“登录”按钮时，LoginView 将尝试使用表单中的用户名和密码对用户进行身份验证 -->

<!-- 如果成功，它将登录用户并重定向到 settings.py 中指定的 LOGIN_REDIRECT_URL -->
```

#### 认证：LogoutView

```python
# LogoutView 已由 Django 预创建
from django.contrib.auth.views import LogoutView

# 添加一个 URL 以访问该视图
path('logout/', LogoutView.as_view(), name='logout') # 原文 LoginView.as_view()，应为 LogoutView.as_view()

# 在模板中包含一个链接
<a href="{% url 'logout' %}">登出</a>

# 链接执行后，用户将被登出并重定向到 settings.py 中指定的 LOGOUT_REDIRECT_URL
```

#### 认证：SignupView

```python
# 创建一个 SignupView (该视图默认未创建)
# 导入 Django 预创建的注册表单
from django.contrib.auth.forms import UserCreationForm
from django.views.generic import CreateView
from django.urls import reverse # 导入 reverse

class SignupView(CreateView):
        template_name = 'registration/signup.html'
        form_class = UserCreationForm

        def get_success_url(self):
                return reverse("login")
```

```html
<!-- 创建模板：registration/signup.html -->
{% extends "base.html" %} {% block content %}
<form method="post">
    {% csrf_token %} {{ form }}
    <button type="submit">注册</button>
</form>
{% endblock content %}
```

```python
# 添加一个 URL 以访问该视图
from posts.views import SignupView # 假设 SignupView 在 posts.views 中

path('signup/', SignupView.as_view(), name='signup')
```

```python
# 可选：自定义 UserCreationForm
# (forms.py)
from django.contrib.auth import get_user_model
from django.contrib.auth.forms import UserCreationForm, UsernameField # 导入 UsernameField

User = get_user_model()
class CustomUserCreationForm(UserCreationForm): # 原文 UserCreattionForm，应为 UserCreationForm
        class Meta:
                model = User
                fields = ['username']
                field_classes = {'username': UsernameField} # 原文 fields_classes，应为 field_classes
```

#### 可选的预创建认证路由

```python
# urls.py
urlpatterns += [path('', include('django.contrib.auth.urls'))] # 原文 urlpatterns += path(...)
# /login, /logout, /signup, 等。
```

#### 模板认证助手

```html
<!-- 认证链接 -->
<a href="{% url 'login' %}">登录</a>
<a href="{% url 'signup' %}">注册</a>
<a href="{% url 'logout' %}">登出</a>

<!-- 检查用户是否登录 -->
{% if request.user.is_authenticated %} 已登录为: {{ request.user.username }} {% endif %}
```

#### 授权：LoginRequiredMixin 和 login_required

```python
from django.contrib.auth.mixins import LoginRequiredMixin
from django.views import generic # 假设 generic 被使用

# 仅限已认证用户访问视图 (views.py)
class PostsCreateView(LoginRequiredMixin, generic.CreateView):
        ...
        ...


from django.contrib.auth.decorators import login_required

@login_required(login_url='/login')
def search_page(request):
        ...
        ...
```

#### 手动认证、登录和登出

```python
from django.contrib.auth import authenticate, login, logout # 导入 logout
from django.shortcuts import redirect, render # 导入 render, redirect

def login_page(request):
        if request.method == "POST":
                username = request.POST.get("username")
                password = request.POST.get("password")
                user = authenticate(request, username=username, password=password)
                if user is not None:
                        login(request, user)
                        return redirect("index") # 假设 "index" 是一个有效的 URL 名称

        return render(request, "registration/login.html", {})


def logout_page(request):
        logout(request)
        return redirect("index") # 假设 "index" 是一个有效的 URL 名称
```

#### 用户更改密码

```python
# set_password 会对密码进行哈希处理
user.set_password('raw password')
```

## 创建自定义账户模型

```python
~$ python manage.py startapp accounts
```

```python
# 将 accounts 应用添加到 settings.py
INSTALLED_APPS = [ … ,
                 'accounts.apps.AccountsConfig',
                    ]
.
.
.
AUTH_USER_MODEL = 'accounts.User'
```

```python
# accounts/models.py
from django.db import models
from django.contrib.auth.models import BaseUserManager, AbstractBaseUser, PermissionsMixin

class UserManager(BaseUserManager):
        def create_user(self, username, email, password=None, **extra_fields):
                if not username:
                        raise ValueError('用户必须有一个用户名')
                if not email:
                        raise ValueError('用户必须有一个邮箱')

                email = self.normalize_email(email) # 添加 email 规范化
                user = self.model(username=username, email=email, **extra_fields) # 确保 username 也被传递
                user.set_password(password)
                user.save(using=self._db)
                return user

        def create_superuser(self, username,  email, password=None, **extra_fields):
                extra_fields.setdefault('is_staff', True)
                extra_fields.setdefault('is_superuser', True)
                extra_fields.setdefault('is_active', True)

                if extra_fields.get('is_staff') is not True: # 确保 is_staff 为 True
                        raise ValueError('超级用户必须设置 is_staff=True。')
                if extra_fields.get('is_superuser') is not True: # 确保 is_superuser 为 True
                        raise ValueError('超级用户必须设置 is_superuser=True。')

                return self.create_user(username, email, password, **extra_fields) # 原文 user.save() 重复，create_user 已保存


class User(AbstractBaseUser, PermissionsMixin):
        username = models.CharField(verbose_name='用户名', max_length=255, unique=True)
        email = models.EmailField(verbose_name='邮箱', max_length=255, unique=True)
        phone = models.BigIntegerField(verbose_name='电话号码', unique=True, blank=True, null=True)
        is_active = models.BooleanField(default=True, verbose_name="是否激活")
        is_staff = models.BooleanField(default=False, verbose_name="是否为员工")
        is_superuser = models.BooleanField(default=False, verbose_name="是否为超级用户")

        objects = UserManager()

        # 我们可以使用任何字段作为用户名
        USERNAME_FIELD = 'username'  # 或 'email' 或 'phone'
        REQUIRED_FIELDS = ['email'] # 如果 USERNAME_FIELD 是 username，则 email 通常是 REQUIRED_FIELDS

        def __str__(self):
                return self.username

        class Meta:
                verbose_name = "用户"
                verbose_name_plural = "用户"
```

```python
# accounts/forms.py
from django import forms
from django.contrib.auth.forms import ReadOnlyPasswordHashField
from django.core.exceptions import ValidationError
from accounts.models import User
from django.utils.translation import gettext_lazy as _


class UserCreationForm(forms.ModelForm):
        password1 = forms.CharField(label='密码', widget=forms.PasswordInput)
        password2 = forms.CharField(label='确认密码', widget=forms.PasswordInput)

        class Meta:
                model = User
                fields = ('username', 'email', 'phone') # 移除了 is_active, is_staff，这些通常不由用户创建时设置

        def clean_password2(self):
                password1 = self.cleaned_data.get("password1")
                password2 = self.cleaned_data.get("password2")
                if password1 and password2 and password1 != password2:
                        raise ValidationError("密码不匹配")
                return password2

        def save(self, commit=True):
                user = super().save(commit=False)
                user.set_password(self.cleaned_data["password1"])
                if commit:
                        user.save()
                return user


class UserChangeForm(forms.ModelForm):
        password = ReadOnlyPasswordHashField(label=_("Password"), help_text=_("Raw passwords are not stored, so there is no way to see this user's password, but you can change the password using <a href=\"../password/\">this form</a>.")) # 添加了 help_text

        class Meta:
                model = User
                fields = ('username', 'email', 'phone', 'password', 'is_active', 'is_staff') # 添加了 password

        def clean_password(self):
                # 不管用户输入什么，都返回初始哈希值。
                # 这可以防止用户意外地将哈希值更改为空字符串。
                return self.initial["password"]


class LoginForm(forms.Form):
        # 原文使用 email 作为登录字段，但模型 USERNAME_FIELD 是 username
        # 这里假设登录也使用 username，如果用 email 登录，User 模型和 authenticate 调用需要相应调整
        username = forms.CharField( # 改为 username
                widget=forms.TextInput(attrs={'class': 'form-control', 'placeholder': '用户名'}), label='用户名') # 改为 用户名
        password = forms.CharField(
                widget=forms.PasswordInput(attrs={'class': 'form-control', 'placeholder': '密码'}),label='密码')


class RegisterForm(forms.ModelForm):
        password1 = forms.CharField(label='密码', widget=forms.PasswordInput(
                attrs={'class': 'form-control'}))
        password2 = forms.CharField(label='确认密码',
                                                                widget=forms.PasswordInput(attrs={'class': 'form-control'}))

        class Meta:
                model = User
                fields = ('username', 'email', 'phone')

                widgets = {  # 可选
                        'username': forms.TextInput(attrs={'class': 'form-control'}),
                        'email': forms.EmailInput(attrs={'class': 'form-control'}),
                        'phone': forms.NumberInput(
                                attrs={'class': 'form-control', 'type': 'tel', # 'maxlength': '11', 'minlength': '11' 通常由模型或前端处理
                                             'onkeypress': 'return isNumber(event)', 'required': 'false'})} # required 属性应为布尔值或省略

        def clean_password2(self):
                password1 = self.cleaned_data.get("password1")
                password2 = self.cleaned_data.get("password2")
                if password1 and password2 and password1 != password2:
                        raise ValidationError("密码不匹配")
                # else: # else 不是必需的
                return password2 # 返回 password2

        def save(self, commit=True):
                user = super().save(commit=False)
                user.set_password(self.cleaned_data["password1"])
                if commit:
                        user.save()
                return user

class EditProfileForm(forms.ModelForm):
        class Meta:
                model = User
                fields = ('username', 'email', 'phone')


class ChangePasswordForm(forms.Form): # 类名更改以更清晰
        password_old = forms.CharField(label=_('旧密码'), widget=forms.PasswordInput( # 添加旧密码字段
                attrs={'class': 'form-control', 'placeholder': '旧密码'}))
        password1 = forms.CharField(label=_('新密码'), widget=forms.PasswordInput(
                attrs={'class': 'form-control', 'placeholder': '新密码'}))
        password2 = forms.CharField(label=_('确认新密码'),
                                                                widget=forms.PasswordInput(
                                                                        attrs={'class': 'form-control', 'placeholder': '再次输入新密码'}))

        def __init__(self, user, *args, **kwargs): # 添加 user 参数
                self.user = user
                super().__init__(*args, **kwargs)

        def clean_password_old(self): # 验证旧密码
                password_old = self.cleaned_data.get("password_old")
                if not self.user.check_password(password_old):
                        raise ValidationError(_("您的旧密码输入不正确。请重新输入。"))
                return password_old

        def clean_password2(self):
                password1 = self.cleaned_data.get("password1")
                password2 = self.cleaned_data.get("password2")
                if password1 and password2 and password1 != password2:
                        raise ValidationError("新密码不匹配")
                return password2

        def save(self, commit=True): # 添加 save 方法
                password = self.cleaned_data["password1"]
                self.user.set_password(password)
                if commit:
                        self.user.save()
                return self.user
```

```python
# accounts/admin.py
from django import forms
from django.contrib import admin
from django.contrib.auth.admin import UserAdmin as BaseUserAdmin
# from django.contrib.auth.forms import ReadOnlyPasswordHashField # 已在 accounts.forms 中导入
from django.core.exceptions import ValidationError
# from django.contrib.auth.models import Group # 如果要取消注册 Group，则需要导入
from accounts.models import User
from .forms import UserCreationForm as AdminUserCreationForm, UserChangeForm as AdminUserChangeForm # 从本地 forms.py 导入并重命名以避免冲突


# UserCreationForm 和 UserChangeForm 已在 accounts/forms.py 中定义，可以直接使用或在 admin 中重新定义
# 这里假设使用 accounts/forms.py 中定义的，但 admin 中通常有自己的版本
# 为清晰起见，我们使用上面导入的 AdminUserCreationForm 和 AdminUserChangeForm

class UserAdmin(BaseUserAdmin):
        form = AdminUserChangeForm
        add_form = AdminUserCreationForm
        list_display = ('username', 'email', 'phone', 'is_active', 'is_staff', 'is_superuser') # 添加了 phone
        list_editable = ('is_staff', 'is_active')
        list_filter = ('is_staff', 'is_superuser', 'is_active', 'groups') # 添加了 is_superuser, is_active
        fieldsets = (
                (None, {'fields': ( 'username', 'email', 'phone', 'password')}),
                ('权限', {'fields': ('is_active', 'is_staff', 'is_superuser', 'groups', 'user_permissions')}), # 合并权限字段
        )
        add_fieldsets = (
                (None, {
                        'classes': ('wide',),
                        'fields': ('username', 'email', 'phone', 'password1', 'password2'),
                }),
                # ('权限', { # 在创建时，权限通常通过 staff/superuser 状态和组来处理
                #     'fields': ('is_active', 'is_staff', 'is_superuser', 'groups', 'user_permissions'),
                # })
        )
        search_fields = ('username', 'email', 'phone')
        ordering = ('username',) # 通常按 username 排序
        filter_horizontal = ('groups', 'user_permissions',)
        # 如果 User 模型有 first_name, last_name，BaseUserAdmin 会期望它们
        # 如果没有，需要从 fieldsets 和 list_display 中移除或调整


admin.site.register(User, UserAdmin)
# from django.contrib.auth.models import Group # 如果要取消注册 Group
# admin.site.unregister(Group)
```

```python
# accounts/urls.py
from django.urls import path
from accounts import views

app_name = 'accounts'
urlpatterns = [
        path('login/', views.userLogin, name='login'),
        path('register/', views.userRegister, name='register'),
        path('logout/', views.userLogout, name='logout') # 原文 LogoutPage，通常用 userLogout
]
```

```python
# accounts/views.py
from django.shortcuts import render, redirect
from django.contrib.auth import login, logout, authenticate
from django.contrib.auth.decorators import login_required
from django.utils.translation import gettext_lazy as _
from accounts.forms import LoginForm, RegisterForm # 假设 RegisterForm 用于注册
from django.contrib import messages
from accounts.models import User


def userRegister(request):
        if request.user.is_authenticated: # 如果用户已登录，重定向
                return redirect('app_name:home') # 假设 app_name:home 是主页
        form = RegisterForm()
        if request.method == 'POST':
                form = RegisterForm(request.POST)
                if form.is_valid():
                        # cd = form.cleaned_data # form.save() 会处理 cleaned_data
                        # 下面的逻辑应该在 RegisterForm 的 save 方法或 clean 方法中处理唯一性检查
                        # 这里简化，假设表单已处理验证
                        user = form.save()
                        login(request, user)
                        messages.success(request, _("您已成功注册用户"), extra_tags="success")
                        return redirect('app_name:home') # 假设 app_name:home 是主页
                else:
                        # 表单错误处理
                        for field, errors in form.errors.items():
                                for error in errors:
                                        messages.error(request, f"{form.fields[field].label if field != '__all__' else ''}: {error}", 'warning')
        return render(request, 'accounts/register.html', {'form': form})


def userLogin(request):
        if request.user.is_authenticated: # 如果用户已登录，重定向
                return redirect('app_name:home')
        if request.method == 'POST':
                form = LoginForm(request.POST)
                if form.is_valid():
                        cd = form.cleaned_data
                        # USERNAME_FIELD 在模型中是 'username'，所以 authenticate 使用 username
                        user = authenticate(request, username=cd['username'], password=cd['password'])
                        if user is not None:
                                if user.is_active: # 检查用户是否激活
                                        login(request, user)
                                        messages.success(request, _("登录成功"), extra_tags="success")
                                        # 重定向到 next 参数或主页
                                        next_url = request.GET.get('next')
                                        return redirect(next_url or 'app_name:home')
                                else:
                                        messages.error(request, _("此账户已被禁用。"), extra_tags="warning")
                        else:
                                messages.error(request, _("您的用户名或密码错误"), extra_tags="warning")
                else:
                        messages.error(request, _("请正确输入您的信息"), extra_tags="warning")
        else:
                form = LoginForm()
        return render(request, 'accounts/login.html', {'form': form})


@login_required # 默认 login_url 是 settings.LOGIN_URL
def userLogout(request): # 原文 LogoutPage
        logout(request)
        messages.success(request, _("您已成功登出"), extra_tags="success")
        return redirect('app_name:home')
```

## 发送邮件

```python
# settings.py
EMAIL_BACKEND = "django.core.mail.backends.console.EmailBackend" # 开发时输出到控制台

# 发送邮件函数
from django.core.mail import send_mail

send_mail(
        subject = "一篇新帖子已创建",
        message = "前往网站查看详情",
        from_email = "test@test.com", # 发件人邮箱
        recipient_list = ["test2@test.com"] # 收件人列表
)
```

## 信号 (Signals)

```python
# models.py (或 signals.py)
from django.db.models.signals import post_save # pre_save 未在此示例中使用
from django.dispatch import receiver # 使用 receiver 装饰器是更现代的方式
# from .models import UserProfile # 假设 UserProfile 模型已定义
# from django.contrib.auth.models import User # 或自定义的 User 模型

# 假设 User 和 UserProfile 模型已定义
# class UserProfile(models.Model):
# user = models.OneToOneField(User, on_delete=models.CASCADE)
# ... 其他字段

@receiver(post_save, sender=User) # User 应为实际的用户模型
def post_user_created_signal(sender, instance, created, **kwargs):
        if created:
                UserProfile.objects.create(user=instance)

# 如果不使用装饰器：
# post_save.connect(post_user_created_signal, sender=User)
# 确保此代码在 Django 加载时运行，例如在 app_name/apps.py 的 ready 方法中导入信号处理模块
```

## 数据填充 (Seed)

```python
from app_name.models import Product, Category
from django.http import HttpResponse
from faker import Faker
import random # 用于随机选择分类

def seed(request):
        Product.objects.all().delete()
        Category.objects.all().delete()

        categories_names = ["体育", "家居", "电子产品", "书籍", "服装"] # 示例分类名称
        created_categories = []
        for cat_name in categories_names:
                category = Category.objects.create(name=cat_name)
                created_categories.append(category)

        fake = Faker()
        for _ in range(100):
                product = Product()
                product.name = fake.unique.bs() # 使用更像产品名的假数据
                product.short_description = fake.sentence(nb_words=10)
                product.main_picture = fake.image_url(width=400, height=300) # 指定图片大小
                product.price = round(random.uniform(5.0, 500.0), 2) # 生成更真实的价格
                product.category =  random.choice(created_categories) # 从已创建的分类中随机选择
                product.save()

        return HttpResponse('数据填充完成')
```

## 环境变量

### .env 键/值文件

```python
$ pip install python-decouple
```

在项目根文件夹中创建一个名为 `.env` 的文件

```env
SECRET_KEY='your secret key'
ALLOWED_HOSTS='127.0.0.1,localhost,your_domain.com' # ALLOWED_HOSTS 是一个列表，decouple 可以处理
DEBUG=True # 示例
DATABASE_URL='postgres://user:password@host:port/dbname' # 示例
```

在 `settings.py` 中更改与安全相关的设置以指向 `.env` 文件

```python
from decouple import config, Csv

SECRET_KEY = config('SECRET_KEY')
# ALLOWED_HOSTS 应该是一个列表
ALLOWED_HOSTS = config('ALLOWED_HOSTS', cast=Csv())
DEBUG = config('DEBUG', default=False, cast=bool) # 示例
# DATABASE_URL = config('DATABASE_URL') # 示例，如果使用 dj-database-url
```

## 异步任务

### Django Celery Redis

Celery 是一个分布式任务队列，可以在主程序之外收集、记录、调度和执行任务。

#### 步骤 1：使用 pip 安装 Celery

```python
~$ pip install celery redis # 同时安装 redis 依赖，或者 pip install celery[redis]
```

#### 步骤 2：在您的项目模块中添加 `celery.py` 文件

```python
# your_project_name/celery.py (与 settings.py 同级)
import os
from celery import Celery

# 设置 Django 设置模块的默认环境变量。
os.environ.setdefault('DJANGO_SETTINGS_MODULE', 'your_project_name.settings')

app = Celery('your_project_name')

# 使用字符串参数，这样 worker 就不必序列化配置对象。
# - namespace='CELERY' 表示所有 Celery 相关的配置键都应该有一个 `CELERY_` 前缀。
app.config_from_object('django.conf:settings', namespace='CELERY')

# 从所有已注册的 Django app configs 中自动发现任务。
app.autodiscover_tasks()

@app.task(bind=True)
def debug_task(self):
        print(f'Request: {self.request!r}')
```

#### 步骤 3：将 Celery 应用导入 Django

<small>为确保 Django 启动时加载 Celery 应用，请将以下代码添加到项目模块中 `settings.py` 文件旁边的 `__init__.py` 文件中。</small>

```python
# your_project_name/__init__.py
from .celery import app as celery_app

__all__ = ('celery_app',)
```

#### 步骤 4：下载并运行 Redis 作为 Celery 的 ‘broker’

```bash
~$ redis-server
```

<small>您可以通过在终端中输入以下内容来测试 Redis 是否正常工作：</small>

```bash
~$ redis-cli ping
```

Redis 应该回复 PONG - 试试看！

#### 步骤 5：在 Django 项目中添加 Redis 作为依赖项：

```python
~$ pip install redis # 如果步骤1中已安装 celery[redis] 或 redis，则此步骤可省略
```

#### 步骤 6：将 Celery 相关配置添加到 Django 设置文件

一旦 Redis 启动，将以下代码添加到您的 `settings.py` 文件中，并使用 `django-celery-results` 来存储结果。

```python
~$ pip install django-celery-results
```

此扩展使您能够使用 Django ORM 存储 Celery 任务结果。<br> 它定义了一个用于存储任务结果的单一模型 (`django_celery_results.models.TaskResult`)，您可以像查询任何其他 Django 模型一样查询此数据库表。

```python
# settings.py

INSTALLED_APPS = [
                                … ,
                                'django_celery_results',
                                ]

# Celery 配置
CELERY_BROKER_URL = 'redis://localhost:6379/0' # /0 表示 Redis 的第0个数据库
CELERY_RESULT_BACKEND = 'redis://localhost:6379/0' # 也可以使用 'django-db'
CELERY_ACCEPT_CONTENT = ['application/json']
CELERY_TASK_SERIALIZER = 'json'
CELERY_RESULT_SERIALIZER = 'json'
CELERY_TIMEZONE = TIME_ZONE # TIME_ZONE 是 Django settings.py 中已定义的
# 如果使用 django-celery-results 作为结果后端
# CELERY_RESULT_BACKEND = 'django-db'
# CELERY_CACHE_BACKEND = 'django-cache' # 如果使用 Django 缓存作为 Celery 缓存后端

# Django 缓存配置 (如果 CELERY_CACHE_BACKEND = 'django-cache')
# CACHES = {
#     'default': {
#         'BACKEND': 'django_redis.cache.RedisCache', # 使用 django-redis
#         'LOCATION': 'redis://127.0.0.1:6379/1', # 使用不同的 Redis 数据库用于缓存
#         "OPTIONS": {
#             "CLIENT_CLASS": "django_redis.client.DefaultClient",
#         }
#     }
# }
# 如果 CELERY_RESULT_BACKEND = 'django-db'，则不需要 CACHES 配置，除非项目其他部分需要
# 确保运行迁移以创建 django_celery_results 所需的表
# python manage.py migrate django_celery_results
```

#### 就是这样！您现在应该能够将 Celery 与 Django 一起使用了

测试 Celery worker 是否准备好接收任务：

```python
~$ celery -A your_project_name worker -l info
```

最重要的任务是：始终需要运行一个 worker 来执行 celery 任务，如果 Redis 抛出任何错误，例如：

```
AttributeError: 'str' object has no attribute 'items'
```

- 解决方案是：您可能需要检查 Celery 和 Redis 的版本兼容性，或者配置序列化问题。

### 添加一个新任务

#### 步骤 1：在您的 Django 应用中添加 `tasks.py` 文件。

```python
# app_name/tasks.py
from celery import shared_task
# from celery.decorators import task # shared_task 是推荐的方式
from time import sleep
import time # 导入 time 模块

@shared_task(name='my_first_task') # 使用 shared_task 更好，因为它不需要直接访问 celery app 实例
def my_first_task(duration):
        sleep(duration)
        return('第一个任务完成')

@shared_task
def test_func():
        for i in range(10):
                print(i)
                sleep(0.1) # 添加少量延迟以便观察
        return '测试函数结束_OK'

@shared_task
def adding(x, y):
        time.sleep(10) # 确保 time 已导入
        result = x + y
        return result
```

#### 步骤 2：将任务分配给 Celery。

您需要将任务分配给 celery。要分配此任务，您需要以不同的方式调用此函数。celery 提供了 `delay()` 和 `apply_async()` 方法来调用任务。

```bash
# Python 中的普通函数调用
~$ my_first_task() # 这不会通过 Celery 执行

# 通过函数调用将任务添加到 celery
~$ my_first_task.delay()
```

您可以使用 `delay` 方法向函数发送参数。<small>要查看 celery 的运行情况，请打开终端的另一个选项卡，然后转到项目目录 (如果您正在使用虚拟环境，请激活它) 并再次运行此命令</small>

```bash
~$ celery -A your_project_name worker -l info
```

### 在您的应用中创建一个视图

```python
# app_name/views.py
from django.http import HttpResponse
from .tasks import my_first_task, test_func, adding # 使用相对导入

def index(request):
        my_first_task.delay(10)
        task_result = adding.delay(x=4, y=5)
        # task_result.id 可以用来稍后查询任务状态或结果
        return HttpResponse(f'响应完成。任务 ID: {task_result.id}')

def test(request):
        test_func.delay()
        return HttpResponse("测试任务已分派")
```

#### 然后从您的应用 URL 调用视图

```python
# app_name/urls.py
from django.urls import path
from .views import index, test # 使用相对导入

app_name = 'app_name' # 定义 app_name 以便在模板或重定向中使用命名空间

urlpatterns = [
        path('celery-index/', index, name='celery_index_url'),
        path('celery-test/', test, name='celery_test_url'),
]
```

### 在生产环境中使用 Supervisor 运行 Celery

#### 步骤 1：在 Ubuntu 服务器上安装 Supervisor

```bash
~$ sudo apt-get update
~$ sudo apt-get install supervisor
```

#### 步骤 2：在 Supervisor 中添加 `.conf` 文件

```bash
~$ sudo nano /etc/supervisor/conf.d/your_project_name_celery.conf
```
`your_project_name_celery` 可以是任何您喜欢的名称，但最好与您的项目相关。

#### 步骤 3：在 `your_project_name_celery.conf` 中添加一些配置

```ini
[program:your_project_name_celery]
command=/path/to/your/virtualenv/bin/celery -A your_project_name worker -l INFO
directory=/path/to/your/django_project_directory/
user=your_user # 运行 celery worker 的用户，例如 www-data 或您的部署用户
numprocs=1
autostart=true
autorestart=true
startsecs=10
stopwaitsecs=600
killasgroup=true
stdout_logfile=/path/to/your/django_project_directory/logs/celery_worker.log
stderr_logfile=/path/to/your/django_project_directory/logs/celery_worker_err.log
```

描述配置文件：
```ini
[program:your_project_name_celery]
# 您的 supervisord 程序名称

command=/path/to/your/virtualenv/bin/celery -A your_project_name worker -l INFO
# 如果使用虚拟环境，请设置 celery 程序的完整路径

directory=/path/to/your/django_project_directory/
# 您的 Django 项目目录

user=your_user
# 运行 celery worker 的用户。该用户必须存在。

numprocs=1
# 启动的进程数 (通常为1，除非您了解 Celery 并发模型)

autostart=true
# 如果为 true，则在 supervisord 启动时此程序将自动启动

autorestart=true
# 可以是 false、unexpected 或 true。如果为 false，则进程永远不会自动重启。如果为 unexpected，则当程序以非此进程配置关联的退出代码 (参见 exitcodes) 退出时，进程将重新启动。如果为 true，则当进程退出时，无论其退出代码如何，都将无条件重新启动。

startsecs=10
# 程序启动后需要保持运行的秒数，以认为启动成功

stopwaitsecs=600
# 发送 SIGTERM 后等待进程退出的秒数，之后发送 SIGKILL

killasgroup=true
# 如果为 true，当停止或杀死主进程时，也会杀死其整个进程组

stdout_logfile=/path/to/your/django_project_directory/logs/celery_worker.log
# 将进程标准输出放入此文件

stderr_logfile=/path/to/your/django_project_directory/logs/celery_worker_err.log
# 将进程标准错误输出放入此文件 (如果 redirect_stderr=false)
# redirect_stderr=true # 如果为 true，则将进程的 stderr 输出发送回 supervisord 的 stdout 文件描述符 (在 UNIX shell 术语中，这相当于执行 /the/program 2>&1)。如果使用此选项，则不需要 stderr_logfile。
```

#### 步骤 4：通知服务器配置更改

添加新程序后，我们应该运行以下两个命令，以通知服务器重新读取配置文件并应用任何更改。

```bash
~$ sudo supervisorctl reread
~$ sudo supervisorctl update
```

#### 管理 Supervisor 应用

```bash
~$ sudo supervisorctl
```

您将看到已注册进程的列表。您应该会看到一个名为 `your_project_name_celery` 的进程，状态为 `RUNNING`。

```
your_project_name_celery      RUNNING   pid 6853, uptime 0:22:30
supervisor>
```

输入 `help` 获取可用命令列表。

```
supervisor> help
default commands (type help <topic>):
=====================================
add    exit      open  reload  restart   start   tail
avail  fg        pid   remove  shutdown  status  update
clear  maintail  quit  reread  signal    stop    version
```

简而言之，我们可以通过将程序名称作为参数传递给相应命令来 `start`、`stop` 和 `restart` 程序。我们还可以使用 `tail` 命令查看程序输出。完成后，您可以 `quit`。

```bash
supervisor> quit
```

## 在服务器上部署 Django

### 在 Ubuntu 服务器上使用 Postgres、Nginx 和 Gunicorn 设置 Django

#### 步骤 1 — 从 Ubuntu 存储库安装软件包

```bash
sudo apt update
sudo apt install python3-venv python3-dev libpq-dev postgresql postgresql-contrib nginx curl
```

#### 步骤 2 — 创建 PostgreSQL 数据库和用户

```bash
sudo -u postgres psql
```

- 首先，为您的项目创建一个数据库：

```sql
postgres=# CREATE DATABASE myproject;
```

- 接下来，为我们的项目创建一个数据库用户。确保选择一个安全的密码：

```sql
postgres=# CREATE USER myprojectuser WITH PASSWORD 'password';
```

- 之后，您将修改刚创建的用户的一些连接参数

```sql
postgres=# ALTER ROLE myprojectuser SET client_encoding TO 'utf8';
postgres=# ALTER ROLE myprojectuser SET default_transaction_isolation TO 'read committed';
postgres=# ALTER ROLE myprojectuser SET timezone TO 'UTC';
```

- 现在，您可以授予新用户管理新数据库的权限：

```sql
postgres=# GRANT ALL PRIVILEGES ON DATABASE myproject TO myprojectuser;
```

- 完成后，通过键入以下命令退出 PostgreSQL 提示符：

```sql
postgres=# \q
```

#### 步骤 3 — 为您的项目创建 Python 虚拟环境

- 在项目目录中，通过键入以下命令创建 Python 虚拟环境：

```bash
mkdir ~/myprojectdir
cd ~/myprojectdir
```

- 在项目目录中，通过键入以下命令创建 Python 虚拟环境：

```bash
python3 -m venv myprojectenv
```

- 在安装项目的 Python 依赖项之前，您需要激活虚拟环境。您可以通过键入以下命令来执行此操作：

```bash
source myprojectenv/bin/activate
```

- 激活虚拟环境后，使用本地 pip 实例安装 Django、Gunicorn 和 psycopg2 PostgreSQL 适配器

```bash
(myprojectenv)$ pip install django gunicorn psycopg2-binary
```

#### 步骤 4 — 创建和配置新的 Django 项目

- 安装 Python 组件后，您现在可以创建实际的 Django 项目文件。

```bash
(myprojectenv)$ django-admin startproject myprojectname ~/myprojectdir # myprojectname 是项目名
# 注意：上面的命令会在 ~/myprojectdir 内部创建一个名为 myprojectname 的目录，
# 并在该目录内创建 manage.py 和另一个 myprojectname 目录 (包含 settings.py 等)。
# 如果希望项目文件直接在 ~/myprojectdir 中，可以使用：
# (myprojectenv)$ django-admin startproject myprojectname .
# (在 cd ~/myprojectdir 之后)
```

- 对于新创建的项目文件，您应该做的第一件事是调整设置。在文本编辑器中打开设置文件：

```bash
(myprojectenv)$ nano ~/myprojectdir/myprojectname/settings.py # 路径取决于上面的 startproject 命令
```

- 首先找到 `ALLOWED_HOSTS` 指令。

```python
# ~/myprojectdir/myprojectname/settings.py
ALLOWED_HOSTS = ['your_server_domain_or_IP', 'second_domain_or_IP', '. . .', 'localhost']
```

- 接下来，找到配置数据库访问的部分。它将以 `DATABASES` 开头。文件中的配置适用于 SQLite 数据库。

```python
. . .
DATABASES = {
        'default': {
                'ENGINE': 'django.db.backends.postgresql_psycopg2', # 或 'django.db.backends.postgresql'
                'NAME': 'myproject', # 之前创建的数据库名
                'USER': 'myprojectuser', # 之前创建的用户名
                'PASSWORD': 'password', # 用户的密码
                'HOST': 'localhost', # 或 PostgreSQL 服务器的 IP 地址
                'PORT': '', # 默认为 5432，如果不同则指定
        }
}
. . .
```

- 接下来，移至文件底部并添加一个设置，指示应放置静态文件的位置。

```python
. . .
STATIC_URL = '/static/' # URL 前缀，用于在模板中引用静态文件

# https://docs.djangoproject.com/en/4.0/ref/settings/#default-auto-field
DEFAULT_AUTO_FIELD = 'django.db.models.BigAutoField'

import os
STATIC_ROOT = os.path.join(BASE_DIR, 'staticfiles') # collectstatic 将收集静态文件到此目录
# MEDIA_URL = '/media/' # 如果使用媒体文件
# MEDIA_ROOT = os.path.join(BASE_DIR, 'mediafiles') # 存储上传的媒体文件
. . .
```

#### 步骤 5 — 完成初始项目设置

- 现在，您可以使用管理脚本将初始数据库模式迁移到我们的 PostgreSQL 数据库：

```bash
(myprojectenv)$ python ~/myprojectdir/manage.py makemigrations
(myprojectenv)$ python ~/myprojectdir/manage.py migrate
```

- 通过键入以下命令为项目创建一个管理用户：

```bash
(myprojectenv)$ python ~/myprojectdir/manage.py createsuperuser
```

- 您可以通过键入以下命令将所有静态内容收集到您配置的目录位置：

```bash
(myprojectenv)$ python ~/myprojectdir/manage.py collectstatic
```

#### 步骤 6 — 测试 Gunicorn 服务项目的能力

```bash
(myprojectenv)$ cd ~/myprojectdir
(myprojectenv)$ gunicorn --bind 0.0.0.0:8000 myprojectname.wsgi:application # myprojectname.wsgi
```

- 您现在已完成 Django 应用程序的配置。您可以通过键入以下命令退出我们的虚拟环境：

```bash
(myprojectenv)$ deactivate
```

#### 步骤 7 — 为 Gunicorn 创建 systemd Socket 和服务文件

```bash
sudo nano /etc/systemd/system/gunicorn.socket
```

- 在内部，您将创建一个 `[Unit]` 部分来描述套接字，一个 `[Socket]` 部分来定义套接字位置，以及一个 `[Install]` 部分来确保在正确的时间创建套接字：

```ini
# /etc/systemd/system/gunicorn.socket
[Unit]
Description=gunicorn socket

[Socket]
ListenStream=/run/gunicorn.sock

[Install]
WantedBy=sockets.target
```

- 完成后保存并关闭文件。
- 接下来，在文本编辑器中使用 sudo 权限为 Gunicorn 创建并打开一个 systemd 服务文件。服务文件名应与套接字文件名匹配，但扩展名除外：

```bash
sudo nano /etc/systemd/system/gunicorn.service
```

```ini
# /etc/systemd/system/gunicorn.service
[Unit]
Description=gunicorn daemon
Requires=gunicorn.socket
After=network.target

[Service]
User=sammy # 替换为运行 Gunicorn 的用户
Group=www-data # 替换为适当的组，通常是用户的主组或 www-data
WorkingDirectory=/home/sammy/myprojectdir # 替换为您的项目目录
ExecStart=/home/sammy/myprojectdir/myprojectenv/bin/gunicorn \
                    --access-logfile - \
                    --workers 3 \
                    --bind unix:/run/gunicorn.sock \
                    myprojectname.wsgi:application # 替换为您的项目名.wsgi:application

[Install]
WantedBy=multi-user.target
```

- 您现在可以启动并启用 Gunicorn 套接字。这将在 `/run/gunicorn.sock` 创建套接字文件，并在启动时创建。当连接到该套接字时，systemd 将自动启动 `gunicorn.service` 来处理它

```bash
sudo systemctl start gunicorn.socket
sudo systemctl enable gunicorn.socket
```

#### 步骤 8 — 检查 Gunicorn 套接字文件

- 检查进程的状态以了解它是否能够启动：

```bash
sudo systemctl status gunicorn.socket
```

- 接下来，检查 `/run` 目录中是否存在 `gunicorn.sock` 文件：

```bash
file /run/gunicorn.sock
```

#### 步骤 9 — 测试套接字激活

```bash
sudo systemctl status gunicorn # 此时可能未运行，因为还没有连接
```

- 要测试套接字激活机制，您可以通过 `curl` 向套接字发送连接，方法是键入：

```bash
curl --unix-socket /run/gunicorn.sock localhost
```

- 您应该在终端中收到应用程序的 HTML 输出。这表明 Gunicorn 已启动并且能够为您的 Django 应用程序提供服务。您可以通过键入以下命令来验证 Gunicorn 服务是否正在运行：

```bash
sudo systemctl status gunicorn
```

- 检查您的 `/etc/systemd/system/gunicorn.service` 文件是否有问题。如果您对 `/etc/systemd/system/gunicorn.service` 文件进行了更改，请重新加载守护程序以重新读取服务定义，并通过键入以下命令重新启动 Gunicorn 进程

```bash
sudo systemctl daemon-reload
sudo systemctl restart gunicorn
```

#### 步骤 10 — 配置 Nginx 以代理传递到 Gunicorn

- 首先在 Nginx 的 `sites-available` 目录中创建并打开一个新的服务器块：

```bash
sudo nano /etc/nginx/sites-available/myproject # myproject 是配置文件名
```

```nginx
server {
        listen 80;
        server_name your_server_domain_or_IP; # 替换为您的域名或 IP

        location = /favicon.ico { access_log off; log_not_found off; }
        location /static/ {
                alias /home/sammy/myprojectdir/staticfiles/; # 替换为您的 STATIC_ROOT 路径
        }

        location /media/ { # 如果使用媒体文件
                alias /home/sammy/myprojectdir/mediafiles/; # 替换为您的 MEDIA_ROOT 路径
        }

        location / {
                include proxy_params;
                proxy_pass http://unix:/run/gunicorn.sock;
        }
}
```

- 完成后保存并关闭文件。现在，您可以通过将其链接到 `sites-enabled` 目录来启用该文件：

```bash
sudo ln -s /etc/nginx/sites-available/myproject /etc/nginx/sites-enabled/
```

- 通过键入以下命令测试 Nginx 配置是否存在语法错误：

```bash
sudo nginx -t
```

- 如果没有报告错误，请通过键入以下命令重新启动 Nginx：

```bash
sudo systemctl restart nginx
```

- 您需要为端口 80 上的正常流量打开防火墙

```bash
sudo ufw allow 'Nginx Full'
```

您现在应该能够转到服务器的域或 IP 地址来查看您的应用程序。

#### 步骤 11 — Nginx 和 Gunicorn 故障排除

- Nginx 显示默认页面而不是 Django 应用程序

```bash
sudo tail -F /var/log/nginx/error.log
```

- Django 显示：“could not connect to server: Connection refused”（无法连接到服务器：连接被拒绝）

```bash
sudo systemctl status postgresql
```

- 如果它没有运行，您可以通过键入以下命令启动它并使其在启动时自动启动 (如果尚未配置为这样做)：

```bash
sudo systemctl start postgresql
sudo systemctl enable postgresql
```

如果您更改 Gunicorn 套接字或服务文件，请重新加载守护程序并通过键入以下命令重新启动进程：

```bash
sudo systemctl daemon-reload
sudo systemctl restart gunicorn.socket gunicorn.service
```

如果您更改 Nginx 服务器块配置，请测试配置然后通过键入以下命令重新启动 Nginx：

```bash
sudo nginx -t && sudo systemctl restart nginx
```
