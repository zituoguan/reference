---
title: PyTorch
date: 2023-04-12
background: bg-[#ee4c2c]
tags:
  - AI
  - Python
categories:
  - 其他
intro: 这是 PyTorch 的快速参考备忘单列表。另请参阅 [PyTorch 网站](https://pytorch.org/)
---

## 导入 { .cols-1 }

### 通用

```
import torch                                        # 根包
from torch.utils.data import Dataset, DataLoader    # 数据集表示和加载
```

### 神经网络 API

```
import torch.autograd as autograd         # 计算图
from torch import Tensor                  # 计算图中的张量节点
import torch.nn as nn                     # 神经网络
import torch.nn.functional as F           # 层、激活函数等
import torch.optim as optim               # 优化器，例如梯度下降、ADAM 等
from torch.jit import script, trace       # 混合前端装饰器和跟踪 JIT
```

### Torchscript 和 JIT

```
torch.jit.trace()         # 获取你的模块或函数以及一个示例
                          # 数据输入，并跟踪数据在模型中传播时
                          #遇到的计算步骤

@script                   # 用于指示正在跟踪的代码中
                          # 存在数据依赖控制流的装饰器
```

### ONNX

```
torch.onnx.export(model, dummy data, xxxx.proto)       # 使用训练好的模型、虚拟数据
                                                       # 和所需的文件名导出 ONNX 格式的模型

model = onnx.load("alexnet.proto")                     # 加载 ONNX 模型
onnx.checker.check_model(model)                        # 检查模型 IR
                                                       # 是否格式良好

onnx.helper.printable_graph(model.graph)               # 打印图的人类可读
                                                       # 表示形式
```

### 视觉

```
from torchvision import datasets, models, transforms     # 视觉数据集、
                                                         # 架构和转换

import torchvision.transforms as transforms              # 可组合的转换
```

### 分布式训练

```
import torch.distributed as dist             # 分布式通信
from torch.multiprocessing import Process    # 内存共享进程
```

## 张量 { .cols-1 }

### 创建

```
x = torch.randn(*size)              # 具有独立 N(0,1) 条目的张量
x = torch.[ones|zeros](*size)       # 全为 1 [或 0] 的张量
x = torch.tensor(L)                 # 从 [嵌套] 列表或 ndarray L 创建张量
y = x.clone()                       # x 的克隆
with torch.no_grad():               # 停止 autograd 跟踪张量历史记录的代码块
requires_grad=True                  # 参数，设置为 True 时，跟踪计算
                                    # 历史记录以用于将来的导数计算
```

### 维度

```
x.size()                                  # 返回类似元组的维度对象
x = torch.cat(tensor_seq, dim=0)          # 沿维度 dim 连接张量
y = x.view(a,b,...)                       # 将 x 重塑为大小 (a,b,...)
y = x.view(-1,a)                          # 将 x 重塑为大小 (b,a)，其中 b 为某个值
y = x.transpose(a,b)                      # 交换维度 a 和 b
y = x.permute(*dims)                      # 排列维度
y = x.unsqueeze(dim)                      # 添加了轴的张量
y = x.unsqueeze(dim=2)                    # (a,b,c) 张量 -> (a,b,1,c) 张量
y = x.squeeze()                           # 移除所有大小为 1 的维度 (a,1,b,1) -> (a,b)
y = x.squeeze(dim=1)                      # 移除指定的大小为 1 的维度 (a,1,b,1) -> (a,b,1)
```

### 代数

```
ret = A.mm(B)       # 矩阵乘法
ret = A.mv(x)       # 矩阵向量乘法
x = x.t()           # 矩阵转置
```

### GPU 使用

```
torch.cuda.is_available                                     # 检查 CUDA 是否可用
x = x.cuda()                                                # 将 x 的数据从 CPU 移动到
                                                            # GPU 并返回新对象

x = x.cpu()                                                 # 将 x 的数据从 GPU 移动到 CPU
                                                            # 并返回新对象

if not args.disable_cuda and torch.cuda.is_available():     # 设备无关的代码
    args.device = torch.device('cuda')                      # 和模块化
else:                                                       #
    args.device = torch.device('cpu')                       #

net.to(device)                                              # 递归地将其参数和缓冲区
                                                            # 转换为特定于设备的张量

x = x.to(device)                                            # 将张量复制到设备
                                                            # (gpu, cpu)
```

### 深度学习

```
nn.Linear(m,n)                                # 从 m 到 n 个单元的全连接层

nn.ConvXd(m,n,s)                              # X 维卷积层，从 m 到 n 个通道，
                                              # 其中 X⍷{1,2,3}，核大小为 s

nn.MaxPoolXd(s)                               # X 维池化层
                                              # (符号同上)

nn.BatchNormXd                                # 批量归一化层
nn.RNN/LSTM/GRU                               # 循环层
nn.Dropout(p=0.5, inplace=False)              # 适用于任何维度输入的 dropout 层
nn.Dropout2d(p=0.5, inplace=False)            # 二维通道级 dropout
nn.Embedding(num_embeddings, embedding_dim)   # 从索引到嵌入向量的
                                              # (张量级) 映射
```

### 损失函数

```
nn.X                                  # 其中 X 是 L1Loss, MSELoss, CrossEntropyLoss
                                      # CTCLoss, NLLLoss, PoissonNLLLoss,
                                      # KLDivLoss, BCELoss, BCEWithLogitsLoss,
                                      # MarginRankingLoss, HingeEmbeddingLoss,
                                      # MultiLabelMarginLoss, SmoothL1Loss,
                                      # SoftMarginLoss, MultiLabelSoftMarginLoss,
                                      # CosineEmbeddingLoss, MultiMarginLoss,
                                      # 或 TripletMarginLoss
```

### 激活函数

```
nn.X                                  # 其中 X 是 ReLU, ReLU6, ELU, SELU, PReLU, LeakyReLU,
                                      # RReLu, CELU, GELU, Threshold, Hardshrink, HardTanh,
                                      # Sigmoid, LogSigmoid, Softplus, SoftShrink,
                                      # Softsign, Tanh, TanhShrink, Softmin, Softmax,
                                      # Softmax2d, LogSoftmax 或 AdaptiveSoftmaxWithLoss
```

### 优化器

```
opt = optim.x(model.parameters(), ...)      # 创建优化器
opt.step()                                  # 更新权重
optim.X                                     # 其中 X 是 SGD, Adadelta, Adagrad, Adam,
                                            # AdamW, SparseAdam, Adamax, ASGD,
                                            # LBFGS, RMSprop 或 Rprop
```

### 学习率调度

```
scheduler = optim.X(optimizer,...)      # 创建学习率调度器
scheduler.step()                        # 在优化器更新权重后更新学习率
optim.lr_scheduler.X                    # 其中 X 是 LambdaLR, MultiplicativeLR,
                                        # StepLR, MultiStepLR, ExponentialLR,
                                        # CosineAnnealingLR, ReduceLROnPlateau, CyclicLR,
                                        # OneCycleLR, CosineAnnealingWarmRestarts,
```

## 数据工具 { .cols-1 }

### 数据集

```
Dataset                    # 表示数据集的抽象类
TensorDataset              # 张量形式的带标签数据集
Concat Dataset             # 数据集的串联
```

### 数据加载器和数据采样器

```
DataLoader(dataset, batch_size=1, ...)      # 加载数据批次，与单个
                                            # 数据点的结构无关

sampler.Sampler(dataset,...)                # 处理从数据集中采样方式的
                                            # 抽象类

sampler.XSampler where ...                  # Sequential, Random, SubsetRandom,
                                            # WeightedRandom, Batch, Distributed
```
