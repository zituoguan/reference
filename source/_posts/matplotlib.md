---
title: "Matplotlib"
date: 06-06-2025
background: bg-[#1a073e]
tags:
  - "数据可视化"
  - "matplotlib"
  - "绘图"
categories:
  - "Python"
intro: |
  [Matplotlib](https://matplotlib.org/) 是一个用于在 Python 中创建静态、动画和交互式绘图的综合库。
  本速查表提供了从基础到高级用法的快速参考，涵盖了数据科学、机器学习和科学计算的基本功能。
plugins:
  - copyCode
---


---

##  入门 {.cols-2}

### 导入

```python
import matplotlib.pyplot as plt  # 核心绘图库
import numpy as np               # 用于数值运算
```

### 基本绘图

```python
x = np.linspace(0, 10, 100)      # 0到10之间的100个点
y = np.sin(x)                    # 正弦函数值
plt.plot(x, y)                   # 创建一个线图
plt.show()                       # 显示绘图
```

---

##  绘图类型 {.cols-2}

### 折线图

```python
plt.plot(x, y)                   # y 对 x 的折线图
plt.title("正弦波")             # 设置标题
plt.xlabel("x轴")               # 标记x轴
plt.ylabel("y轴")               # 标记y轴
plt.grid(True)                  # 显示网格线
plt.show()
```

### 散点图

```python
plt.scatter(x, y)               # 散点图
plt.title("散点图")
plt.show()
```

### 条形图

```python
categories = ['A', 'B', 'C']
values = [10, 20, 15]
plt.bar(categories, values)     # 垂直条形图
plt.title("条形图")
plt.show()
```

### 水平条形图

```python
plt.barh(categories, values)    # 水平条形图
plt.title("水平条形图")
plt.show()
```

### 直方图

```python
data = np.random.randn(1000)    # 随机正态分布数据
plt.hist(data, bins=30)         # 30个区间的直方图
plt.title("直方图")
plt.show()
```

### 饼图

```python
sizes = [25, 35, 20, 20]
labels = ['A', 'B', 'C', 'D']
plt.pie(sizes, labels=labels, autopct='%1.1f%%')  # 带百分比标签的饼图
plt.title("饼图")
plt.show()
```

---

##  自定义 {.row-span-2}

| 功能            | 代码示例                                                                             | 描述                                    |
| --------------- | ------------------------------------------------------------------------------------ | --------------------------------------- |
| 标题            | `plt.title("标题")`                                                                  | 设置绘图的标题                            |
| X/Y轴标签       | `plt.xlabel("X")`, `plt.ylabel("Y")`                                                 | 标记坐标轴                                |
| 网格            | `plt.grid(True)`                                                                     | 显示网格                                  |
| 图例            | `plt.legend(["线1"])`                                                                | 添加图例                                  |
| 线条样式        | `plt.plot(x, y, linestyle='--')`                                                     | 虚线                                    |
| 颜色            | `plt.plot(x, y, color='green')`                                                      | 设置线条颜色                              |
| 标记点          | `plt.plot(x, y, marker='o')`                                                         | 在数据点上显示标记                          |
| 坐标轴范围      | `plt.xlim(0, 10)`, `plt.ylim(-1, 1)`                                                 | 设置坐标轴范围                            |
| 刻度标签        | `plt.xticks([...])`, `plt.yticks([...])`                                             | 自定义刻度位置                            |
| 文本注解        | `plt.text(5, 0, "中点")`                                                             | 在特定坐标添加文本                          |
| 箭头            | `plt.annotate("峰值", xy=(7, 1), xytext=(6, 1.5), arrowprops=dict(arrowstyle="->"))` | 添加带箭头的注解                          |
| 样式表          | `plt.style.use('ggplot')`                                                            | 使用预定义样式，如 `seaborn`, `bmh`       |

---

##  子图与布局

### 多个子图

```python
fig, axs = plt.subplots(2, 2)        # 创建2x2的子图网格
axs[0, 0].plot(x, y)                 # 左上角子图
axs[0, 1].scatter(x, y)              # 右上角子图
axs[1, 0].bar(categories, values)    # 左下角子图
axs[1, 1].hist(data)                 # 右下角子图
plt.tight_layout()                   # 调整间距以防止重叠
plt.show()
```

### 图像大小

```python
plt.figure(figsize=(10, 5))         # 设置图像大小（宽度，高度，单位：英寸）
```

---

##  高级可视化 {.cols-2}

### 热力图

```python
data = np.random.rand(10, 10)       # 随机10x10矩阵
plt.imshow(data, cmap='hot', interpolation='nearest')  # 以图像形式显示
plt.colorbar()                      # 显示颜色条
plt.title("热力图")
plt.show()
```

### 等高线图

```python
X, Y = np.meshgrid(x, x)
Z = np.sin(X) * np.cos(Y)
plt.contour(X, Y, Z)                # 等高线
plt.title("等高线图")
plt.show()
```

### 3D绘图

```python
from mpl_toolkits.mplot3d import Axes3D
fig = plt.figure()
ax = fig.add_subplot(111, projection='3d')  # 3D子图
ax.plot3D(x, y, np.cos(x))                  # 3D线图
plt.title("3D绘图")
plt.show()
```

---

##  处理图像

```python
import matplotlib.image as mpimg
img = mpimg.imread('image.jpg')     # 加载图像
plt.imshow(img)                     # 显示图像
plt.axis('off')                     # 关闭坐标轴
plt.title("图像显示")
plt.show()
```

---

## 机器学习应用

### 绘制损失与周期关系图

```python
epochs = range(1, 11)
loss = [0.9, 0.7, 0.5, 0.4, 0.3, 0.25, 0.2, 0.18, 0.15, 0.13]
plt.plot(epochs, loss)
plt.title("训练损失")
plt.xlabel("周期 (Epoch)")
plt.ylabel("损失 (Loss)")
plt.show()
```

### 混淆矩阵 (热力图)

```python
from sklearn.metrics import confusion_matrix
import seaborn as sns

y_true = [0, 1, 2, 2, 0]
y_pred = [0, 0, 2, 2, 1]
cm = confusion_matrix(y_true, y_pred)    # 创建混淆矩阵
sns.heatmap(cm, annot=True, fmt='d', cmap='Blues')  # 热力图可视化
plt.title("混淆矩阵")
plt.show()
```

### ROC曲线

```python
from sklearn.metrics import roc_curve, auc

fpr, tpr, _ = roc_curve([0, 0, 1, 1], [0.1, 0.4, 0.35, 0.8])  # 计算ROC
roc_auc = auc(fpr, tpr)                 # 曲线下面积 (AUC)
plt.plot(fpr, tpr, label=f'AUC = {roc_auc:.2f}')
plt.plot([0, 1], [0, 1], 'k--')         # 对角线
plt.xlabel("假正例率 (False Positive Rate)")
plt.ylabel("真正例率 (True Positive Rate)")
plt.title("ROC曲线")
plt.legend()
plt.show()
```

---

##  保存绘图

```python
plt.savefig("figure.png", dpi=300, bbox_inches='tight')  # 将绘图保存到文件
```

---

##  显示与清除

```python
plt.show()     # 显示绘图窗口
plt.clf()      # 清除当前图像 (在循环中绘图时有用)
plt.close()    # 关闭图像窗口 (在脚本或GUI应用中用)
```

---

##  更多实用函数

| 函数                           | 用途                            |
| ------------------------------ | ------------------------------- |
| `plt.fill_between(x, y1, y2)`  | 填充两条曲线之间的区域            |
| `plt.axhline(y=value)`         | 在y值处绘制水平线                 |
| `plt.axvline(x=value)`         | 在x值处绘制垂直线                 |
| `plt.errorbar(x, y, yerr=...)` | 绘制带误差棒的图                  |
| `plt.twinx()`                  | 创建共享x轴的次级y轴              |
| `plt.subplots_adjust(...)`     | 手动调整子图间距                  |
| `plt.gca()`                    | 获取当前坐标轴 (Axes)             |
| `plt.gcf()`                    | 获取当前图像 (Figure)             |

---
