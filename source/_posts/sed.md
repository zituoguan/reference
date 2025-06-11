---
title: Sed 命令
date: 2020-12-27 18:34:08
background: bg-red-400
tags:
  - 编辑器
  - 替换
  - 文本
  - 实用工具
categories:
  - Linux 命令
intro: |
  [Sed](https://www.gnu.org/software/sed/manual/sed.html) 是一个流编辑器，这份 sed 速查表包含 sed 命令和一些常用的 sed 技巧。
plugins:
  - copyCode
---

## 入门指南

### Sed 用法

语法

```shell script
$ sed [选项] 命令 [输入文件]
```

使用管道

```shell script
$ cat report.txt | sed 's/Nick/John/g'
```

```shell script
$ echo '123abc' | sed 's/[0-9]+//g'
```

### 选项示例 {.col-span-2}

| 选项   | 示例                                       | 描述                             |
| ------ | ------------------------------------------ | --------------------------------------- |
| `-i`   | sed -ibak 's/On/Off/' php.ini              | 备份并直接修改输入文件   |
| `-E`   | sed -E 's/[0-9]+//g' input-file            | 使用扩展正则表达式        |
| `-n`   | sed -n '3 p' config.conf                   | 禁止默认模式空间打印 |
| `-f`   | sed -f script.sed config.conf              | 执行 sed 脚本文件                 |
| `-e`   | sed -e 'command1' -e 'command2' input-file | 执行多个 sed 命令           |

{.show-header}

### 多个命令

```shell script {.wrap}
$ echo "hello world" | sed -e 's/h/H/g' -e 's/w/W/g'
Hello World
```

使用 `-e` 执行多个 sed 命令

### Sed 脚本

```shell script
$ echo 's/h/H/g' >> hello.sed
$ echo 's/w/W/g' >> hello.sed
$ echo "hello world" | sed -f hello.sed
Hello World
```

使用 `-f` 执行 sed 脚本文件

### 示例

```shell script
$ sed 's/old/new/g' file.txt
$ sed 's/old/new/g' file.txt > new.txt

$ sed 's/old/new/g' -i file.txt
$ sed 's/old/new/g' -i.backup file.txt
```

参见：[Sed 示例](#sed-examples)

## Sed 命令

### 命令 {.col-span-2}

| 命令 | 示例                                | 描述                 |
| ------- | -------------------------------------- | --------------------------- |
| `p`     | sed -n '1,4 p' input.txt               | 打印第 1-4 行             |
| `p`     | sed -n -e '1,4 p' -e '6,7 p' input.txt | 打印第 1-4 行和第 6-7 行     |
| `d`     | sed '1,4 d' input.txt                  | 打印除第 1-4 行外的所有行      |
| `w`     | sed -n '1,4 w output.txt' input.txt    | 将模式空间写入文件 |
| `a`     | sed '2 a new-line' input.txt           | 在指定行后追加行           |
| `i`     | sed '2 i new-line' input.txt           | 在指定行前插入行           |

{.show-header}

### 空间命令

| 命令 | 描述                                                  |
| ------- | ------------------------------------------------------------ |
| `n`     | 打印模式空间，清空模式空间，并读取下一行 |
| `x`     | 交换模式空间与保持空间的内容                           |
| `h`     | 将模式空间复制到保持空间                           |
| `H`     | 将模式空间追加到保持空间                           |
| `g`     | 将保持空间复制到模式空间                           |
| `G`     | 将保持空间追加到模式空间                           |

另请参阅：[文件行距](#file-spacing)

### 标志

```shell script
$ sed 's/old/new/[标志]' [输入文件]
```

---

| 标志     | 描述                                |
| -------- | ------------------------------------------ |
| `g`      | 全局替换                        |
| `1,2...` | 替换第 n 次出现的内容              |
| `p`      | 仅打印被替换的行            |
| `w`      | 仅将被替换的行写入文件  |
| `I`      | 搜索时忽略大小写                |
| `e`      | 在命令行中替换并执行 |

### 循环命令

| 命令   | 描述                                                        |
| --------- | ------------------------------------------------------------------ |
| `b 标签` | 跳转到标签（用于循环）                                    |
| `t 标签` | 仅在成功替换后跳转到标签<br>（用于循环） |
| `:标签`  | b 和 t 命令的标签（用于循环）                       |
| `N`       | 将下一行追加到模式空间                                  |
| `P`       | 打印多行模式中的第一行                                       |
| `D`       | 删除多行模式中的第一行                                       |

### 其他标志

| 标志                      | 描述                                                                  |
| ------------------------- | ---------------------------------------------------------------------------- |
| <code>/ \| ^ @ ! #</code> | 替换分隔符可以是任意字符                                  |
| `&`                       | 获取匹配的模式                                                     |
| `( ) \1 \2 \3`            | 使用 `(` 和 `)`进行分组。<br>在替换中使用 `\1`、`\2` 引用分组 |

## Sed 示例

### 替换文本 {.row-span-2}

替换字符串的所有出现

```shell script
$ sed 's/old/new/g' file.txt
```

仅替换字符串的第 n 次出现

```shell script
$ sed 's/old/new/2' file.txt
```

仅在第 5 行替换字符串

```shell script
$ sed '5 s/old/new/' file.txt
```

将 "world" 替换为 "universe"，但仅当行以 "hello" 开头时

```shell script
$ sed '/hello/s/world/universe/' file.txt
```

移除每行末尾的 "\"

```shell script
$ sed 's/\\$//' file.txt
```

移除每行开头的所有空白字符

```shell script
$ sed 's/^\s*//' file.txt
```

移除注释。即使是行尾的注释

```shell script
$ sed 's/#.*$//' file.txt
```

### 搜索文本

搜索字符串并仅打印匹配的行

```shell script
$ sed -n '/hello/p' file.txt
```

不区分大小写搜索

```shell script
$ sed -n '/hello/Ip' file.txt
```

搜索字符串但仅输出不匹配的行

```shell script
$ sed -n '/hello/!p' file.txt
```

### 追加行

在第 2 行后追加行

```shell script
$ sed '2a 第 2 行后的文本' file.txt
```

在文件末尾追加行

```shell script
$ sed '$a 文件结束！' file.txt
```

从第 3 行开始，每隔 3 行追加一行

```shell script
$ sed '3~3a 一些文本' file.txt
```

### 行号操作 {.col-span-2}

给文件行编号（简单左对齐）

```shell script
$ sed = file.txt | sed 'N;s/\n/\t/'
```

给文件行编号（数字在左侧，右对齐）

```shell script
$ sed = file.txt | sed 'N; s/^/   /; s/ *\(.\{6,\}\)\n/\1  /'
```

给文件行编号，但仅当行不为空时打印数字

```shell script
$ sed '/./=' file.txt | sed '/./N; s/\n/ /'
```

计算行数（模拟 "wc -l"）

```shell script
$ sed -n '$='
```

### 前插行

在第 5 行前插入文本

```shell script
$ sed '5i 第五行' file.txt
```

在包含 "hello" 的每一行前插入 "示例： "

```shell script
$ sed '/hello/i 示例： ' file.txt
```

### 删除行

删除文件中的第 5-7 行

```shell script
$ sed '5,7d' file.txt
```

从第 3 行开始，每隔 2 行删除一行

```shell script
$ sed '3~2d' file.txt
```

删除文件中的最后一行

```shell script
$ sed '$d' file.txt
```

删除以 "Hello" 开头的行

```shell script
$ sed '/^Hello/d' file.txt
```

删除所有空行

```shell script
$ sed '/^$/d' file.txt
```

删除以 "#" 开头的行

```shell script
$ sed '/^#/d' file.txt
```

### 文件行距

双倍行距

```shell script
$ sed G
```

删除所有空行并双倍行距

```shell script
$ sed '/^$/d;G'
```

三倍行距文件

```shell script
$ sed 'G;G'
```

取消双倍行距

```shell script
$ sed 'n;d'
```

在匹配 "regex" 的行上方插入一个空行

```shell script
$ sed '/regex/{x;p;x;}'
```

在匹配 "regex" 的行下方插入一个空行

```shell script
$ sed '/regex/G'
```

在匹配 "regex" 的行上下各插入一个空行

```shell script
$ sed '/regex/{x;p;x;G;}'
```

## 另请参阅 {.cols-1}

- [sed 速查表](https://gist.github.com/ssstonebraker/6140154) _(gist.github.com)_
