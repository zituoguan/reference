---
title: Laravel
date: 2021-11-09 18:26:55
background: bg-[#e44230]
label: PHP
tags:
  - web
  - framework
  - php
categories:
  - 编程
intro: |
  [Laravel](https://laravel.com/docs/8.x/) 是一个富有表现力且先进的 PHP Web 应用程序框架。
  本速查表为 Laravel 8 的常用命令和功能提供参考。
plugins:
  - copyCode
---

## 入门

### 要求 {.row-span-2}

- PHP 版本 >= 7.3
- BCMath PHP 扩展
- Ctype PHP 扩展
- Fileinfo PHP 扩展
- JSON PHP 扩展
- Mbstring PHP 扩展
- OpenSSL PHP 扩展
- PDO PHP 扩展
- Tokenizer PHP 扩展
- XML PHP 扩展

确保您的 Web 服务器将所有请求定向到应用程序的 `public/index.php` 文件，请参阅：
[部署](#deployment)

### Windows

- #### 安装 [Docker Desktop](https://www.docker.com/products/docker-desktop)
- #### 安装并启用 [WSL2](https://docs.microsoft.com/en-us/windows/wsl/install)
- #### 确保 Docker Desktop [配置为使用 WSL2](https://docs.docker.com/desktop/windows/wsl/)
- #### 在 WSL2 终端中：
      ```shell
      $ curl -s https://laravel.build/example-app | bash
      $ cd example-app
      $ ./vendor/bin/sail up
      ```
  {.marker-timeline}

通过 `http://localhost` 访问应用程序

### Mac

- #### 安装 [Docker Desktop](https://www.docker.com/products/docker-desktop)
- #### 在终端中：
      ```shell
      $ curl -s https://laravel.build/example-app | bash
      $ cd example-app
      $ ./vendor/bin/sail up
      ```
  {.marker-timeline}

通过 `http://localhost` 访问应用程序

### Linux

```shell
$ curl -s https://laravel.build/example-app | bash
$ cd example-app
$ ./vendor/bin/sail up
```

通过 [Composer](https://getcomposer.org) 安装

```bash
$ composer create-project laravel/laravel example-app
$ cd example-app
$ php artisan serve
```

通过 `http://localhost` 访问应用程序

## 配置

### .env {.cols-2}

从 `.env` 文件中检索值

```php
env('APP_DEBUG');

// 带默认值
env('APP_DEBUG', false);
```

确定当前环境

```php
use Illuminate\Support\Facades\App;

$environment = App::environment();
```

使用“点”语法访问配置值

```php
// config/app.php --> ['timezone' => '']
$value = config('app.timezone');

// 如果配置值不存在，则检索默认值...
$value = config('app.timezone', 'Asia/Seoul');
```

在运行时设置配置值：

```php
config(['app.timezone' => 'America/Chicago']);
```

### 调试模式

开启（本地开发）：

```php
// .env 文件
APP_ENV=local
APP_DEBUG=true
// ...
```

关闭（生产环境）：

```php
// .env 文件
APP_ENV=production
APP_DEBUG=false
// ...
```

### 维护模式

临时禁用应用程序（503 状态码）

```bash
php artisan down
```

#### 禁用维护模式

```bash
php artisan up
```

#### 绕过维护模式

```bash
php artisan down --secret="1630542a-246b-4b66-afa1-dd72a4c43515"
```

访问您的应用程序 URL `https://example.com/1630542a-246b-4b66-afa1-dd72a4c43515` 以设置 cookie 并绕过
维护屏幕

## 路由

### 路由 HTTP 方法 {.row-span-2}

```php
Route::get($uri, $callback);
Route::post($uri, $callback);
Route::put($uri, $callback);
Route::patch($uri, $callback);
Route::delete($uri, $callback);
Route::options($uri, $callback);
```

多种 HTTP 方法

```php
Route::match(['get', 'post'], '/', function () {
    //
});

Route::any('/', function () {
    //
});
```

### 基本定义 {.row-span-2}

```php
use Illuminate\Support\Facades\Route;

// 闭包
Route::get('/greeting', function () {
    return 'Hello World';
});

// 控制器操作
Route::get(
    '/user/profile',
    [UserProfileController::class, 'show']
);
```

### 依赖注入

```php
use Illuminate\Http\Request;

Route::get('/users', function (Request $request) {
    // ...
});
```

类型提示具体依赖项以实现自动注入

### 视图路由

```php
// 参数 1: URI, 参数 2: 视图名称
Route::view('/welcome', 'welcome');

// 带数据
Route::view('/welcome', 'welcome', ['name' => 'Taylor']);
```

路由只需要返回一个视图。

### 路由模型绑定 {.row-span-4}

#### 隐式绑定

使用闭包

```php
use App\Models\User;

Route::get('/users/{user}', function (User $user) {
    return $user->email;
});

// /user/1 --> User::where('id', '=', 1);
```

使用控制器操作

```php
use App\Http\Controllers\UserController;
use App\Models\User;

// 路由定义...
Route::get('/users/{user}', [UserController::class, 'show']);

// 控制器方法定义...
public function show(User $user)
{
    return view('user.profile', ['user' => $user]);
}
```

使用自定义解析列

```php
use App\Models\Post;

Route::get('/posts/{post:slug}', function (Post $post) {
    return $post;
});

// /posts/my-post --> Post::where('slug', '=', 'my-post');
```

始终使用不同的列进行解析

```php
// 在 App\Models\Post 中
public function getRouteKeyName()
{
    return 'slug';
}
```

多个模型 - 第二个是第一个的子模型

```php
use App\Models\Post;
use App\Models\User;

Route::get('/users/{user}/posts/{post:slug}', function (User $user, Post $post) {
    return $post;
});
```

一种将模型实例直接自动注入路由的便捷方法

### 路由参数 {.row-span-2}

捕获路由中 URI 的段

#### 必需参数

```php
Route::get('/user/{id}', function ($id) {
    return 'User '.$id;
});
```

使用依赖注入

```php
use Illuminate\Http\Request;

Route::get('/user/{id}', function (Request $request, $id) {
    return 'User '.$id;
});
```

#### 可选参数

```php
Route::get('/user/{name?}', function ($name = null) {
    return $name;
});

Route::get('/user/{name?}', function ($name = 'John') {
    return $name;
});
```

### 重定向路由

HTTP `302` 状态

```php
Route::redirect('/here', '/there');
```

设置状态码

```php
Route::redirect('/here', '/there', 301);
```

永久 `301` 重定向

```php
Route::permanentRedirect('/here', '/there');
```

### 正则表达式约束 {.cols-2}

```php
Route::get('/user/{name}', function ($name) {
    //
})->where('name', '[A-Za-z]+');

Route::get('/user/{id}', function ($id) {
    //
})->where('id', '[0-9]+');

Route::get('/user/{id}/{name}', function ($id, $name) {
    //
})->where(['id' => '[0-9]+', 'name' => '[a-z]+']);
```

另请参阅：[正则表达式速查表](/regex)

### 命名路由

路由名称应始终唯一

```php
Route::get('/user/profile', function () {
    //
})->name('profile');
```

请参阅：[辅助函数](#helpers-cols-3)

### 回退路由

```php
Route::fallback(function () {
    //
});
```

当没有其他路由匹配时执行

### 路由组

#### 中间件

```php
Route::middleware(['first', 'second'])->group(function () {
    Route::get('/', function () {
        // 使用 first 和 second 中间件...
    });

    Route::get('/user/profile', function () {
        // 使用 first 和 second 中间件...
    });
});
```

#### URI 前缀

```php
Route::prefix('admin')->group(function () {
    Route::get('/users', function () {
        // 匹配 "/admin/users" URL
    });
});
```

#### 名称前缀

```php
Route::name('admin.')->group(function () {
    Route::get('/users', function () {
        // 路由分配的名称为 "admin.users"...
    })->name('users');
});
```

跨路由共享属性

### 访问当前路由

```php
use Illuminate\Support\Facades\Route;

// Illuminate\Routing\Route
$route = Route::current();

// 字符串
$name = Route::currentRouteName();

// 字符串
$action = Route::currentRouteAction();
```

## 辅助函数

### 路由 {.row-span-2}

#### 命名路由

```php
$url = route('profile');
```

带参数

```php
// Route::get('/user/{id}/profile', /*...*/ )->name('profile);

$url = route('profile', ['id' => 1]);

// /user/1/profile/
```

带查询字符串

```php
// Route::get('/user/{id}/profile', /*...*/ )->name('profile);

$url = route('profile', ['id' => 1, 'photos'=>'yes']);

// /user/1/profile?photos=yes
```

#### 重定向

```php
// 生成重定向...
return redirect()->route('profile');
```

#### Eloquent 模型

```php
echo route('post.show', ['post' => $post]);
```

路由辅助函数将自动提取模型的路由键。请参阅 [路由](#routing-cols-4)

### URL 生成

为您的应用程序生成任意 URL，这些 URL 将自动使用当前请求的方案（HTTP 或 HTTPS）和主机

```php
$post = App\Models\Post::find(1);

echo url("/posts/{$post->id}");

// http://example.com/posts/1
```

#### 当前 URL

```php
// 获取不带查询字符串的当前 URL...
echo url()->current();

// 获取包含查询字符串的当前 URL...
echo url()->full();

// 获取先前请求的完整 URL...
echo url()->previous();
```

### 命名路由 URL

```php
$url = route('profile');
```

请参阅 [命名路由](#named-route)

### 错误处理

```php
public function isValid($value)
{
    try {
        // 验证值...
    } catch (Throwable $e) {
        report($e);

        return false;
    }
}
```

报告异常但继续处理当前请求

### HTTP 异常

```php
// 页面未找到
abort(404);

// 未授权
abort(401);

// 禁止访问
abort(403);

// 服务器错误
abort(500);
```

使用状态码生成 HTTP 异常响应

## 控制器

### 基本

```php
namespace App\Http\Controllers;

use App\Http\Controllers\Controller;
use App\Models\User;

class UserController extends Controller
{
    public function show($id)
    {
        return view('user.profile', [
            'user' => User::findOrFail($id)
        ]);
    }
}
```

为此控制器方法定义路由：

```php
use App\Http\Controllers\UserController;

Route::get('/user/{id}', [UserController::class, 'show']);
```

## 请求

### CSRF 保护

Laravel 会为每个活动的用户会话自动生成一个 CSRF “令牌”。
此令牌用于验证经过身份验证的用户是否是实际发出请求的人。

获取当前会话的令牌：

```php
Route::get('/token', function (Request $request) {
    $token = $request->session()->token();

    $token = csrf_token();

    // ...
});
```

`POST`、`PUT`、`PATCH` 或 `DELETE` 表单应在表单中包含一个隐藏的 CSRF `_token` 字段以验证请求。

```html
<form method="POST" action="/profile">
  @csrf

  <!-- 等同于... -->
  <input type="hidden" name="_token" value="{{ csrf_token() }}" />
</form>
```

请参阅 [表单](#forms-cols-3)

### 访问请求

通过类型提示控制器操作或路由闭包来获取当前请求的实例

```php
// 控制器操作
class UserController extends Controller
{
    public function store(Request $request)
    {
        $name = $request->input('name');
    }
}

// 闭包
Route::get('/', function (Request $request) {
    //
});
```

[请参阅路由](#routing)

### 路径

请求的路径信息

```php
$uri = $request->path();

// https://example.com/foo/bar --> foo/bar
```

#### 将路径与模式匹配

验证传入的请求路径是否与给定模式匹配

```php
// * 是通配符
if ($request->is('admin/*')) {
    //
}
```

确定传入的请求是否与命名路由匹配

```php
if ($request->routeIs('admin.*')) {
    //
}
```

### URL

传入请求的完整 URL

```php
// 不带查询字符串的 URL
$url = $request->url();

// 包含查询字符串的 URL
$urlWithQueryString = $request->fullUrl();

// 将数据附加到查询字符串
$request->fullUrlWithQuery(['type' => 'phone']);
```

### 请求方法

```php
$method = $request->method();

// 验证 HTTP 动词是否与给定字符串匹配
if ($request->isMethod('post')) {
    //
}
```

### 客户端 IP

```php
$ipAddress = $request->ip();
```

### 标头

```php
$value = $request->header('X-Header-Name');

$value = $request->header('X-Header-Name', 'default value');

// 确定请求是否包含给定标头
if ($request->hasHeader('X-Header-Name')) {
    //
}

// 从 Authorization 标头中检索持有者令牌
$token = $request->bearerToken();
```

### 内容类型

返回一个包含请求接受的所有内容类型的数组

```php
$contentTypes = $request->getAcceptableContentTypes();
```

布尔值检查请求是否接受内容类型

```php
if ($request->accepts(['text/html', 'application/json'])) {
    // ...
}
```

### 输入 {.row-span-4}

以数组形式检索所有传入请求的输入数据

```php
$input = $request->all();
```

以集合形式检索所有传入请求的输入数据

```php
$input = $request->collect();

// 以集合形式检索子集
$request->collect('users')->each(function ($user) {
    // ...
});
```

请参阅 [辅助函数](#helpers-cols-3)

检索用户输入（也从查询字符串中获取值）

```php
$name = $request->input('name');

// 如果不存在则使用默认值
$name = $request->input('name', 'Sally');
```

访问数组输入

```php
$name = $request->input('products.0.name');

$names = $request->input('products.*.name');
```

以关联数组形式检索所有输入值：

```php
$input = $request->input();
```

仅从查询字符串中检索值：

```php
$name = $request->query('name');

// 带默认值
$name = $request->query('name', 'Helen');
```

以关联数组形式检索所有查询字符串值：

```php
$query = $request->query();
```

#### 布尔输入值

有助于复选框输入或其他布尔值。对于 `1`、`"1"`、`true`、`"true"`、`"on"` 和 `"yes"` 返回 `true`。
所有其他值将返回 `false`

```php
$archived = $request->boolean('archived');
```

### 动态属性

通过属性访问输入。
如果未作为输入找到，则将检查路由参数。

```php
$name = $request->name;
```

### 检索部分输入

```php
$input = $request->only(['username', 'password']);

$input = $request->only('username', 'password');

$input = $request->except(['credit_card']);

$input = $request->except('credit_card');
```

### 检查存在性

确定值是否存在

```php
if ($request->has('name')) {
    //
}

// 检查是否所有值都存在
if ($request->has(['name', 'email'])) {
    //
}

// 如果任何值存在
if ($request->hasAny(['name', 'email'])) {
    //
}

// 如果请求中存在文件
if ($request->hasFile('image')) {
    //
}
```

### 旧输入

从先前的请求中检索输入

```php
$username = $request->old('username');
```

或者使用 `old()` 辅助函数

```html
<input type="text" name="username" value="{{ old('username') }}">
```

请参阅：[辅助函数](#helpers-cols-3)
请参阅：[表单](#forms-cols-3)

### 上传的文件

从请求中检索上传的文件

```php
$file = $request->file('photo');

$file = $request->photo;
```

获取文件路径或扩展名

```php
$path = $request->photo->path();

$extension = $request->photo->extension();
```

使用随机生成的文件名存储上传的文件

```php
// 文件应存储的路径，相对于
// 文件系统配置的根目录
$path = $request->photo->store('images');

// 可选的第二个参数，用于指定文件系统磁盘
$path = $request->photo->store('images', 's3');
```

存储上传的文件并指定名称

```php
$path = $request->photo->storeAs('images', 'filename.jpg');

$path = $request->photo->storeAs('images', 'filename.jpg', 's3');
```

更多信息：[Laravel 文件存储](https://laravel.com/docs/8.x/filesystem)

## 视图

### 简介

- [Laravel 文档 - 视图](https://laravel.com/docs/8.x/views)

```html
<!-- 存储在 resources/views/greeting.blade.php 中的视图 -->

<html>
  <body>
    <h1>你好, <?php echo $name; ?></h1>
  </body>
</html>
```

通过在 `resources/views` 目录中放置一个扩展名为 `.blade.php` 的文件来创建视图。

### 向视图传递数据

#### 作为数组

```php
return view('greetings', ['name' => 'Victoria']);
```

#### 使用 with()

```php
return view('greeting')
            ->with('name', 'Victoria')
            ->with('occupation', 'Astronaut');
```

使用数据的键访问每个值

```html
<html>
  <body>
    <h1>你好, {{ $name }}</h1>
    <!-- 或者 -->
    <h1>你好, <?php echo $name; ?></h1>
  </body>
</html>
```

### view 辅助函数

使用 `view()` 辅助函数从路由返回视图

```php
Route::get('/', function () {
    return view('greeting', ['name' => 'James']);
});
```

请参阅：[视图路由](#view-routes) 和 [辅助函数](#helpers)

### 子目录

```php
// resources/views/admin.profile.blade.php
return view('admin.profile');
```

## Blade 模板

### 简介

- [Laravel 文档 - Blade 模板](https://laravel.com/docs/8.x/blade)

Blade 是 Laravel 中包含的模板引擎，它也允许您使用纯 PHP。

### 视图

Blade 视图使用 `view()` 辅助函数返回

```php
Route::get('/', function () {
    return view('welcome', ['name' => 'Samantha']);
});
```

请参阅：[视图](#view-helper)

### 注释

```html
{{-- 此注释不会出现在渲染的 HTML 中 --}}
```

### 指令 {.row-span-3}

#### if 语句

```php
@if (count($records) === 1)
    我有一条记录！
@elseif (count($records) > 1)
    我有多个记录！
@else
    我没有任何记录！
@endif
```

#### isset 和 empty

```php
@isset($records)
    // $records 已定义且不为 null...
@endisset

@empty($records)
    // $records 为 "empty"...
@endempty
```

#### 身份验证

```php
@auth
    // 用户已通过身份验证...
@endauth

@guest
    // 用户未通过身份验证...
@endguest
```

#### 循环

<!-- prettier-ignore -->
```html
@for ($i = 0; $i < 10; $i++)
    当前值为 {{ $i }}
@endfor

@foreach ($users as $user)
    <p>这是用户 {{ $user->id }}</p>
@endforeach

@forelse ($users as $user)
    <li>{{ $user->name }}</li>
@empty
    <p>没有用户</p>
@endforelse

@while (true)
    <p>我正在永远循环。</p>
@endwhile
```

循环迭代：

```php
@foreach ($users as $user)
    @if ($loop->first)
        这是第一次迭代。
    @endif

    @if ($loop->last)
        这是最后一次迭代。
    @endif

    <p>这是用户 {{ $user->id }}</p>
@endforeach
```

更多信息：[Laravel 循环变量](https://laravel.com/docs/8.x/blade#the-loop-variable)

### 显示数据

Blade 的 echo 语句 `{{ }}` 会自动通过 PHP 的 `htmlspecialchars` 函数处理，以防止 XSS 攻击。

显示 name 变量的内容：

```html
你好, {{ $name }}.
```

显示 PHP 函数的结果：

```html
当前 UNIX 时间戳是 {{ time() }}.
```

显示数据而不使用 `htmlspecialchars` 转义

```html
你好, {!! $name !!}.
```

### 包含子视图

从另一个视图中包含 Blade 视图。
父视图可用的所有变量也对包含的视图可用

```html
<div>
  <!-- resources/views/shared/errors/blade.php -->
  @include('shared.errors')

  <form>
    <!-- 表单内容 -->
  </form>
</div>
```

### 原生 PHP

执行纯 PHP 代码块

```php
@php
    $counter = 1;
@endphp
```

### 堆栈

Blade 允许您推送到命名堆栈，这些堆栈可以在另一个视图或布局中渲染。
对于子视图所需的 javascript 库很有用

```html
<!-- 添加到堆栈 -->
@push('scripts')
<script src="/example.js"></script>
@endpush
```

渲染堆栈

```html
<head>
  <!-- 头部内容 -->

  @stack('scripts')
</head>
```

前置到堆栈的开头

```php
@push('scripts')
    这将是第二个...
@endpush

// 稍后...

@prepend('scripts')
    这将是第一个...
@endprepend
```

## 表单

### 简介

- [Laravel 文档 - 表单](https://laravel.com/docs/8.x/blade#forms)

### CSRF 字段

包含一个隐藏的 CSRF 令牌字段以验证请求

<!-- prettier-ignore -->
```html
<form method="POST" action="/profile">
  @csrf

  ...
</form>
```

请参阅：[CSRF 保护](#csrf-protection)

### 方法字段

由于 HTML 表单无法发出 `PUT`、`PATCH` 或 `DELETE` 请求，您需要添加一个隐藏的 `_method` 字段来伪造这些 HTTP 动词：

<!-- prettier-ignore -->
```html
<form action="/post/my-post" method="POST">
  @method('PUT')

  ...
</form>
```

### 验证错误

<!-- prettier-ignore -->
```html
<!-- /resources/views/post/create.blade.php -->

<label for="title">文章标题</label>

<input id="title" type="text" class="@error('title') is-invalid @enderror" />

@error('title')
  <div class="alert alert-danger">{{ $message }}</div>
@enderror
```

请参阅：[验证](#validation-cols-3)

### 重新填充表单

由于验证错误而重定向时，请求输入会闪存到会话中。
使用 `old` 方法从先前的请求中检索输入

```php
$title = $request->old('title');
```

或者 `old()` 辅助函数

```html
<input type="text" name="title" value="{{ old('title') }}" />
```

## 验证

### 简介

- [Laravel 文档 - 验证](https://laravel.com/docs/8.x/validation)

如果验证失败，将生成到先前 URL 的重定向响应。
如果传入的请求是 XHR 请求，则将返回带有验证错误消息的 JSON 响应。

### 逻辑

```php
// 在 routes/web.php 中
Route::get('/post/create', [App\Http\Controllers\PostController::class, 'create']);
Route::post('/post', [App\Http\Controllers\PostController::class, 'store']);

// 在 app/Http/Controllers/PostController 中...
public function store(Request $request)
{
    $validated = $request->validate([
        // 输入名称 => 验证规则
        'title' => 'required|unique:posts|max:255',
        'body' => 'required',
    ]);

    // 博客文章有效...
}
```

### 规则 {.row-span-5}

也可以作为数组传递

```php
$validatedData = $request->validate([
    'title' => ['required', 'unique:posts', 'max:255'],
    'body' => ['required'],
]);
```

#### after:date

字段必须是给定日期之后的值。

```php
'start_date' => 'required|date|after:tomorrow'
```

您可以指定另一个字段与日期进行比较，而不是日期字符串

```php
'finish_date' => 'required|date|after:start_date'
```

请参阅 [before:date](#beforedate)

#### after_or_equal:date

字段必须是给定日期之后或等于给定日期的值。
请参阅 [after:date](#afterdate)

#### before:date

字段必须是给定日期之前的值。
可以将另一个字段的名称作为 `date` 的值提供。
请参阅 [after:date](#afterdate)

#### alpha_num

字段必须完全是字母数字字符

#### boolean

字段必须能够转换为 `boolean`。
接受的输入是 `true`、`false`、`1`、`0`、`"1"` 和 `"0"`

#### confirmed

字段必须有一个匹配的 `{field}_confirmation` 字段。
例如，如果字段是 password，则必须存在一个匹配的 `password_confirmation` 字段

#### current_password

字段必须与经过身份验证的用户的密码匹配。

#### date

根据 `strtotime` PHP 函数，字段必须是有效的、非相对的日期。

#### email

字段必须格式化为电子邮件地址。

#### file

字段必须是成功上传的文件。
请参阅：[上传的文件](#uploaded-files)

#### max:value

字段必须小于或等于最大值。
字符串、数字、数组和文件的计算方式与 [size](#sizevalue) 规则类似。

#### min:value

字段必须具有最小值。
字符串、数字、数组和文件的计算方式与 [size](#sizevalue) 规则类似。

#### mimetypes:text/plain,...

文件必须匹配给定的 MIME 类型之一：

```php
'video' => 'mimetypes:video/avi,video/mpeg,video/quicktime'
```

将读取文件内容，框架将尝试猜测 MIME 类型，而不管客户端提供的 MIME 类型如何。

#### mimes:foo,bar,...

字段的 MIME 类型必须对应于列出的扩展名之一。

```php
'photo' => 'mimes:jpg,bmp,png'
```

将读取文件内容，框架将尝试猜测 MIME 类型，而不管客户端提供的 MIME 类型如何。

[MIME 类型和扩展名的完整列表](https://svn.apache.org/repos/asf/httpd/httpd/trunk/docs/conf/mime.types)

#### nullable

字段可以为 null。

#### numeric

字段必须是数字。

#### password

字段必须与经过身份验证的用户的密码匹配。

#### prohibited

字段必须为空或不存在。

#### prohibited_if:anotherfield,value,...

如果 _anotherfield_ 字段等于任何值，则该字段必须为空或不存在。

#### prohibited_unless:anotherfield,value,...

除非 _anotherfield_ 字段等于任何值，否则该字段必须为空或不存在。

#### required

字段必须存在于输入数据中且不能为空。
如果满足以下条件之一，则字段被视为“空”：

- 值为 `null`。
- 值为空字符串。
- 值为空数组或空的 `Countable` 对象。
- 值是没有路径的已上传文件。

#### required_with:foo,bar,...

仅当任何其他指定字段存在且不为空时，该字段才必须存在且不为空

#### size:value

字段的大小必须与给定值匹配。

- 对于字符串：字符数
- 对于数字数据：整数值（还必须具有 `numeric` 或 `integer` 规则）。
- 对于数组：数组的计数
- 对于文件：文件大小（以千字节为单位）

```php
// 验证字符串长度是否正好为 12 个字符...
'title' => 'size:12';
// 验证提供的整数是否等于 10...
'seats' => 'integer|size:10';
// 验证数组是否正好有 5 个元素...
'tags' => 'array|size:5';
// 验证上传的文件大小是否正好为 512 千字节...
'image' => 'file|size:512';
```

#### unique:table,column

字段在给定的数据库表中不得存在

#### url

字段必须是有效的 URL

[查看所有可用规则](https://laravel.com/docs/8.x/validation#available-validation-rules)

### 验证密码

确保密码具有足够的复杂度

```php
$validatedData = $request->validate([
    'password' => ['required', 'confirmed', Password::min(8)],
]);
```

`Password` 规则对象允许您轻松自定义密码复杂度要求

```php
// 要求至少 8 个字符...
Password::min(8)

// 要求至少一个字母...
Password::min(8)->letters()

// 要求至少一个大写字母和一个小写字母...
Password::min(8)->mixedCase()

// 要求至少一个数字...
Password::min(8)->numbers()

// 要求至少一个符号...
Password::min(8)->symbols()
```

确保密码未在公共密码数据泄露事件中泄露

```php
Password::min(8)->uncompromised()
```

> _使用 [k-匿名性](https://en.wikipedia.org/wiki/K-anonymity) 模型，通过
> [haveibeenpwned.com](https://haveibeenpwned.com) 服务，而不会牺牲用户的隐私或安全_

方法可以链接

```php
Password::min(8)
    ->letters()
    ->mixedCase()
    ->numbers()
    ->symbols()
    ->uncompromised()
```

### 显示验证错误

```php
<!-- /resources/views/post/create.blade.php -->

<h1>创建文章</h1>

@if ($errors->any())
    <div class="alert alert-danger">
        <ul>
            @foreach ($errors->all() as $error)
                <li>{{ $error }}</li>
            @endforeach
        </ul>
    </div>
@endif

<!-- 创建文章表单 -->
```

请参阅：[验证错误](#validation-errors)

### 可选字段

如果您不希望验证器将 `null` 值视为无效，则通常需要将“可选”请求字段标记为 `nullable`

```php
// publish_at 字段可以为 null 或有效的日期表示形式
$request->validate([
    'title' => 'required|unique:posts|max:255',
    'body' => 'required',
    'publish_at' => 'nullable|date',
]);
```

### 已验证的输入

检索经过验证的请求数据

```php
$validated = $request->validated();
```

或者使用 `safe()`，它返回 `Illuminate\Support\ValidatedInput` 的实例

```php
$validated = $request->safe()->only(['name', 'email']);

$validated = $request->safe()->except(['name', 'email']);

$validated = $request->safe()->all();
```

#### 迭代

```php
foreach ($request->safe() as $key => $value) {
    //
}
```

#### 作为数组访问

```php
$validated = $request->safe();

$email = $validated['email'];
```

## 会话

### 简介

- [Laravel 文档 - 会话](https://laravel.com/docs/8.x/session)

Laravel 附带了各种会话后端，可通过统一的 API 进行访问。包括 Memcached、Redis 和数据库支持。

#### 配置

会话配置在 `config/session.php` 中。
默认情况下，Laravel 配置为使用文件会话驱动程序

### 检查 Isset / Exists

如果项目存在且不为 `null`，则返回 `true`：

```php
if ($request->session()->has('users')) {
    //
}
```

如果存在，即使为 `null`，也返回 `true`：

```php
if ($request->session()->exists('users')) {
    //
}
```

如果项目为 `null` 或不存在，则返回 `true`：

```php
if ($request->session()->missing('users')) {
    //
}
```

### 检索数据 {.row-span-2}

#### 通过请求

```php
// ...
class UserController extends Controller
{
    public function show(Request $request, $id)
    {
        $value = $request->session()->get('key');

        //
    }
}
```

将默认值作为第二个参数传递，以便在键不存在时使用

```php
$value = $request->session()->get('key', 'default');

// 可以传递闭包并作为默认值执行
$value = $request->session()->get('key', function () {
    return 'default';
});
```

#### 通过 session 辅助函数

```php
Route::get('/home', function () {
    // 从会话中检索一条数据...
    $value = session('key');

    // 指定默认值...
    $value = session('key', 'default');

    // 在会话中存储一条数据...
    session(['key' => 'value']);
});
```

请参阅：[会话辅助函数]()

#### 所有会话数据

```php
$data = $request->session()->all();
```

#### 检索并删除

从会话中检索并删除一个项目

```php
$value = $request->session()->pull('key', 'default');
```

### 存储数据

通过请求实例

```php
$request->session()->put('key', 'value');
```

通过全局“session”辅助函数

```php
session(['key' => 'value']);
```

将新值推送到作为数组的会话值上

```php
// 团队名称数组
$request->session()->push('user.teams', 'developers');
```

## 日志记录

### 配置

日志记录行为的配置选项在 `config/logging.php` 中。
默认情况下，Laravel 在记录消息时将使用堆栈通道，该通道将多个日志通道聚合到单个通道中。

### 级别 {.row-span-2}

[RFC 5424 规范](https://tools.ietf.org/html/rfc5424) 中定义的所有日志级别都可用：

- emergency (紧急)
- alert (警报)
- critical (危急)
- error (错误)
- warning (警告)
- notice (注意)
- info (信息)
- debug (调试)

### Log Facade {.row-span-2}

```php
use Illuminate\Support\Facades\Log;

Log::emergency($message);
Log::alert($message);
Log::critical($message);
Log::error($message);
Log::warning($message);
Log::notice($message);
Log::info($message);
Log::debug($message);
```

### 上下文信息

```php
use Illuminate\Support\Facades\Log;

Log::info('用户登录失败。', ['id' => $user->id]);
```

## 部署

### 简介

- [Laravel 文档 - 部署](https://laravel.com/docs/8.x/deployment)

确保您的 Web 服务器将所有请求定向到应用程序的 `public/index.php` 文件

### 优化

#### Composer 的自动加载器映射

```bash
composer install --optimize-autoloader --no-dev
```

#### 配置加载

确保您只在配置文件中调用 `env` 函数。
一旦配置被缓存，`.env` 文件将不会被加载，并且所有对 `.env` 变量的 `env` 函数调用都将返回 `null`

```bash
php artisan config:cache
```

#### 路由加载

```bash
php artisan route:cache
```

#### 视图加载

```bash
php artisan view:cache
```

### 调试模式

`config/app.php` 中的调试选项决定了向用户显示多少有关错误的信息。
默认情况下，此选项设置为 `.env` 文件中 `APP_DEBUG` 环境变量的值。在生产环境中，此值应始终为 `false`。
如果在生产环境中将 `APP_DEBUG` 变量设置为 `true`，则可能会将敏感配置值暴露给最终用户。

## 另请参阅

- [Laravel 文档](https://laravel.com/docs/8.x)
- [Laracasts](https://laracasts.com/)
- [Laravel API](https://laravel.com/api/8.x/)

