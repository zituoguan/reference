---
title: HTML 画布
date: 2024-05-28 22:16:42
background: bg-[#cc5534]
tags:
  - web
  - 前端
categories:
  - 编程
intro: |
  这份 HTML 画布快速参考备忘单以易读的布局列出了常用的 HTML5 画布 API。
plugins:
  - copyCode
  - runCode
---

## 入门

### 基本设置

```html
<!DOCTYPE html>
<html>
  <head>
    <title>画布示例</title>
  </head>
  <body>
    <canvas id="myCanvas" width="500" height="400" style="border:1px solid #000000;"></canvas>
    <script src="script.js"></script>
  </body>
</html>
```

### 获取绘图上下文

```js
const canvas = document.getElementById("myCanvas");
const ctx = canvas.getContext("2d");
```

## 绘制图形

### 矩形

```js
ctx.fillStyle = "red"; // 设置填充颜色为红色
ctx.fillRect(10, 10, 150, 100); // 绘制填充矩形 (x, y, 宽度, 高度)

ctx.strokeStyle = "blue"; // 设置描边颜色为蓝色
ctx.lineWidth = 5; // 设置线条宽度
ctx.strokeRect(200, 10, 150, 100); // 绘制描边矩形 (x, y, 宽度, 高度)

ctx.clearRect(15, 15, 30, 30); // 清除指定矩形区域 (x, y, 宽度, 高度)
```

## 路径

### 线条

```js
ctx.beginPath(); // 开始一条新路径
ctx.moveTo(50, 50); // 将画笔移动到起点 (x, y)
ctx.lineTo(200, 50); // 绘制一条直线到终点 (x, y)
ctx.lineTo(200, 200); // 绘制下一条直线到终点 (x, y)
ctx.closePath(); // 闭合路径（连接当前点到路径起点）
ctx.stroke(); // 描边当前路径
```

### 圆形

```js
ctx.beginPath();
// 绘制圆形 (圆心x, 圆心y, 半径, 起始角度, 结束角度, 逆时针[可选])
ctx.arc(150, 150, 75, 0, 2 * Math.PI);
ctx.fillStyle = "green";
ctx.fill(); // 填充当前路径
ctx.stroke(); // 描边当前路径
```

### 圆弧

```js
ctx.beginPath();
// 绘制圆弧 (圆心x, 圆心y, 半径, 起始角度, 结束角度)
ctx.arc(150, 150, 75, 0, Math.PI);
ctx.stroke();
```

## 贝塞尔曲线与二次曲线

### 二次曲线

```js
ctx.beginPath();
ctx.moveTo(50, 250);
// 绘制二次贝塞尔曲线 (控制点x, 控制点y, 结束点x, 结束点y)
ctx.quadraticCurveTo(200, 100, 400, 250);
ctx.stroke();
```

### 贝塞尔曲线

```js
ctx.beginPath();
ctx.moveTo(50, 300);
// 绘制三次贝塞尔曲线 (控制点1x, 控制点1y, 控制点2x, 控制点2y, 结束点x, 结束点y)
ctx.bezierCurveTo(150, 100, 350, 500, 450, 300);
ctx.stroke();
```

### 文本

```js
ctx.font = "30px Arial"; // 设置字体样式
ctx.fillStyle = "black";
ctx.fillText("Hello Canvas", 10, 50); // 绘制填充文本 (文本内容, x, y)

ctx.strokeText("Hello Canvas", 10, 100); // 绘制描边文本 (文本内容, x, y)
```

### 图像

```js
const img = new Image();
img.src = "path/to/image.jpg"; // 图片路径
img.onload = () => {
  ctx.drawImage(img, 10, 10); // 绘制图像 (图像元素, x, y)
  // 绘制图像并缩放 (图像元素, x, y, 宽度, 高度)
  ctx.drawImage(img, 50, 50, 100, 100);
  // 绘制图像的一部分并缩放 (图像元素, 源图像x, 源图像y, 源图像宽度, 源图像高度, 目标画布x, 目标画布y, 目标宽度, 目标高度)
  ctx.drawImage(img, 100, 100, 100, 100, 150, 150, 200, 200);
};
```

## 变换

### 平移

```js
ctx.translate(100, 100); // 平移画布 (x轴位移, y轴位移)
ctx.fillRect(0, 0, 50, 50); // 变换后的坐标系中绘制
```

### 旋转

```js
ctx.rotate((Math.PI / 180) * 45); // 旋转画布 (旋转角度 - 弧度)
ctx.fillRect(100, 100, 50, 50); // 变换后的坐标系中绘制
```

### 缩放

```js
ctx.scale(2, 2); // 缩放画布 (x轴缩放因子, y轴缩放因子)
ctx.fillRect(50, 50, 50, 50); // 变换后的坐标系中绘制
```

## 渐变

### 线性渐变

```js
// 创建线性渐变 (起点x, 起点y, 终点x, 终点y)
const linearGradient = ctx.createLinearGradient(0, 0, 200, 0);
linearGradient.addColorStop(0, "red"); // 添加颜色断点 (位置, 颜色)
linearGradient.addColorStop(1, "blue");
ctx.fillStyle = linearGradient;
ctx.fillRect(10, 10, 200, 100);
```

### 径向渐变

```js
// 创建径向渐变 (起始圆心x, 起始圆心y, 起始圆半径, 结束圆心x, 结束圆心y, 结束圆半径)
const radialGradient = ctx.createRadialGradient(75, 50, 5, 90, 60, 100);
radialGradient.addColorStop(0, "red");
radialGradient.addColorStop(1, "blue");
ctx.fillStyle = radialGradient;
ctx.fillRect(10, 10, 200, 100);
```

### 图案填充

```js
const img = new Image();
img.src = "path/to/image.jpg";
img.onload = () => {
  // 创建图案 (图像元素, 重复方式: 'repeat', 'repeat-x', 'repeat-y', 'no-repeat')
  const pattern = ctx.createPattern(img, "repeat");
  ctx.fillStyle = pattern;
  ctx.fillRect(0, 0, 300, 300);
};
```

### 阴影

```js
ctx.shadowColor = "rgba(0, 0, 0, 0.5)"; // 阴影颜色
ctx.shadowBlur = 10; // 阴影模糊级别
ctx.shadowOffsetX = 5; // 阴影水平偏移
ctx.shadowOffsetY = 5; // 阴影垂直偏移

ctx.fillStyle = "red";
ctx.fillRect(100, 100, 100, 100);
```

## 合成

### 全局透明度 (globalAlpha)

```js
ctx.globalAlpha = 0.5; // 设置全局透明度
ctx.fillStyle = "red";
ctx.fillRect(100, 100, 100, 100);

ctx.fillStyle = "blue";
ctx.fillRect(150, 150, 100, 100);
```

### 全局合成操作 (globalCompositeOperation)

```js
ctx.globalCompositeOperation = "source-over"; // 默认值，新图形绘制在旧图形之上
ctx.fillStyle = "red";
ctx.fillRect(100, 100, 100, 100);

ctx.globalCompositeOperation = "destination-over"; // 新图形绘制在旧图形之下
ctx.fillStyle = "blue";
ctx.fillRect(150, 150, 100, 100);
```

### 动画

```js
let x = 0;
function draw() {
  ctx.clearRect(0, 0, canvas.width, canvas.height); // 清除画布
  ctx.fillStyle = "blue";
  ctx.fillRect(x, 100, 50, 50);
  x += 2;
  requestAnimationFrame(draw); // 请求下一帧动画
}
draw();
```

## 拓展阅读

- [MDN 文档](https://developer.mozilla.org/zh-CN/docs/Web/API/Canvas_API)
