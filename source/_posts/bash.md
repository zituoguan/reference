---
title: Bash
date: 2020-11-25 18:28:43
background: bg-[#3e4548]
tags:
    - shell
    - sh
    - echo
    - script
    - linux
categories:
    - 编程
    - 操作系统
intro: 这是 Linux Bash shell 脚本入门的快速参考备忘单。
plugins:
    - copyCode
---

## 入门

### hello.sh

```bash
#!/bin/bash

VAR="world"
echo "Hello $VAR!" # => Hello world!
```

执行脚本

```shell script
$ bash hello.sh
```

### 变量

```bash
NAME="John"

echo ${NAME}    # => John (变量)
echo $NAME      # => John (变量)
echo "$NAME"    # => John (变量)
echo '$NAME'    # => $NAME (精确字符串)
echo "${NAME}!" # => John! (变量)

NAME = "John"   # => 错误 (关于空格)
```

### 注释

```bash
# 这是 Bash 的行内注释。
```

```bash
: '
这是一个
非常简洁的注释
在 bash 中
'
```

多行注释使用 `:'` 开始，`'` 结束

### 参数 {.row-span-2}

| 表达式      | 描述                           |
| ----------- | ------------------------------------- |
| `$1` … `$9` | 参数 1 ... 9                     |
| `$0`        | 脚本本身的名称             |
| `$1`        | 第一个参数                        |
| `${10}`     | 位置参数 10               |
| `$#`        | 参数数量                   |
| `$$`        | shell 的进程 ID               |
| `$*`        | 所有参数                         |
| `$@`        | 所有参数，从第一个开始    |
| `$-`        | 当前选项                       |
| `$_`        | 上一个命令的最后一个参数 |

参见：[特殊参数](http://wiki.bash-hackers.org/syntax/shellvars#special_parameters_and_shell_variables)

### 函数

```bash
get_name() {
        echo "John"
}

echo "You are $(get_name)"
```

参见：[函数](#bash-函数)

### 条件语句 {#conditionals-example}

```bash
if [[ -z "$string" ]]; then
        echo "字符串为空"
elif [[ -n "$string" ]]; then
        echo "字符串不为空"
fi
```

参见：[条件语句](#bash-条件语句)

### 大括号展开

```bash
echo {A,B}.js
```

---

| 表达式 | 描述         |
| ---------- | ------------------- |
| `{A,B}`    | 等同于 `A B`       |
| `{A,B}.js` | 等同于 `A.js B.js` |
| `{1..5}`   | 等同于 `1 2 3 4 5` |

参见：[大括号展开](http://wiki.bash-hackers.org/syntax/expansion/brace)

### Shell 执行

```bash
# => I'm in /path/of/current
echo "I'm in $(PWD)"

# 等同于：
echo "I'm in `pwd`"
```

参见：[命令替换](http://wiki.bash-hackers.org/syntax/expansion/cmdsubst)

## Bash 参数展开

### 语法 {.row-span-2}

| 代码              | 描述         |
| ----------------- | ------------------- |
| `${FOO%suffix}`   | 移除后缀       |
| `${FOO#prefix}`   | 移除前缀       |
| `${FOO%%suffix}`  | 移除长后缀  |
| `${FOO##prefix}`  | 移除长前缀  |
| `${FOO/from/to}`  | 替换首次匹配 |
| `${FOO//from/to}` | 全部替换         |
| `${FOO/%from/to}` | 替换后缀      |
| `${FOO/#from/to}` | 替换前缀      |

#### 子字符串

| 表达式      | 描述                    |
| --------------- | ------------------------------ |
| `${FOO:0:3}`    | 子字符串 _(位置, 长度)_ |
| `${FOO:(-3):3}` | 从右侧开始的子字符串       |

#### 长度

| 表达式 | 描述      |
| ---------- | ---------------- |
| `${#FOO}`  | `$FOO` 的长度 |

#### 默认值

| 表达式        | 描述                              |
| ----------------- | ---------------------------------------- |
| `${FOO:-val}`     | `$FOO`，如果未设置则为 `val`                |
| `${FOO:=val}`     | 如果未设置，则将 `$FOO` 设置为 `val`             |
| `${FOO:+val}`     | 如果 `$FOO` 已设置，则为 `val`                   |
| `${FOO:?message}` | 如果 `$FOO` 未设置，则显示消息并退出 |

### 替换

```bash
echo ${food:-Cake}  #=> $food 或 "Cake"
```

```bash
STR="/path/to/foo.cpp"
echo ${STR%.cpp}    # /path/to/foo
echo ${STR%.cpp}.o  # /path/to/foo.o
echo ${STR%/*}      # /path/to

echo ${STR##*.}     # cpp (扩展名)
echo ${STR##*/}     # foo.cpp (基本路径)

echo ${STR#*/}      # path/to/foo.cpp
echo ${STR##*/}     # foo.cpp

echo ${STR/foo/bar} # /path/to/bar.cpp
```

### 切片

```bash
name="John"
echo ${name}           # => John
echo ${name:0:2}       # => Jo
echo ${name::2}        # => Jo
echo ${name::-1}       # => Joh
echo ${name:(-1)}      # => n
echo ${name:(-2)}      # => hn
echo ${name:(-2):2}    # => hn

length=2
echo ${name:0:length}  # => Jo
```

参见：[参数展开](http://wiki.bash-hackers.org/syntax/pe)

### 基本路径和目录路径

```bash
SRC="/path/to/foo.cpp"
```

```bash
BASEPATH=${SRC##*/}
echo $BASEPATH  # => "foo.cpp"


DIRPATH=${SRC%$BASEPATH}
echo $DIRPATH   # => "/path/to/"
```

### 转换

```bash
STR="HELLO WORLD!"
echo ${STR,}   # => hELLO WORLD!
echo ${STR,,}  # => hello world!

STR="hello world!"
echo ${STR^}   # => Hello world!
echo ${STR^^}  # => HELLO WORLD!

ARR=(hello World)
echo "${ARR[@],}" # => hello world
echo "${ARR[@]^}" # => Hello World
```

## Bash 数组

### 定义数组

```bash
Fruits=('Apple' 'Banana' 'Orange')

Fruits[0]="Apple"
Fruits[1]="Banana"
Fruits[2]="Orange"

ARRAY1=(foo{1..2}) # => foo1 foo2
ARRAY2=({A..D})    # => A B C D

# 合并 => foo1 foo2 A B C D
ARRAY3=(${ARRAY1[@]} ${ARRAY2[@]})

# declare 结构
declare -a Numbers=(1 2 3)
Numbers+=(4 5) # 追加 => 1 2 3 4 5
```

### 索引

| -                  | -             |
| ------------------ | ------------- |
| `${Fruits[0]}`     | 第一个元素 |
| `${Fruits[-1]}`    | 最后一个元素  |
| `${Fruits[*]}`     | 所有元素  |
| `${Fruits[@]}`     | 所有元素  |
| `${#Fruits[@]}`    | 元素总数 |
| `${#Fruits}`       | 第一个元素的长度 |
| `${#Fruits[3]}`    | 第 n 个元素的长度 |
| `${Fruits[@]:3:2}` | 范围         |
| `${!Fruits[@]}`    | 所有键   |

### 迭代

```bash
Fruits=('Apple' 'Banana' 'Orange')

for e in "${Fruits[@]}"; do
        echo $e
done
```

#### 带索引

```bash
for i in "${!Fruits[@]}"; do
    printf "%s\t%s\n" "$i" "${Fruits[$i]}"
done

```

### 操作 {.col-span-2}

```bash
Fruits=("${Fruits[@]}" "Watermelon")     # 推入 (Push)
Fruits+=('Watermelon')                   # 也可推入 (Push)
Fruits=( ${Fruits[@]/Ap*/} )             # 通过正则表达式匹配移除
unset Fruits[2]                          # 移除一个项目
Fruits=("${Fruits[@]}")                  # 复制
Fruits=("${Fruits[@]}" "${Veggies[@]}")  # 连接
lines=(`cat "logfile"`)                  # 从文件读取
```

### 数组作为参数

```bash
function extract()
{
        local -n myarray=$1
        local idx=$2
        echo "${myarray[$idx]}"
}
Fruits=('Apple' 'Banana' 'Orange')
extract Fruits 2     # => Orange
```

## Bash 字典

### 定义

```bash
declare -A sounds
```

```bash
sounds[dog]="bark"
sounds[cow]="moo"
sounds[bird]="tweet"
sounds[wolf]="howl"
```

### 使用字典

```bash
echo ${sounds[dog]} # 狗的声音
echo ${sounds[@]}   # 所有值
echo ${!sounds[@]}  # 所有键
echo ${#sounds[@]}  # 元素数量
unset sounds[dog]   # 删除狗
```

### 迭代

```bash
for val in "${sounds[@]}"; do
        echo $val
done
```

---

```bash
for key in "${!sounds[@]}"; do
        echo $key
done
```

## Bash 条件语句

### 整数条件

| 条件           | 描述                                 |
| ------------------- | ------------------------------------------- |
| `[[ NUM -eq NUM ]]` | <yel>相</yel>等                            |
| `[[ NUM -ne NUM ]]` | <yel>不</yel>相<yel>等</yel>             |
| `[[ NUM -lt NUM ]]` | <yel>小</yel>于             |
| `[[ NUM -le NUM ]]` | <yel>小</yel>于或<yel>等</yel>于    |
| `[[ NUM -gt NUM ]]` | <yel>大</yel>于          |
| `[[ NUM -ge NUM ]]` | <yel>大</yel>于或<yel>等</yel>于 |
| `(( NUM < NUM ))`   | 小于                                   |
| `(( NUM <= NUM ))`  | 小于或等于                          |
| `(( NUM > NUM ))`   | 大于                                |
| `(( NUM >= NUM ))`  | 大于或等于                          |

### 字符串条件

| 条件          | 描述                 |
| ------------------ | --------------------------- |
| `[[ -z STR ]]`     | 空字符串                |
| `[[ -n STR ]]`     | <yel>非</yel>空字符串 |
| `[[ STR == STR ]]` | 相等                       |
| `[[ STR = STR ]]`  | 相等 (同上)          |
| `[[ STR < STR ]]`  | 小于 _(ASCII)_         |
| `[[ STR > STR ]]`  | 大于 _(ASCII)_      |
| `[[ STR != STR ]]` | 不相等                   |
| `[[ STR =~ STR ]]` | 正则表达式                      |

### 示例 {.row-span-3}

#### 字符串

```bash
if [[ -z "$string" ]]; then
        echo "字符串为空"
elif [[ -n "$string" ]]; then
        echo "字符串不为空"
else
        echo "这永远不会发生"
fi
```

#### 组合

```bash
if [[ X && Y ]]; then
        ...
fi
```

#### 相等

```bash
if [[ "$A" == "$B" ]]; then
        ...
fi
```

#### 正则表达式

```bash
if [[ '1. abc' =~ ([a-z]+) ]]; then
        echo ${BASH_REMATCH[1]}
fi
```

#### 更小

```bash
if (( $a < $b )); then
     echo "$a 小于 $b"
fi
```

#### 存在

```bash
if [[ -e "file.txt" ]]; then
        echo "文件存在"
fi
```

### 文件条件 {.row-span-2}

| 条件         | 描述                            |
| ----------------- | -------------------------------------- |
| `[[ -e FILE ]]`   | <yel>存</yel>在                      |
| `[[ -d FILE ]]`   | <yel>目</yel>录                   |
| `[[ -f FILE ]]`   | <yel>文</yel>件                        |
| `[[ -h FILE ]]`   | 符号链接                                |
| `[[ -s FILE ]]`   | 大小 > 0 字节                      |
| `[[ -r FILE ]]`   | <yel>可</yel>读                    |
| `[[ -w FILE ]]`   | <yel>可</yel>写                    |
| `[[ -x FILE ]]`   | 可执行                             |
| `[[ f1 -nt f2 ]]` | f1 <yel>比</yel> f2 <yel>新</yel> |
| `[[ f1 -ot f2 ]]` | f2 <yel>比</yel> f1 <yel>旧</yel> |
| `[[ f1 -ef f2 ]]` | 相同文件                             |

### 更多条件

| 条件            | 描述          |
| -------------------- | -------------------- | ----- | --- |
| `[[ -o noclobber ]]` | 如果选项已启用 |
| `[[ ! EXPR ]]`       | 非                  |
| `[[ X && Y ]]`       | 与                  |
| `[[ X                |                      | Y ]]` | 或  |

### 逻辑与、或

```bash
if [ "$1" = 'y' -a $2 -gt 0 ]; then
        echo "yes"
fi

if [ "$1" = 'n' -o $2 -lt 0 ]; then
        echo "no"
fi
```

## Bash 循环

### 基本 for 循环

```bash
for i in /etc/rc.*; do
        echo $i
done
```

### C 风格 for 循环

```bash
for ((i = 0 ; i < 100 ; i++)); do
        echo $i
done
```

### 范围 {.row-span-2}

```bash
for i in {1..5}; do
        echo "Welcome $i"
done
```

#### 带步长

```bash
for i in {5..50..5}; do
        echo "Welcome $i"
done
```

### Continue

```bash {data=3,5}
for number in $(seq 1 3); do
        if [[ $number == 2 ]]; then
                continue;
        fi
        echo "$number"
done
```

### Break

```bash
for number in $(seq 1 3); do
        if [[ $number == 2 ]]; then
                # 跳过循环的其余部分。
                break;
        fi
        # 这只会打印 1
        echo "$number"
done
```

### Until

```bash
count=0
until [ $count -gt 10 ]; do
        echo "$count"
        ((count++))
done
```

### While 与递增

```bash
i=1
while [[ $i -lt 4 ]]; do
        echo "Number: $i"
        ((i++))
done
```

### While 与递减

```bash
i=3
while [[ $i -gt 0 ]]; do
        echo "Number: $i"
        ((i--))
done
```

#### 与 test 结合

```bash
i=3
while ((i--)); do
        echo "Number: $i"
done
```

### 无限循环

```bash
while true; do
        # 这里是一些代码。
done
```

### 无限循环 (简写)

```bash
while :; do
        # 这里是一些代码。
done
```

### 读取行

```bash
cat file.txt | while read line; do
        echo $line
done
```

## Bash 函数

### 定义函数

```bash
myfunc() {
        echo "hello $1"
}
```

```bash
# 与上面相同 (备用语法)
function myfunc() {
        echo "hello $1"
}
```

```bash
myfunc "John"
```

### 返回值

```bash
myfunc() {
        local myresult='some value'
        echo $myresult
}
```

```bash
result="$(myfunc)"
```

### 抛出错误

```bash
myfunc() {
        return 1
}
```

```bash
if myfunc; then
        echo "success"
else
        echo "failure"
fi
```

## Bash 选项 {.cols-2}

### 选项

```bash
# 避免覆盖文件
# (echo "hi" > foo)
set -o noclobber

# 用于在出错时退出
# 避免级联错误
set -o errexit

# 揭示隐藏的失败
set -o pipefail

# 暴露未设置的变量
set -o nounset
```

### Glob 选项

```bash
# 不匹配的 glob 被移除
# ('*.foo' => '')
shopt -s nullglob

# 不匹配的 glob 抛出错误
shopt -s failglob

# 不区分大小写的 glob
shopt -s nocaseglob

# 通配符匹配点文件
# ("*.sh" => ".foo.sh")
shopt -s dotglob

# 允许 ** 进行递归匹配
# ('lib/**/*.rb' => 'lib/a/b/c.rb')
shopt -s globstar
```

## Bash 历史 {.cols-2}

### 命令

| 命令               | 描述                               |
| --------------------- | ----------------------------------------- |
| `history`             | 显示历史                              |
| `sudo !!`             | 使用 sudo 运行上一个命令        |
| `shopt -s histverify` | 不要立即执行展开的结果 |

### 展开

| 表达式   | 描述                                          |
| ------------ | ---------------------------------------------------- |
| `!$`         | 展开最近命令的最后一个参数         |
| `!*`         | 展开最近命令的所有参数         |
| `!-n`        | 展开第 `n` 个最近的命令                     |
| `!n`         | 展开历史中的第 `n` 个命令                     |
| `!<command>` | 展开命令 `<command>` 的最近一次调用 |

### 操作

| 代码                 | 描述                                                           |
| -------------------- | --------------------------------------------------------------------- |
| `!!`                 | 再次执行上一个命令                                            |
| `!!:s/<FROM>/<TO>/`  | 在最近的命令中将 `<FROM>` 的首次出现替换为 `<TO>` |
| `!!:gs/<FROM>/<TO>/` | 在最近的命令中将 `<FROM>` 的所有出现替换为 `<TO>`  |
| `!$:t`               | 仅从最近命令的最后一个参数展开基本名称       |
| `!$:h`               | 仅从最近命令的最后一个参数展开目录       |

`!!` 和 `!$` 可以替换为任何有效的展开。

### 切片

| 代码     | 描述                                                                              |
| -------- | ---------------------------------------------------------------------------------------- |
| `!!:n`   | 仅从最近的命令展开第 `n` 个标记 (命令是 `0`；第一个参数是 `1`) |
| `!^`     | 从最近的命令展开第一个参数                                           |
| `!$`     | 从最近的命令展开最后一个标记                                               |
| `!!:n-m` | 从最近的命令展开标记范围                                          |
| `!!:n-$` | 从最近的命令展开第 `n` 个标记到最后一个标记                                      |

`!!` 可以替换为任何有效的展开，例如 `!cat`、`!-2`、`!42` 等。

## 其他

### 数值计算

```bash
$((a + 200))      # 将 $a 增加 200
```

```bash
$(($RANDOM%200))  # 随机数 0..199
```

### 子 Shell

```bash
(cd somedir; echo "我现在在 $PWD")
pwd # 仍然在第一个目录
```

### 检查命令

```bash
command -V cd
#=> "cd 是一个函数/别名/等等"
```

### 重定向 {.row-span-2 .col-span-2}

```bash
python hello.py > output.txt   # stdout 到 (文件)
python hello.py >> output.txt  # stdout 到 (文件), 追加
python hello.py 2> error.log   # stderr 到 (文件)
python hello.py 2>&1           # stderr 到 stdout
python hello.py 2>/dev/null    # stderr 到 (空设备)
python hello.py &>/dev/null    # stdout 和 stderr 到 (空设备)
```

```bash
python hello.py < foo.txt      # 将 foo.txt 提供给 python 的 stdin
```

### 相对路径 Source

```bash
source "${0%/*}/../share/foo.sh"
```

### 脚本目录

```bash
DIR="${0%/*}"
```

### Case/Switch 语句

```bash
case "$1" in
        start | up)
        vagrant up
        ;;

        *)
        echo "用法: $0 {start|stop|ssh}"
        ;;
esac
```

### 捕获错误 {.col-span-2}

```bash
trap 'echo 大约在 $LINENO 行发生错误' ERR
```

或

```bash
traperr() {
        echo "错误: ${BASH_SOURCE[1]} 大约在 ${BASH_LINENO[0]} 行"
}

set -o errtrace
trap traperr ERR
```

### printf

```bash
printf "Hello %s, I'm %s" Sven Olga
#=> "Hello Sven, I'm Olga

printf "1 + 1 = %d" 2
#=> "1 + 1 = 2"

printf "Print a float: %f" 2
#=> "Print a float: 2.000000"
```

### 获取选项 {.col-span-2}

```bash
while [[ "$1" =~ ^- && ! "$1" == "--" ]]; do case $1 in
        -V | --version )
        echo $version
        exit
        ;;
        -s | --string )
        shift; string=$1
        ;;
        -f | --flag )
        flag=1
        ;;
esac; shift; done
if [[ "$1" == '--' ]]; then shift; fi
```

### 检查命令结果 {.col-span-2}

```bash
if ping -c 1 google.com; then
        echo "看起来你有可用的网络连接"
fi
```

### 特殊变量 {.row-span-2}

| 表达式 | 描述                  |
| ---------- | ---------------------------- |
| `$?`       | 上一个任务的退出状态     |
| `$!`       | 上一个后台任务的 PID  |
| `$$`       | Shell 的 PID                 |
| `$0`       | Shell 脚本的文件名 |

参见 [特殊参数](http://wiki.bash-hackers.org/syntax/shellvars#special_parameters_and_shell_variables)。

### Grep 检查 {.col-span-2}

```bash
if grep -q 'foo' ~/.bash_history; then
        echo "你过去似乎输入过 'foo'"
fi
```

### 反斜杠转义 {.row-span-2}

- &nbsp;
- \!
- \"
- \#
- \&
- \'
- \(
- \)
- \,
- \;
- \<
- \>
- \[
- \|
- \\
- \]
- \^
- \{
- \}
- \`
- \$
- \*
- \?

{.cols-4 .marker-none}

使用 `\` 转义这些特殊字符

### Heredoc (在此文档)

```sh
cat <<END
hello world
END
```

### 返回上一个目录

```bash
pwd # /home/user/foo
cd bar/
pwd # /home/user/foo/bar
cd -
pwd # /home/user/foo
```

### 读取输入

```bash
echo -n "继续吗? [y/n]: "
read ans
echo $ans
```

```bash
read -n 1 ans    # 仅一个字符
```

### 条件执行

```bash
git commit && git push
git commit || echo "提交失败"
```

### 严格模式

```bash
set -euo pipefail
IFS=$'\n\t'
```

参见：[非官方 bash 严格模式](http://redsymbol.net/articles/unofficial-bash-strict-mode/)

### 可选参数

```bash
args=("$@")
args+=(foo)
args+=(bar)
echo "${args[@]}"
```

将参数放入数组然后追加

## 另请参阅 {.cols-1}

- [Devhints](https://devhints.io/bash) _(devhints.io)_
- [Bash-hackers wiki](http://wiki.bash-hackers.org/) _(bash-hackers.org)_
- [Shell vars](http://wiki.bash-hackers.org/syntax/shellvars) _(bash-hackers.org)_
- [Y 分钟学习 bash](https://learnxinyminutes.com/docs/bash/) _(learnxinyminutes.com)_
- [Bash 指南](http://mywiki.wooledge.org/BashGuide) _(mywiki.wooledge.org)_
- [ShellCheck](https://www.shellcheck.net/) _(shellcheck.net)_
- [shell - Standard Shell](https://devmanual.gentoo.org/tools-reference/bash/index.html) _(devmanual.gentoo.org)_

