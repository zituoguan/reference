---
title: Unity Shader Graph（着色器视图）
date: 2024-08-10 12:15:05
background: bg-[#7c7c7c]
label:
tags:
  - unity
  - shader
  - computer graphics
  - visual effects
categories:
  - 编程
intro: |
  这是 Unity Shader Graph（着色器视图）的可视化速查表。该工具用于在流行的游戏引擎 Unity 中创建自定义着色器材质。
---

## Shader Graph 节点 {.cols-2}

<code>我们使用 <yel>**SAIT**</yel> 来表示输出类型与输入类型相同。</code> {.col-span-2}

## 1. 属性 {.cols-2}

### 定位 {.row-span-2}

<yel>**Position (位置)**</yel> - 提供顶点位置
- **输入**
  - |-|-|
  | -------- | ---------------------- |
  | /     | 无输入               |

  {.left-text}

- **输出**
  - |-|-|
  | -------- | ---------------------- |
  | `Vector3`| 提供顶点位置|
  
  {.left-text}

{.shortcuts .marker-round .cols-2}

<yel>**Normal (法线)**</yel> - 提供表面法线方向
- **输入**
  - |-|-|
  | -------- | ---------------------- |
  | /     | 无输入               |

  {.left-text}

- **输出**
  - |-|-|
  | -------- | ---------------------- |
  | `Vector3`| 提供表面法线 |

  {.left-text}

{.shortcuts .marker-round .cols-2}

<yel>**World Position (世界位置)**</yel> - 返回对象的世界空间位置
- **输入**
  - |-|-|
  | -------- | ---------------------- |
  | /     | 无输入               |

  {.left-text}

- **输出**
  - |-|-|
  | -------- | ---------------------- |
  | `Vector3` | 世界空间位置   |

  {.left-text}

{.shortcuts .marker-round .cols-2}

<yel>**Object Position (对象位置)**</yel> - 返回对象的局部空间位置
- **输入**
  - |-|-|
  | -------- | ---------------------- |
  | /     | 无输入               |

  {.left-text}

- **输出**
  - |-|-|
  | -------- | ---------------------- |
  | `Vector3` | 局部空间位置   |

  {.left-text}

{.shortcuts .marker-round .cols-2}

<yel>**Screen Position (屏幕位置)**</yel> - 返回对象的屏幕空间位置
- **输入**
  - |-|-|
  | -------- | ---------------------- |
  | /     | 无输入               |

  {.left-text}

- **输出**
  - |-|-|
  | -------- | ---------------------- |
  | `Vector4` | 屏幕空间位置  |

  {.left-text}

{.shortcuts .marker-round .cols-2}

<yel>**Camera Position (摄像机位置)**</yel> - 返回摄像机的世界空间位置
- **输入**
  - |-|-|
  | -------- | ---------------------- |
  | /     | 无输入               |

  {.left-text}

- **输出**
  - |-|-|
  | -------- | ---------------------- |
  | `Vector3` | 摄像机世界空间位置 |

  {.left-text}

{.shortcuts .marker-round .cols-2}

### 计时

<yel>**Time (时间)**</yel> - 输出各种与时间相关的值
- **输入**
  - |-|-|
  | -------- | ---------------------- |
  | /     | 无输入               |

  {.left-text}

- **输出**
  - |-|-|
  | -------- | ---------------------- |
  | `Float`  | 时间 (T) - 自着色器启动以来经过的总时间 |
  | `Float`  | 正弦时间 (T/8π) - 基于时间的正弦波                    |
  | `Float`  | 余弦时间 (T/8π) - 基于时间的余弦波                  |
  | `Float`  | 增量时间 - 上一帧与当前帧之间经过的时间 |

  {.left-text}

{.shortcuts .marker-round .cols-2}


## 2. 数学运算 {.cols-2}

### 基本数学运算

<yel>**Add (加法)**</yel> - 将两个值相加
- **输入**
  - |-|-|
  | -------- | ---------------------- |
  | `Float` <br> `Vector` | 第一个值  |
  | `Float` <br> `Vector` | 第二个值 |

  {.left-text}

- **输出**
  - |-|-|
  | -------- | ---------------------- |
  | SAIT | 两个输入的和 |

  {.left-text}
  
{.shortcuts .marker-round .cols-2}

<yel>**Subtract (减法)**</yel> - 从一个值中减去另一个值
- **输入**
  - |-|-|
  | -------- | ---------------------- |
  | `Float` <br> `Vector` | 被减数      |
  | `Float` <br> `Vector` | 减数   |

  {.left-text}

- **输出**
  - |-|-|
  | -------- | ---------------------- |
  | SAIT | 两个输入的差 |

  {.left-text}
  
{.shortcuts .marker-round .cols-2}

<yel>**Multiply (乘法)**</yel> - 将两个值相乘
- **输入**
  - |-|-|
  | -------- | ---------------------- |
  | `Float` <br> `Vector` <br> `Matrix` | 第一个值 |
  | `Float` <br> `Vector` <br> `Matrix` | 第二个值|

  {.left-text}

- **输出**
  - |-|-|
  | -------- | ---------------------- |
  | SAIT | 两个输入的积 |

  {.left-text}

{.shortcuts .marker-round .cols-2}

### 高级数学运算 {.row-span-2}

<yel>**Power (幂)**</yel> - 计算输入的幂
- **输入**
  - |-|-|
  | -------- | ---------------------- |
  | `Float`  | 底数                   |
  | `Float`  | 指数               |

  {.left-text}

- **输出**
  - |-|-|
  | -------- | ---------------------- |
  | `Float`  | 底数相对于指数的幂的结果 |

  {.left-text}

{.shortcuts .marker-round .cols-2}

<yel>**Sqrt (平方根)**</yel> - 输入的平方根
- **输入**
  - |-|-|
  | -------- | ---------------------- |
  | `Float`  | 输入值             |

  {.left-text}

- **输出**
  - |-|-|
  | -------- | ---------------------- |
  | `Float`  | 输入的平方根 |

  {.left-text}

{.shortcuts .marker-round .cols-2}

<yel>**Abs (绝对值)**</yel> - 输出绝对值
- **输入**
  - |-|-|
  | -------- | ---------------------- |
  | `Float` <br> `Vector` | 输入值  |

  {.left-text}

- **输出**
  - |-|-|
  | -------- | ---------------------- |
  | SAIT | 输入的绝对值 |

  {.left-text}

{.shortcuts .marker-round .cols-2}

<yel>**Dot Product (点积)**</yel> - 计算两个向量之间的点积
- **输入**
  - |-|-|
  | -------- | ---------------------- |
  | `Vector3` <br> `Vector4` | 第一个向量 |
  | `Vector3` <br> `Vector4` | 第二个向量|

  {.left-text}

- **输出**
  - |-|-|
  | -------- |  ---------------------- |
  |`Float`  | 点积结果 |

  {.left-text}

{.shortcuts .marker-round .cols-2}

<yel>**Cross Product (叉积)**</yel> - 计算两个向量之间的叉积
- **输入**
  - |-|-|
  | -------- | ---------------------- |
  | `Vector3` | 第一个向量           |
  | `Vector3` | 第二个向量          |

  {.left-text}

- **输出**
  - |-|-|
  | -------- | ---------------------- |
  | `Vector3` | 叉积结果 |

  {.left-text}

{.shortcuts .marker-round .cols-2}

### 三角函数

<yel>**Sin (正弦)**</yel> - 输出输入的正弦值
- **输入**
  - |-|-|
  | -------- | ---------------------- |
  | `Float`  | 输入（弧度）        |

  {.left-text}

- **输出**
  - |-|-|
  | -------- | ---------------------- |
  | `Float`  | 输入的正弦值       |

  {.left-text}

{.shortcuts .marker-round .cols-2}

<yel>**Cos (余弦)**</yel> - 输出输入的余弦值
- **输入**
  - |-|-|
  | -------- | ---------------------- |
  | `Float`  | 输入（弧度）        |

  {.left-text}

- **输出**
  - |-|-|
  | -------- | ---------------------- |
  | `Float`  | 输入的余弦值     |

  {.left-text}

{.shortcuts .marker-round .cols-2}

### 插值 {.row-span-2}

<yel>**Lerp (线性插值)**</yel> - 在两个值之间进行线性插值
- **输入**
  - |-|-|
  | -------- | ---------------------- |
  | `Float` <br> `Vector`  | 起始值             |
  | `Float` <br> `Vector`  | 结束值               |
  | `Float` <br> `Vector`  | 插值因子 (T)|

  {.left-text}

- **输出**
  - |-|-|
  | -------- | ---------------------- |
  | SAIT  | 插值结果     |

  {.left-text}

{.shortcuts .marker-round .cols-2}

<yel>**Step (阶跃)**</yel> - 在两个阈值之间创建一个阶跃
- **输入**
  - |-|-|
  | -------- | ---------------------- |
  | `Float` <br> `Vector`  | 阈值               |
  | `Float` <br> `Vector`  | 输入                   |

  {.left-text}

- **输出**
  - |-|-|
  | -------- | ---------------------- |
  | SAIT  | 阶跃结果             |

  {.left-text}

{.shortcuts .marker-round .cols-2}


## 3. 颜色处理 {.cols-2}

### 基本颜色操作

<yel>**Color (颜色)**</yel> - 提供一个恒定的颜色值
- **输入**
  - |-|-|
  | -------- | ---------------------- |
  | /     | 无输入               |

  {.left-text}

- **输出**
  - |-|-|
  | -------- | ---------------------- |
  | `Vector4` | RGBA 颜色值       |

  {.left-text}

{.shortcuts .marker-round .cols-2}

<yel>**Add Color (颜色相加)**</yel> - 将两个颜色值相加
- **输入**
  - |-|-|
  | -------- | ---------------------- |
  | `Vector4` | 第一个颜色            |
  | `Vector4` | 第二个颜色           |

  {.left-text}

- **输出**
  - |-|-|
  | -------- | ---------------------- |
  | `Vector4` | 两个颜色的和  |

  {.left-text}

{.shortcuts .marker-round .cols-2}

<yel>**Multiply Color (颜色相乘)**</yel> - 将两个颜色值相乘
- **输入**
  - |-|-|
  | -------- | ---------------------- |
  | `Vector4` | 第一个颜色            |
  | `Vector4` | 第二个颜色           |

  {.left-text}

- **输出**
  - |-|-|
  | -------- | ---------------------- |
  | `Vector4` | 两个颜色的积 |

  {.left-text}

{.shortcuts .marker-round .cols-2}

<yel>**Lerp Color (颜色插值)**</yel> - 在两个颜色之间进行插值
- **输入**
  - |-|-|
  | -------- | ---------------------- |
  | `Vector4` | 起始颜色            |
  | `Vector4` | 结束颜色              |
  | `Float`   | 插值因子 (T)|

  {.left-text}

- **输出**
  - |-|-|
  | -------- | ---------------------- |
  | `Vector4` | 插值后的颜色     |

  {.left-text}

{.shortcuts .marker-round .cols-2}

### 颜色调整 {.row-span-2}

<yel>**Saturation (饱和度)**</yel> - 调整输入颜色的饱和度
- **输入**
  - |-|-|
  | -------- | ---------------------- |
  | `Vector4` | 输入颜色            |
  | `Float`   | 饱和度因子      |

  {.left-text}

- **输出**
  - |-|-|
  | -------- | ---------------------- |
  | `Vector4` | 调整后的颜色         |

  {.left-text}

{.shortcuts .marker-round .cols-2}

<yel>**Contrast (对比度)**</yel> - 调整输入颜色的对比度
- **输入**
  - |-|-|
  | -------- | ---------------------- |
  | `Vector4` | 输入颜色            |
  | `Float`   | 对比度因子        |

  {.left-text}

- **输出**
  - |-|-|
  | -------- | ---------------------- |
  | `Vector4` | 调整后的颜色         |

  {.left-text}

{.shortcuts .marker-round .cols-2}

<yel>**Hue (色相)**</yel> - 调整输入颜色的色相
- **输入**
  - |-|-|
  | -------- | ---------------------- |
  | `Vector4` | 输入颜色            |
  | `Float`   | 色相偏移量       |

  {.left-text}

- **输出**
  - |-|-|
  | -------- | ---------------------- |
  | `Vector4` | 色相偏移后的颜色 |

  {.left-text}

{.shortcuts .marker-round .cols-2}

<yel>**Invert Colors (反色)**</yel> - 反转输入颜色
- **输入**
  - |-|-|
  | -------- | ---------------------- |
  | `Vector4` | 输入颜色            |

  {.left-text}

- **输出**
  - |-|-|
  | -------- | ---------------------- |
  | `Vector4` | 反转后的颜色         |

  {.left-text}

{.shortcuts .marker-round .cols-2}

<yel>**Replace Color (替换颜色)**</yel> - 将输入中的特定颜色替换为新颜色
- **输入**
  - |-|-|
  | -------- | ---------------------- |
  | `Vector4` | 输入颜色            |
  | `Vector4` | 目标颜色           |
  | `Vector4` | 替换颜色      |

  {.left-text}

- **输出**
  - |-|-|
  | -------- | ---------------------- |
  | `Vector4` | 替换值后的颜色 |

  {.left-text}

{.shortcuts .marker-round .cols-2}

<yel>**White Balance (白平衡)**</yel> - 调整输入颜色的白平衡
- **输入**
  - |-|-|
  | -------- | ---------------------- |
  | `Vector4` | 输入颜色            |
  | `Float`   | 色温值      |
  | `Float`   | 色调值             |

  {.left-text}

- **输出**
  - |-|-|
  | -------- | ---------------------- |
  | `Vector4` | 调整后的颜色         |

  {.left-text}

{.shortcuts .marker-round .cols-2}

### 通道操作

<yel>**Channel Mixer (通道混合器)**</yel> - 独立修改颜色通道
- **输入**
  - |-|-|
  | -------- | ---------------------- |
  | `Vector4` | 输入颜色            |
  | `Float`   | 红色通道乘数 |
  | `Float`   | 绿色通道乘数 |
  | `Float`   | 蓝色通道乘数 |

  {.left-text}

- **输出**
  - |-|-|
  | -------- | ---------------------- |
  | `Vector4` | 修改后的颜色         |

  {.left-text}

{.shortcuts .marker-round .cols-2}

## 4. 纹理处理 {.cols-2}

### 采样

<yel>**Sample Texture (采样纹理)**</yel> - 从纹理中检索颜色数据
- **输入**
  - |-|-|
  | -------- | ---------------------- |
  | `Texture (sampler)` | 纹理输入  |
  | `Vector2` | UV 坐标         |

  {.left-text}

- **输出**
  - |-|-|
  | -------- | ---------------------- |
  | `Vector4` | 来自纹理的颜色数据 |

  {.left-text}

{.shortcuts .marker-round .cols-2}

<yel>**UV (UV坐标)**</yel> - 提供用于纹理映射的 UV 坐标
- **输入**
  - |-|-|
  | -------- | ---------------------- |
  | /     | 无输入               |

  {.left-text}

- **输出**
  - |-|-|
  | -------- | ---------------------- |
  | `Vector2` | UV 坐标         |

  {.left-text}

{.shortcuts .marker-round .cols-2}

### 操作 {.row-span-2}

<yel>**Tiling Offset (平铺偏移)**</yel> - 调整纹理的平铺和偏移
- **输入**
  - |-|-|
  | -------- | ---------------------- |
  | `Vector2` | 平铺值          |
  | `Vector2` | 偏移值          |

  {.left-text}

- **输出**
  - |-|-|
  | -------- | ---------------------- |
  | `Vector2` | 修改后的 UV 坐标 |

  {.left-text}

{.shortcuts .marker-round .cols-2}

<yel>**Distortion (扭曲)**</yel> - 扭曲对象表面
- **输入**
  - |-|-|
  | -------- | ---------------------- |
  | `Float`   | 扭曲强度    |
  | `Vector2` | UV 坐标         |

  {.left-text}

- **输出**
  - |-|-|
  | -------- | ---------------------- |
  | `Vector2` | 扭曲后的 UV 坐标  |

  {.left-text}

{.shortcuts .marker-round .cols-2}

<yel>**Parallax (视差)**</yel> - 使用视差映射模拟深度
- **输入**
  - |-|-|
  | -------- | ---------------------- |
  | Texture (sampler) | 输入纹理  |
  | `Vector2` | UV 坐标         |
  | `Float`   | 深度值            |

  {.left-text}

- **输出**
  - |-|-|
  | -------- | ---------------------- |
  | `Vector2` | 调整后的 UV 坐标|

  {.left-text}

{.shortcuts .marker-round .cols-2}

## 5. 特效 {.cols-2}

### 视觉特效 {.row-span-2}

<yel>**Fresnel Effect (菲涅尔效应)**</yel> - 在对象边缘创建辉光效果
- **输入**
  - |-|-|
  | -------- | ---------------------- |
  | `Vector3` | 视图方向         |
  | `Float`   | 特效强度    |

  {.left-text}

- **输出**
  - |-|-|
  | -------- | ---------------------- |
  | `Float`   | 菲涅尔效应值   |

  {.left-text}

{.shortcuts .marker-round .cols-2}

<yel>**Dissolve (溶解)**</yel> - 生成溶解过渡效果

- **输入**
  - |-|-|
  | -------- | ---------------------- |
  | `Texture (sampler)` | 输入纹理  |
  | `Float`   | 溶解阈值     |

  {.left-text}

- **输出**
  - |-|-|
  | -------- | ---------------------- |
  | `Vector4` | 溶解效果输出 |

  {.left-text}

{.shortcuts .marker-round .cols-2}

### 反射 {.row-span-2}

<yel>**Reflection (反射)**</yel> - 基于表面法线方向进行反射
- **输入**
  - |-|-|
  | -------- | ---------------------- |
  | `Vector3` | 入射方向     |
  | `Vector3` | 表面法线         |

  {.left-text}

- **输出**
  - |-|-|
  | -------- | ---------------------- |
  | `Vector3` | 反射方向    |

  {.left-text}

{.shortcuts .marker-round .cols-2}



## 自定义函数节点

### 创建自定义函数节点的步骤 {.col-span-2}

- **步骤 1：在 Shader Graph 中添加自定义函数节点**

  - 在 Shader Graph 中右键单击并选择 **“Create Node”** > **“Custom Function”**。
  - 选择 **“String”**（用于内联 HLSL 代码）或 **“File”**（用于外部 HLSL 文件）。

- **步骤 2：在 Shader Graph 中配置节点**
  - 设置节点的名称。
  - 如果使用 **“File”**，请确保外部 HLSL 文件名与 HLSL 文件中定义的函数名完全匹配。这可确保在 Shader Graph 管道中正确引用该函数。
  
    <yel>**示例**</yel>：如果文件名为 `CustomFunction.hlsl`，则其中的函数也应命名为 `CustomFunction`。

- **步骤 3：在 Shader Graph 中添加输入/输出**
  - 在 Shader Graph 中为自定义函数定义所需的 `Inputs` 和 `Outputs`。这些将自动为您生成端口以连接其他节点。
  
    <yel>**示例**</yel>：
    - **输入**：`Float` (时间), `Vector3` (位置)
    - **输出**：`Vector3` (新位置)
    
    在自定义 HLSL 代码中，`in` 和 `out` 参数对应于这些输入和输出：
    - `in` 表示进入函数的数据（例如，`time`、`position`）。
    - `out` 定义返回值（例如，修改后的 `position`）。

- **步骤 4：编写 HLSL 代码**

  - 如果使用 **“String”** 选项：
    - 直接在 Shader Graph 中的自定义函数节点编辑器内编写 HLSL 代码。
    - 确保 `in` 和 `out` 参数与您在 Shader Graph 中定义的输入和输出匹配。

    - <yel>**内联代码示例**</yel> (使用 **“String”** 模式)：

      ```cpp
      float3 CustomPosition(in float time, in float3 position, out float3 newPosition) {
        newPosition = position + float3(sin(time), cos(time), 0.0);
        return newPosition;
      }
      ```
  
  - 如果使用 **“File”** 选项：
    - 在外部 `.hlsl` 文件中编写 HLSL 代码，并在 Shader Graph 中引用该文件。

    - <yel>**外部 HLSL 文件示例**</yel> (使用 **“File”** 模式)：

      1. **1. 创建一个 HLSL 文件**，名为 `CustomPosition.hlsl`。

      2. **2. 在文件中编写自定义函数**。`in` 和 `out` 参数应与 Shader Graph 输入和输出匹配。

      ```cpp
      float3 CustomPosition(in float time, in float3 position, out float3 newPosition) {
        newPosition = position + float3(sin(time), cos(time), 0.0);
        return newPosition;
      }
      ```

      3. **3. 将文件保存在您的项目目录中**，例如 `Assets/Shaders/CustomPosition.hlsl`。

      4. **4. 在 Shader Graph 中链接文件**：
       - 在自定义函数节点中，切换到 **“File”** 模式并引用 `CustomPosition.hlsl`。
  
- **步骤 5：在 Shader Graph 中使用节点**
  - 将自定义函数节点的输入端口连接到其他节点（例如 `Time` 和 `Position`），以将数据馈送到自定义函数中。
  - 连接输出端口以在 Shader Graph 管道中应用函数结果。

  - <yel>**示例管道**</yel>：

    - **输入**：`Time` (浮点型) 和 `Position` (向量)
    - **输出**：`Modified Position` (带有新位置的向量)
  
    这将使自定义节点根据着色器中的时间更新对象的位置。

{.marker-timeline .shortcuts}


## 另请参阅 {.cols-1}

- [Unity Shader Graph 文档](https://docs.unity3d.com/Manual/shader-graph-overview.html)  _(docs.unity3d.com)_  
- [Tianle Yuan 的 Unity 视觉效果笔记](https://yuantianle.github.io/11_Game_Development/Unity/)
  _(yuantianle.com)_

