---
title: IntelliJ IDEA
date: 2020-12-17 21:51:44
background:
  bg-gradient-to-r from-pink-500 via-violet-400 to-blue-400 hover:from-pink-700 hover:via-violet-600 hover:to-blue-500
tags:
  - jetbrains
  - java
  - 快捷键
categories:
  - 键盘快捷键
intro: |
  IntelliJ IDEA 是一款非常优秀的 Java IDE，它的大多数命令都有快捷键，让您的双手无需离开键盘即可操作。
---

## IDEA Windows 和 Linux 快捷键映射

### 编辑 {.row-span-5}

| 快捷键                     | 描述                                             |
| -------------------------- | :----------------------------------------------- |
| `Ctrl` `Space`             | 基本代码补全                                     |
| `Ctrl` `Shift` `Space`     | 智能代码补全                                     |
| `Ctrl` `Shift` `Enter`     | 完成语句                                         |
| `Ctrl` `P`                 | 参数信息                                         |
| `Ctrl` `Q`                 | 快速文档查询                                     |
| `Shift` `F1`               | 外部文档                                         |
| `Ctrl` `hover`             | 简要信息                                         |
| `Ctrl` `F1`                | 光标处错误或警告提示                             |
| `Alt` `Insert`             | 生成代码                                         |
| `Ctrl` `O`                 | 覆盖方法                                         |
| `Ctrl` `I`                 | 实现方法                                         |
| `Ctrl` `Alt` `T`           | 代码环绕                                         |
| `Ctrl` `/`                 | 注释/取消注释行                                  |
| `Ctrl` `Shift` `/`         | 注释/取消注释块                                  |
| `Ctrl` `W`                 | 连续选中递增的代码块                             |
| `Ctrl` `Shift` `W`         | 将当前选中范围缩小到上一个状态                   |
| `Alt` `Q`                  | 上下文信息                                       |
| `Alt` `Enter`              | 显示意图操作和快速修复                           |
| `Ctrl` `Alt` `L`           | 重新格式化代码                                   |
| `Ctrl` `Alt` `O`           | 优化导入                                         |
| `Ctrl` `Alt` `I`           | 自动缩进行                                       |
| `Tab`                      | 缩进选中行                                       |
| `Shift` `Tab`              | 取消缩进选中行                                   |
| `Ctrl` `X`                 | 剪切当前行或选中块到剪贴板                       |
| `Ctrl` `C`                 | 复制当前行或选中块到剪贴板                       |
| `Ctrl` `V`                 | 从剪贴板粘贴                                     |
| `Ctrl` `Shift` `V`         | 从最近的缓冲区粘贴                               |
| `Ctrl` `D`                 | 复制当前行或选中块                               |
| `Ctrl` `Y`                 | 删除光标所在行                                   |
| `Ctrl` `Shift` `J`         | 智能行合并                                       |
| `Ctrl` `Enter`             | 智能行拆分                                       |
| `Shift` `Enter`            | 开始新行                                         |
| `Ctrl` `Shift` `U`         | 切换光标处单词或选中块的大小写                   |
| `Ctrl` `Shift` `]` _/_ `[` | 选中至代码块结束/开始                            |
| `Ctrl` `Backspace`         | 删除至单词结束/开始                              |
| `Ctrl` `+` _/_ `-`         | 展开/折叠代码块                                  |
| `Ctrl` `Shift` `+`         | 全部展开                                         |
| `Ctrl` `Shift` `-`         | 全部折叠                                         |
| `Ctrl` `F4`                | 关闭当前编辑器标签页                             |

{.shortcuts}

### 用法搜索

| 快捷键                     | 描述                               |
| -------------------------- | :--------------------------------- |
| `Alt` `F7` _/_ `Ctrl` `F7` | 查找用法/在文件中查找用法          |
| `Ctrl` `Shift` `F7`        | 高亮文件中的用法                   |
| `Ctrl` `Alt` `F7`          | 显示用法                           |

{.shortcuts}

### 导航 {.row-span-4}

| 快捷键                          | 描述                                      |
| ------------------------------- | :---------------------------------------- |
| `Ctrl` `N`                      | 转到类                                    |
| `Ctrl` `Shift` `N`              | 转到文件                                  |
| `Ctrl` `Alt` `Shift` `N`        | 转到符号                                  |
| `Alt` `Right` _/_ `Left`        | 转到下一个/上一个编辑器标签页             |
| `F12`                           | 返回上一个工具窗口                        |
| `Esc`                           | 转到编辑器                                |
| `Shift` `Esc`                   | 隐藏活动窗口或上一个活动窗口              |
| `Ctrl` `Shift` `F4`             | 关闭活动的运行、消息等窗口                |
| `Ctrl` `G`                      | 转到行                                    |
| `Ctrl` `E`                      | 最近文件弹窗                              |
| `Ctrl` `Alt` `Left` _/_ `Right` | 向后/向前导航                             |
| `Ctrl` `Shift` `Backspace`      | 导航到上次编辑位置                        |
| `Alt` `F1`                      | 在任何视图中选择当前文件或符号            |
| `Ctrl` `B` _/_ `Ctrl` `Click`   | 转到声明                                  |
| `Ctrl` `Alt` `B`                | 转到实现                                  |
| `Ctrl` `Shift` `I`              | 打开快速定义查找                          |
| `Ctrl` `Shift` `B`              | 转到类型声明                              |
| `Ctrl` `U`                      | 转到父方法/父类                           |
| `Alt` `Up` _/_ `Down`           | 转到上一个/下一个方法                     |
| `Ctrl` `]/[`                    | 移动到代码块结束/开始                     |
| `Ctrl` `F12`                    | 文件结构弹窗                              |
| `Ctrl` `H`                      | 类型层级                                  |
| `Ctrl` `Shift` `H`              | 方法层级                                  |
| `Ctrl` `Alt` `H`                | 调用层级                                  |
| `F2` _/_ `Shift` `F2`           | 下一个/上一个高亮错误                     |
| `F4` _/_ `Ctrl` `Enter`         | 编辑源码/查看源码                         |
| `Alt` `Home`                    | 显示导航栏                                |
| `F11`                           | 切换书签                                  |
| `Ctrl` `F11`                    | 使用助记符切换书签                        |
| `Ctrl` `0...9`                  | 转到编号书签                              |
| `Shift` `F11`                   | 显示书签                                  |

