---
title: Awk
date: 2020-12-31 15:18:34
background: bg-slate-600
tags:
    - bash
    - text
    - script
categories:
    - Linux 命令
intro: |
    这是一份 [GNU awk](https://www.gnu.org/software/gawk/manual/gawk.html) 的单页快速参考备忘单，涵盖了常用的 awk 表达式和命令。
plugins:
    - copyCode
---

## 入门

### 试一试

```shell script {.wrap}
$ awk -F: '{print $1, $NF}' /etc/passwd
```

---

| -             | -                         |
| ------------- | ------------------------- |
| `-F:`         | 使用冒号作为分隔符      |
| `{...}`       | Awk 程序               |
| `print`       | 打印当前记录 |
| `$1`          | 第一个字段               |
| `$NF`         | 最后一个字段                |
| `/etc/passwd` | 输入数据文件           |

{.left-text}

### Awk 程序

```
BEGIN          {<初始化>}
     <模式 1> {<程序动作>}
     <模式 2> {<程序动作>}
     ...
END            {< 最终动作 >}
```

#### 示例

```
awk '
        BEGIN { print "\n>>>开始" }
        !/(login|shutdown)/ { print NR, $0 }
        END { print "<<<结束\n" }
' /etc/passwd
```

### 变量 {.row-span-2}

```bash
                    $1      $2/$(NF-1)    $3/$NF
                     ▼          ▼           ▼
                ┌──────┬──────────────────┬───────┐
$0/NR ▶ │  ID  │  网站         │  URI  │
                ├──────┼──────────────────┼───────┤
$0/NR ▶ │  1   │  r3f.cn │  awk  │
                ├──────┼──────────────────┼───────┤
$0/NR ▶ │  2   │  google.com      │  25   │
                └──────┴──────────────────┴───────┘
```

---

```
# 第一个和最后一个字段
awk -F: '{print $1,$NF}' /etc/passwd

# 带行号
awk -F: '{print NR, $0}' /etc/passwd

# 倒数第二个字段
awk -F: '{print $(NF-1)}' /etc/passwd

# 自定义字符串
awk -F: '{print $1 "=" $6}' /etc/passwd
```

参见：[Awk 变量](#awk-variables)

### Awk 程序示例 {.col-span-2 .row-span-2}

```
awk 'BEGIN {print "hello world"}'        # 打印 "hello world"
awk -F: '{print $1}' /etc/passwd         # -F: 指定字段分隔符

# /模式/ 仅对匹配的模式执行操作
awk -F: '/root/ {print $1}' /etc/passwd

# BEGIN 块在开始时执行一次
awk -F: 'BEGIN { print "uid"} { print $1 }' /etc/passwd

# END 块在结束时执行一次
awk -F: '{print $1} END { print "-完成-"}' /etc/passwd
```

### 条件

```
awk -F: '$3>30 {print $1}' /etc/passwd
```

参见：[Awk 条件](#awk-conditions)

### 生成 1000 个空格

```
awk 'BEGIN{
        while (a++ < 1000)
                s=s " ";
        print s
}'
```

参见：[Awk 循环](#awk-loops)

### 数组

```
awk 'BEGIN {
     fruits["mango"] = "yellow";
     fruits["orange"] = "orange"
     for(fruit in fruits) {
         print "The color of " fruit " is " fruits[fruit]
     }
}'
```

参见：[Awk 数组](#awk-arrays)

### 函数

```
# => 5
awk 'BEGIN{print length("hello")}'
# => HELLO
awk 'BEGIN{print toupper("hello")}'
# => hel
awk 'BEGIN{print substr("hello", 1, 3)}'
```

参见：[Awk 函数](#awk-functions)

## Awk 变量

### 内置变量

| -              | -                                                   |
| -------------- | --------------------------------------------------- |
| `$0`           | 整行                                          |
| `$1, $2...$NF` | 第一个、第二个…最后一个字段                           |
| `NR`           | 记录`N`umber of `R`ecords                               |
| `NF`           | 字段`N`umber of `F`ields                                |
| `OFS`          | 输出`O`utput `F`ield `S`eparator <br> _(默认为 " ")_   |
| `FS`           | 输入`F`ield `S`eparator <br> _(默认为 " ")_      |
| `ORS`          | 输出`O`utput `R`ecord `S`eparator <br> _(默认为 "\n")_ |
| `RS`           | 输入`R`ecord `S`eparator <br> _(默认为 "\n")_    |
| `FILENAME`     | 文件名                                    |

### 表达式

| -                   | -                                  |
| ------------------- | ---------------------------------- |
| `$1 == "root"`      | 第一个字段等于 root            |
| `{print $(NF-1)}`   | 倒数第二个字段                  |
| `NR!=1{print $0}`   | 从第二条记录开始                    |
| `NR > 3`            | 从第四条记录开始                    |
| `NR == 1`           | 第一条记录                       |
| `END{print NR}`     | 总记录数                      |
| `BEGIN{print OFMT}` | 输出格式                      |
| `{print NR, $0}`    | 行号                        |
| `{print NR "	" $0}`  | 行号 (制表符)                  |
| `{$1 = NR; print}`  | 用行号替换第一个字段 |
| `$NF > 4`           | 最后一个字段 > 4                     |
| `NR % 2 == 0`       | 偶数记录                       |
| `NR==10, NR==20`    | 记录 10 到 20                   |
| `BEGIN{print ARGC}` | 总参数个数                    |
| `ORS=NR%5?",":"\n"` | 连接记录                |

### 示例

打印总和与平均值

```
awk -F: '{sum += $3}
         END { print sum, sum/NR }
' /etc/passwd
```

打印参数

```
awk 'BEGIN {
        for (i = 1; i < ARGC; i++)
                print ARGV[i] }' a b c
```

输出字段分隔符为逗号

```
awk 'BEGIN { FS=":";OFS=","}
        {print $1,$2,$3,$4}' /etc/passwd
```

匹配位置

```
awk 'BEGIN {
        if (match("One Two Three", "Tw"))
                print RSTART }'
```

匹配长度

```
awk 'BEGIN {
        if (match("One Two Three", "re"))
                print RLENGTH }'
```

### 环境变量

| -         | -                                                         |
| --------- | --------------------------------------------------------- |
| `ARGC`    | 参数数量                                       |
| `ARGV`    | 参数数组                                        |
| `FNR`     | 文件`F`ile `N`umber of `R`ecords                              |
| `OFMT`    | 数字格式 <br> _(默认为 "%.6g")_                |
| `RSTART`  | 字符串中的位置                                    |
| `RLENGTH` | 匹配长度                                           |
| `SUBSEP`  | 多维数组分隔符 <br> _(默认为 "\034")_ |
| `ARGIND`  | 参数索引                                        |

### 仅 GNU awk

| -             | -                     |
| ------------- | --------------------- |
| `ENVIRON`     | 环境变量 |
| `IGNORECASE`  | 忽略大小写           |
| `CONVFMT`     | 转换格式     |
| `ERRNO`       | 系统错误         |
| `FIELDWIDTHS` | 固定宽度字段    |

### 定义变量

```
awk -v var1="Hello" -v var2="Wold" '
        END {print var1, var2}
' </dev/null
```

#### 使用 shell 变量

```
awk -v varName="$PWD" '
        END {print varName}' </dev/null
```

## Awk 运算符

### 运算符

| -                | -           |
| ---------------- | ----------- |
| `{print $1}`     | 第一个字段 |
| `$2 == "foo"`    | 等于      |
| `$2 != "foo"`    | 不等于  |
| `"foo" in array` | 在数组中    |

#### 正则表达式

| -               | -                 |
| --------------- | ----------------- |
| `/regex/`       | 行匹配      |
| `!/regex/`      | 行不匹配  |
| `$1 ~ /regex/`  | 字段匹配     |
| `$1 !~ /regex/` | 字段不匹配 |

#### 更多条件

| -                        | -   |
| ------------------------ | --- |
| `($2 <= 4 \|\| $3 < 20)` | 或  |
| `($1 == 4 && $3 < 20)`   | 与 |

### 操作

#### 算术运算

- `+`
- `-`
- `*`
- `/`
- `%`
- `++`
- `--`

{.cols-3 .marker-none}

#### 简写赋值

- `+=`
- `-=`
- `*=`
- `/=`
- `%=`

{.cols-3 .marker-none}

#### 比较运算符

- `==`
- `!=`
- `<`
- `>`
- `<=`
- `>=`

{.cols-3 .marker-none}

### 示例

```
awk 'BEGIN {
        if ("foo" ~ "^fo+$")
                print "Fooey!";
}'
```

#### 不匹配

```
awk 'BEGIN {
        if ("boo" !~ "^fo+$")
                print "Boo!";
}'
```

#### if in array (如果存在于数组中)

```
awk 'BEGIN {
        assoc["foo"] = "bar";
        assoc["bar"] = "baz";
        if ("foo" in assoc)
                print "Fooey!";
}'
```

## Awk 函数

### 常用函数 {.col-span-2}

| 函数              | 描述                                                                     |
| --------------------- | ------------------------------------------------------------------------------- |
| `index(s,t)`          | 字符串 t 在字符串 s 中出现的位置，如果未找到则为 0                      |
| `length(s)`           | 字符串 s 的长度 (如果没有参数则为 $0)                                            |
| `rand`                | 0 到 1 之间的随机数                                                   |
| `substr(s,index,len)` | 返回 s 中从 index (从 1 开始计数) 开始的 len 个字符的子字符串            |
| `srand`               | 设置 rand 的种子并返回先前的种子                                      |
| `int(x)`              | 将 x 截断为整数值                                                     |
| `split(s,a,fs)`       | 将字符串 s 按 fs 分割到数组 a 中，返回 a 的长度                  |
| `match(s,r)`          | 正则表达式 r 在字符串 s 中出现的位置，如果未找到则为 0                    |
| `sub(r,t,s)`          | 在字符串 s 中 (如果未给出 s 则为 $0) 用 t 替换第一次出现的正则表达式 r |
| `gsub(r,t,s)`         | 在字符串 s 中用 t 替换所有出现的正则表达式 r                         |
| `system(cmd)`         | 执行 cmd 并返回退出状态                                              |
| `tolower(s)`          | 字符串 s 转为小写                                                           |
| `toupper(s)`          | 字符串 s 转为大写                                                           |
| `getline`             | 将 $0 设置为当前输入文件中的下一个输入记录。                            |

### 用户自定义函数

```
awk '
        # 返回最小值
        function find_min(num1, num2){
             if (num1 < num2)
             return num1
             return num2
        }
        # 返回最大值
        function find_max(num1, num2){
             if (num1 > num2)
             return num1
             return num2
        }
        # 主函数
        function main(num1, num2){
             result = find_min(num1, num2)
             print "Minimum =", result

             result = find_max(num1, num2)
             print "Maximum =", result
        }
        # 脚本从这里开始执行
        BEGIN {
             main(10, 60)
        }
'
```

## Awk 数组

### 带索引的数组

```
awk 'BEGIN {
        arr[0] = "foo";
        arr[1] = "bar";
        print(arr[0]); # => foo
        delete arr[0];
        print(arr[0]); # => ""
}'
```

### 带键的数组

```
awk 'BEGIN {
        assoc["foo"] = "bar";
        assoc["bar"] = "baz";
        print("baz" in assoc); # => 0
        print("foo" in assoc); # => 1
}'
```

### 使用 split 的数组

```
awk 'BEGIN {
        split("foo:bar:baz", arr, ":");
        for (key in arr)
                print arr[key];
}'
```

### 使用 asort 的数组

```
awk 'BEGIN {
        arr[0] = 3
        arr[1] = 2
        arr[2] = 4
        n = asort(arr)
        for (i = 1; i <= n ; i++)
                print(arr[i])
}'
```

### 多维数组

```
awk 'BEGIN {
        multidim[0,0] = "foo";
        multidim[0,1] = "bar";
        multidim[1,0] = "baz";
        multidim[1,1] = "boo";
}'
```

### 多维数组迭代

```
awk 'BEGIN {
        array[1,2]=3;
        array[2,3]=5;
        for (comb in array) {
                split(comb,sep,SUBSEP);
                print sep[1], sep[2],
                array[sep[1],sep[2]]
        }
}'
```

## Awk 条件

### if-else 语句

```
awk -v count=2 'BEGIN {
        if (count == 1)
                print "Yes";
        else
                print "Huh?";
}'
```

#### 三元运算符

```
awk -v count=2 'BEGIN {
        print (count==1) ? "Yes" : "Huh?";
}'
```

### 存在

```
awk 'BEGIN {
        assoc["foo"] = "bar";
        assoc["bar"] = "baz";
        if ("foo" in assoc)
                print "Fooey!";
}'
```

#### 不存在

```
awk 'BEGIN {
        assoc["foo"] = "bar";
        assoc["bar"] = "baz";
        if ("Huh" in assoc == 0 )
                print "Huh!";
}'
```

### switch

```
awk -F: '{
        switch (NR * 2 + 1) {
                case 3:
                case "11":
                        print NR - 1
                        break

                case /2[[:digit:]]+/:
                        print NR

                default:
                        print NR + 1

                case -1:
                        print NR * -1
        }
}' /etc/passwd
```

## Awk 循环

### for...i

```
awk 'BEGIN {
        for (i = 0; i < 10; i++)
                print "i=" i;
}'
```

#### 1 到 100 之间的 2 的幂

```
awk 'BEGIN {
        for (i = 1; i <= 100; i *= 2)
                print i
}'
```

### for...in

```
awk 'BEGIN {
        assoc["key1"] = "val1"
        assoc["key2"] = "val2"
        for (key in assoc)
                print assoc[key];
}'
```

#### 参数

```
awk 'BEGIN {
        for (argnum in ARGV)
                print ARGV[argnum];
}' a b c
```

### 示例 {.row-span-3}

#### 反转记录

```
awk -F: '{ x[NR] = $0 }
        END {
                for (i = NR; i > 0; i--)
                print x[i]
        }
' /etc/passwd
```

#### 反转字段

```
awk -F: '{
        for (i = NF; i > 0; i--)
                printf("%s ",$i);
        print ""
}' /etc/passwd
```

#### 按记录求和

```
awk -F: '{
        s=0;
        for (i = 1; i <= NF; i++)
                s += $i;
        print s
}' /etc/passwd
```

#### 对整个文件求和

```
awk -F: '
        {for (i = 1; i <= NF; i++)
                s += $i;
        };
        END{print s}
' /etc/passwd
```

### while {.row-span-2}

```
awk 'BEGIN {
        while (a < 10) {
                print "- " " concatenation: " a
                a++;
        }
}'
```

#### do...while

```
awk '{
        i = 1
        do {
                print $0
                i++
        } while (i <= 5)
}' /etc/passwd
```

### Break

```
awk 'BEGIN {
        break_num = 5
        for (i = 0; i < 10; i++) {
                print i
                if (i == break_num)
                        break
        }
}'
```

### Continue

```
awk 'BEGIN {
        for (x = 0; x <= 10; x++) {
                if (x == 5 || x == 6)
                        continue
                printf "%d ", x
        }
        print ""
}'
```

## Awk 格式化打印

### 用法

#### 右对齐

```
awk 'BEGIN{printf "|%10s|\n", "hello"}'

|     hello|
```

#### 左对齐

```
awk 'BEGIN{printf "|%-10s|\n", "hello"}'

|hello     |
```

### 常用说明符

| 字符     | 描述           |
| ------------- | --------------------- |
| `c`           | ASCII 字符       |
| `d`           | 十进制整数       |
| `e`, `E`, `f` | 浮点数格式 |
| `o`           | 无符号八进制值  |
| `s`           | 字符串                |
| `%`           | 字面量 %             |

### 空格

```
awk -F: '{
        printf "%-10s %s\n", $1, $(NF-1)
}' /etc/passwd | head -n 3
```

输出

```shell script
root       /root
bin        /bin
daemon     /sbin
```

### 标题

```
awk -F: 'BEGIN {
        printf "%-10s %s\n", "User", "Home"
        printf "%-10s %s\n", "----","----"}
        { printf "%-10s %s\n", $1, $(NF-1) }
' /etc/passwd | head -n 5
```

输出

```
User       Home
----       ----
root       /root
bin        /bin
daemon     /sbin
```

## 其他

### 正则表达式元字符

- `\`
- `^`
- `$`
- `.`
- `[`
- `]`
- `|`
- `(`
- `)`
- `*`
- `+`
- `?`

{.cols-3 .marker-none}

### 转义序列

| -    | -                   |
| ---- | ------------------- |
| `\b` | 退格           |
| `\f` | 换页           |
| `\n` | 换行 (换行符) |
| `\r` | 回车     |
| `\t` | 水平制表符      |
| `\v` | 垂直制表符      |

### 运行脚本

```shell script
$ cat demo.awk
#!/usr/bin/awk -f
BEGIN { x = 23 }
            { x += 2 }
END   { print x }
$ awk -f demo.awk /etc/passwd
69
```

## 另请参阅

- [GNU Awk 用户指南](https://www-zeuthen.desy.de/dv/documentation/unixguide/infohtml/gawk/gawk.html)
    _(www-zeuthen.desy.de)_
- [AWK 备忘单](https://gist.github.com/Rafe/3102414) _(gist.github.com)_

