---
title: Selenium
date: 2024-05-04 19:50:01
background: bg-[#62ae41]
tags:
  - 自动化
  - 测试
categories:
  - 编程
intro: |
  本速查表是为 Selenium初学者准备的速成课程，旨在帮助他们了解 Selenium 的基本概念。
---

## 入门

### 初始化浏览器驱动 {.row-span-2}

| 浏览器    | 语法                                    |
| --------- | --------------------------------------- |
| `Chrome`  | WebDriver driver = new ChromeDriver();  |
| `Edge`    | WebDriver driver = new EdgeDriver();    |
| `Firefox` | WebDriver driver = new FirefoxDriver(); |
| `Safari`  | WebDriver driver = new SafariDriver();  |

{.show-header .left-text}

### Selenium 定位器 {.col-span-2}

| 定位器            | 语法                                          |
| ----------------- | --------------------------------------------- |
| `className`       | driver.findElement(By.className (“key”))      |
| `cssSelector`     | driver.findElement(By.cssSelector(key"))      |
| `id `             | driver.findElement(By.id(key"))               |
| `linkText`        | driver.findElement(By.linkText(key"))         |
| `name`            | driver.findElement(By.name(“key"))            |
| `partialLinkText` | driver.findElement(By.partialLinkText(“key”)) |
| `tagName `        | driver.findElement(By.tagName (“key”))        |
| `xpath`           | driver.findElement(By.xpath(“key”))           |

{.show-header .left-text}

### 导航到 URL

```shell script
driver.get("https://www.example.com");
```

### 关闭所有浏览器窗口

```shell script
driver.quit();
```

### 关闭当前浏览器窗口

```shell script
driver.close();
```

### 导航 {.col-span-2}

| 描述                     | 语法                                           |
| ------------------------------- | ------------------------------------------------ |
| `导航到一个新的 URL`         | driver.navigate().to("https://www.newsite.com"); |
| `前进到下一页`   | driver.navigate().forward();                     |
| `返回到上一页 ` | driver.navigate().back();                        |
| `刷新当前页面`      | driver.navigate().refresh();                     |

{.show-header .left-text}

### Frame 处理 {.col-span-2}

| 描述                       | 语法                              |
| --------------------------------- | ----------------------------------- |
| `切换到一个 frame`               | driver.switchTo().frame("frameId"); |
| `切换回主内容` | driver.switchTo().defaultContent(); |

{.show-header .left-text}

### 警告/弹窗

```shell script
Alert alert = driver.switchTo().alert();

// 用于点击警告框的“确定”按钮。
alert.accept();

// 用于点击警告框中的“取消”按钮。
alert.dismiss();

// 用于向警告框发送文本
alert.sendKeys("text");

// 用于捕获警告消息。
alert().getText();

```

### 鼠标和键盘操作 {.col-span-2}

```shell script
Actions actions = new Actions(driver);

// 将鼠标指针移动到元素的中心并点击它
actions.moveToElement(element).click().build().perform();

// 对元素执行双击操作
actions.doubleClick(element).perform();

// 将元素从一个点拖动到另一个点
actions.dragAndDrop(source, target).perform();

// 向元素发送一系列按键
actions.sendKeys(element, "text").perform();

```

### 页面信息 {.col-span-1}

```shell script
// 获取页面标题
driver.getTitle();

// 获取当前页面 URL
driver.getCurrentUrl();

// 获取整个页面源代码
driver.getPageSource();

```

### 等待 {.col-span-3}

```shell script
// 显式等待：这些是条件等待，可以应用于满足特定条件
WebDriverWait wait = new WebDriverWait(driver, 10);
wait.until(ExpectedConditions.elementToBeClickable(element));
```

```shell script
// 隐式等待：一旦命令运行，隐式等待将在浏览器打开的整个持续时间内保持。
driver.manage().timeouts().implicitlyWait(10, TimeUnit.SECONDS);
```

```shell script
// 流畅等待：Selenium 中的流畅等待标记了 Selenium WebDriver 等待某个条件（Web 元素）变为可见的最长时间。它还定义了 WebDriver 在抛出“ElementNotVisibleException”之前检查条件出现的频率。
FluentWait wait = new FluentWait(driver);
//指定等待的超时时间
wait.withTimeout(5000, TimeUnit.MILLISECONDS);
//指定轮询时间
wait.pollingEvery(250, TimeUnit.MILLISECONDS);
//指定要忽略的异常
wait.ignoring(NoSuchElementException.class)
//这是我们指定等待条件的方式。
wait.until(ExpectedConditions.alertIsPresent());
```