{.shortcuts}

### 搜索/替换

| 快捷键             | 描述                        |
| ------------------ | :-------------------------- |
| `Double Shift`     | 全局搜索                    |
| `Ctrl` `F`         | 查找                        |
| `F3` `Shift` `F3`  | 查找下一个/查找上一个       |
| `Ctrl` `R`         | 替换                        |
| `Ctrl` `Shift` `F` | 在路径中查找                |
| `Ctrl` `Shift` `R` | 在路径中替换                |

{.shortcuts}

### 动态模板

| 快捷键           | 描述                                              |
| ---------------- | :------------------------------------------------ |
| `Ctrl` `Alt` `J` | 使用动态模板环绕                                  |
| `Ctrl` `J`       | 插入动态模板                                      |
| `iter`           | 根据 Java SDK 1.5 风格迭代                        |
| `inst`           | 使用 instanceof 检查对象类型并向下转型            |
| `itco`           | 迭代 java.util.Collection 的元素                  |
| `itit`           | 迭代 java.util.Iterator 的元素                    |
| `itli`           | 迭代 java.util.List 的元素                        |
| `psf`            | public static final                               |
| `thr`            | throw new                                         |

{.shortcuts}

### 重构

| 快捷键           | 描述              |
| ---------------- | :---------------- |
| `F5`             | 复制              |
| `F6`             | 移动              |
| `Alt` `Delete`   | 安全删除          |
| `Shift` `F6`     | 重命名            |
| `Ctrl` `F6`      | 更改签名          |
| `Ctrl` `Alt` `N` | 内联              |
| `Ctrl` `Alt` `M` | 提取方法          |
| `Ctrl` `Alt` `V` | 提取变量          |
| `Ctrl` `Alt` `F` | 提取字段          |
| `Ctrl` `Alt` `C` | 提取常量          |
| `Ctrl` `Alt` `P` | 提取参数          |

{.shortcuts}

### 调试

| 快捷键                        | 描述                     |
| ----------------------------- | :----------------------- |
| `F8/F7`                       | 单步跳过/单步进入        |
| `Shift` `F7` _/_ `Shift` `F8` | 智能单步进入/单步跳出    |
| `Alt` `F9`                    | 运行到光标处             |
| `Alt` `F8`                    | 表达式求值               |
| `F9`                          | 恢复程序                 |
| `Ctrl` `F8`                   | 切换断点                 |
| `Ctrl` `Shift` `F8`           | 查看断点                 |

{.shortcuts}

### 编译和运行

| 快捷键                       | 描述                                     |
| ---------------------------- | :--------------------------------------- |
| `Ctrl` `F9`                  | 构建项目                                 |
| `Ctrl` `Shift` `F9`          | 编译选中的文件、包或模块                 |
| `Alt` `Shift` `F10` _/_ `F9` | 选择配置并运行/调试                      |
| `Shift` `F10` _/_ `F9`       | 运行/调试                                |
| `Ctrl` `Shift` `F10`         | 从编辑器运行上下文配置                   |

{.shortcuts}

### VCS/本地历史

| 快捷键              | 描述                  |
| ------------------- | :-------------------- |
| `Ctrl` `K`          | 提交项目到 VCS        |
| `Ctrl` `T`          | 从 VCS 更新           |
| `Alt` `Shift` `C`   | 查看最近更改          |
| `Alt` <kbd>\`</kbd> | VCS 操作弹窗          |

{.shortcuts}

### 通用

| 快捷键                   | 描述                           |
| ------------------------ | :----------------------------- |
| `Alt` `0...9`            | 打开对应的工具窗口             |
| `Ctrl` `S`               | 全部保存                       |
| `Ctrl` `Alt` `Y`         | 同步                           |
| `Ctrl` `Shift` `F12`     | 切换最大化编辑器               |
| `Alt` `Shift` `F`        | 添加到收藏夹                   |
| `Alt` `Shift` `I`        | 检查当前文件                   |
| `Ctrl` <kbd>\`</kbd>     | 快速切换当前方案               |
| `Ctrl` `Alt` `S`         | 打开设置对话框                 |
| `Ctrl` `Alt` `Shift` `S` | 打开项目结构对话框             |
| `Ctrl` `Shift` `A`       | 查找操作                       |
| `Ctrl` `Tab`             | 在工具和标签页之间切换         |

{.shortcuts}

