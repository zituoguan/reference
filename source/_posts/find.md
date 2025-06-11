---
title: Find 命令
date: 2020-12-28 16:52:20
tags:
  - 搜索
  - 文件
  - 目录
categories:
  - Linux 命令
intro: |
  这是 Linux find 命令的快速参考备忘单，包含常用选项和示例。
plugins:
  - copyCode
---

## 入门

### 用法

```shell script
$ find [路径...] [选项] [表达式]
```

通配符

```shell script
$ find . -name "*.txt"
$ find . -name "2020*.csv"
$ find . -name "json_*"
```

---

- [正则表达式参考](/regex) _(r3f.cn)_
- [Find 命令备忘单](https://gist.github.com/gr1ev0us/3a9b9d9dbdd38f6379288eb2686fc538) _(gist.github.com)_

### 选项示例 {.col-span-2}

| 选项        | 示例                                       | 描述                                        |
| ----------- | ------------------------------------------ | ------------------------------------------- |
| `-type`     | find . -type d                             | 仅查找目录                                  |
| `-name`     | find . -type f -name "\*.txt"              | 按名称查找文件                              |
| `-iname`    | find . -type f -iname "hello"              | 按名称查找文件（不区分大小写）              |
| `-size`     | find . -size +1G                           | 查找大于 1G 的文件                          |
| `-user`     | find . -type d -user jack                  | 查找 jack 的文件                            |
| `-regex`    | find /var -regex '.\*/tmp/.\*[0-9]\*.file' | 使用正则表达式查找。参见 [regex](/regex)    |
| `-maxdepth` | find . -maxdepth 1 -name "a.txt"           | 在当前目录和子目录中                        |
| `-mindepth` | find / -mindepth 3 -maxdepth 5 -name pass  | 在子目录级别 2 和 4 之间                    |

{.show-header}

### 类型

|           |                      |
| --------- | -------------------- |
| `-type d` | 目录                 |
| `-type f` | 文件                 |
| `-type l` | 符号链接             |
| `-type b` | 缓冲块设备           |
| `-type c` | 非缓冲字符设备       |
| `-type p` | 命名管道             |
| `-type s` | 套接字               |

### 大小

|           |                           |
| --------- | ------------------------- |
| `-size b` | 512字节块 (默认)          |
| `-size c` | 字节                      |
| `-size k` | 千字节                    |
| `-size M` | 兆字节                    |
| `-size G` | 吉字节                    |
| `-size T` | 太字节 _(仅 BSD)_         |
| `-size P` | 拍字节 _(仅 BSD)_         |

### 大小 +/-

查找所有大于 10MB 的文件

```shell script
$ find / -size +10M
```

查找所有小于 10MB 的文件

```shell script
$ find / -size -10M
```

查找所有大小正好为 10M 的文件

```shell script
$ find / -size 10M
```

查找大小在 100MB 和 1GB 之间的文件

```shell script
$ find / -size +100M -size -1G
```

`+` 和 `-` 前缀通常表示大于和小于。

### 名称

在当前目录中使用名称查找文件

```shell script
$ find . -name tecmint.txt
```

在 home 目录下查找文件

```shell script
$ find /home -name tecmint.txt
```

使用名称查找文件并忽略大小写

```shell script
$ find /home -iname tecmint.txt
```

使用名称查找目录

```shell script
$ find / -type d -name tecmint
```

使用名称查找 php 文件

```shell script
$ find . -type f -name tecmint.php
```

查找目录中所有的 php 文件

```shell script
$ find . -type f -name "*.php"
```

### 权限

查找权限为 777 的文件。

```shell script
$ find . -type f -perm 0777 -print
```

查找没有权限 777 的文件。

```shell script
$ find / -type f ! -perm 777
```

查找设置了 SUID 的文件。

```shell script
$ find / -perm /u=s
```

查找设置了 SGID 的文件。

```shell script
$ find / -perm /g=s
```

查找只读文件。

```shell script
$ find / -perm /u=r
```

查找可执行文件。

```shell script
$ find / -perm /a=x
```

### 所有者和组

根据用户查找单个文件

```shell script
$ find / -user root -name tecmint.txt
```

根据用户查找所有文件

```shell script
$ find /home -user tecmint
```

根据组查找所有文件

```shell script
$ find /home -group developer
```

查找用户的特定文件

```shell script
$ find /home -user tecmint -iname "*.txt"
```

### 多个文件名

```shell script {.wrap}
$ find . -type f \( -name "*.sh" -o -name "*.txt" \)
```

查找扩展名为 `.sh` 和 `.txt` 的文件

### 多个目录

```shell script {.wrap}
$ find /opt /usr /var -name foo.scala -type f
```

在多个目录中查找文件

### 空文件/目录

```shell script
$ find . -type d -empty
```

删除目录中所有空文件

```shell script
$ find . -type f -empty -delete
```

## 按日期和时间查找

### 含义 {.col-span-2}

| 选项    | 描述                                                        |
| ------- | ----------------------------------------------------------- |
| `atime` | 访问时间 (文件上次<yel>打开</yel>的时间)                    |
| `mtime` | 修改时间 (文件<yel>内容上次修改</yel>的时间)                |
| `ctime` | 更改时间 (文件<yel>inode 上次更改</yel>的时间)              |

#### 示例

| 选项            | 描述                                                       |
| --------------- | ---------------------------------------------------------- |
| `-mtime +0`     | 修改时间在 24 小时以前                                     |
| `-mtime 0`      | 修改时间在现在和 1 天以前之间                              |
| `-mtime -1`     | 修改时间在 1 天以内 (与 `-mtime 0` 相同)                   |
| `-mtime 1`      | 修改时间在 24 小时和 48 小时以前之间                       |
| `-mtime +1`     | 修改时间在 48 小时以前                                     |
| `-mtime +1w`    | 上次修改时间在 1 周以前                                    |
| `-atime 0`      | 上次访问时间在现在和 24 小时以前之间                       |
| `-atime +0`     | 访问时间在 24 小时以前                                     |
| `-atime 1`      | 访问时间在 24 小时和 48 小时以前之间                       |
| `-atime +1`     | 访问时间在 48 小时以前                                     |
| `-atime -1`     | 访问时间在 24 小时以内 (与 `-atime 0` 相同)                |
| `-ctime -6h30m` | 文件状态在过去 6 小时 30 分钟内更改                        |

### 示例

查找过去 50 天内修改的文件

```shell script
$ find / -mtime 50
```

查找过去 50 天内访问的文件

```shell script
$ find / -atime 50
```

查找过去 50-100 天内修改的文件

```shell script
$ find / -mtime +50 –mtime -100
```

查找过去 1 小时内更改的文件

```shell script
$ find / -cmin -60
```

查找过去 1 小时内修改的文件

```shell script
$ find / -mmin -60
```

查找过去 1 小时内访问的文件

```shell script
$ find / -amin -60
```

## 查找并执行操作 {.cols-2}

### 查找并删除 {.row-span-2}

查找并删除多个文件

```shell script
$ find . -type f -name "*.mp3" -exec rm -f {} \;
```

查找并删除单个文件

```shell script
$ find . -type f -name "tecmint.txt" -exec rm -f {} \;
```

查找并删除 100mb 的文件

```shell script
$ find / -type f -size +100m -exec rm -f {} \;
```

查找特定文件并删除

```shell script
$ find / -type f -name *.mp3 -size +10m -exec rm {} \;
```

### 查找并替换

查找所有文件并将内容中的 `const` 替换为 `let`

```shell script {.wrap}
$ find ./ -type f -exec sed -i 's/const/let/g' {} \;
```

查找可读写文件并将内容中的 `old` 替换为 `new`

```shell script {.wrap}
$ find ./ -type f -readable -writable -exec sed -i "s/old/new/g" {} \;
```

另请参阅：[sed 备忘单](/sed)

### 查找并重命名

查找并添加后缀（添加 `.bak`）

```shell script {.wrap}
$ find . -type f -name 'file*' -exec mv {} {}.bak\;
```

查找并重命名扩展名（`.html` => `.gohtml`）

```shell script {.wrap}
$ find ./ -depth -name "*.html" -exec sh -c 'mv "$1" "${1%.html}.gohtml"' _ {} \;
```

### 查找并移动

```shell script
$ find . -name '*.mp3' -exec mv {} /tmp/music \;
```

查找并将其移动到特定目录 (`/tmp/music`)

### 查找并复制

```shell script
$ find . -name '*2020*.xml' -exec cp -r "{}" /tmp/backup \;
```

查找匹配的文件并复制到特定目录 (`/tmp/backup`)

### 查找并连接

将下载目录中的所有 csv 文件合并到 `merged.csv`

```shell script
$ find download -type f -iname '*.csv' | xargs cat > merged.csv
```

将下载目录中所有已排序的 csv 文件合并到 `merged.csv`

```shell script {.wrap}
$ find download -type f -iname '*.csv' | sort | xargs cat > merged.csv
```

### 查找并排序

查找并按升序排序

```shell script
$ find . -type f | sort
```

查找并按降序排序

```shell script
$ find . -type f | sort -r
```

### 查找并修改权限 (chmod) {.row-span-1}

查找文件并将权限设置为 644。

```shell script
$ find / -type f -perm 0777 -print -exec chmod 644 {} \;
```

查找目录并将权限设置为 755。

```shell script
$ find / -type d -perm 777 -print -exec chmod 755 {} \;
```

### 查找并压缩

查找所有 `.java` 文件并将其压缩为 `java.tar`

```shell script
$ find . -type f -name "*.java" | xargs tar cvf java.tar
```

查找所有 `.csv` 文件并将其压缩为 `r3f.cn`

```shell script
$ find . -type f -name "*.csv" | xargs zip r3f.cn
```
