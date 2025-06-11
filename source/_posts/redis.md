---
title: Redis
background: bg-[#c13b2c]
tags:
  - 缓存
categories:
  - 数据库
date: 2020-12-26 19:33:15
intro: |
  这是一个 [redis](https://redis.io/) 快速参考备忘单，列出了 redis 命令的示例
plugins:
  - copyCode
---

## 入门

### 入门

启动 Redis

```shell script
$ redis-server
```

连接到 Redis (Redis CLI 客户端)

```shell script
$ redis-cli
```

连接到 Redis (telnet)

```shell script
$ telnet 127.0.0.1 6379
```

### Hello World

#### Ping

```shell script
redis> PING
PONG
```

#### Hello World

```shell script
redis> SET mykey "Hello world"
OK
redis> GET mykey
"Hello world"
```

### 基本数据类型

- [字符串](#redis-string-command)
- [列表](#redis-list-command)
- [哈希](#redis-hash-command)
- [集合](#redis-set-command)
- [有序集合](#redis-sorted-set-command)

Redis 支持 5 种基本数据类型

## Redis 字符串命令{.cols-3}

### APPEND

```{.wrap}
APPEND key value
```

#### 示例

```shell script
redis> EXISTS mykey
(integer) 0
redis> APPEND mykey "Hello"
(integer) 5
redis> APPEND mykey " World"
(integer) 11
redis> GET mykey
"Hello World"
```

将一个值追加到键

### BITCOUNT

```{.wrap}
BITCOUNT key [start end]
```

#### 示例

```shell script
redis> SET mykey "foobar"
"OK"
redis> BITCOUNT mykey
(integer) 26
redis> BITCOUNT mykey 0 0
(integer) 4
redis> BITCOUNT mykey 1 1
(integer) 6
```

计算字符串中已设置的位数

### BITFIELD

```{.wrap}
BITFIELD key [GET type offset] [SET type offset value] [INCRBY type offset increment] [OVERFLOW WRAP|SAT|FAIL]
```

#### 示例

```shell script
redis> BITFIELD mykey INCRBY i5 100 1 GET u4 0
1) (integer) 1
2) (integer) 0
```

对字符串执行任意位域整数操作

### BITOP

```{.wrap}
BITOP operation destkey key [key ...]
```

#### 示例

```shell script
redis> SET key1 "foobar"
"OK"
redis> SET key2 "abcdef"
"OK"
redis> BITOP AND dest key1 key2
(integer) 6
redis> GET dest
"`bc`ab"
```

在字符串之间执行位运算

### BITPOS

```{.wrap}
BITPOS key bit [start] [end]
```

#### 示例

```shell script
redis> SET mykey "\xff\xf0\x00"
"OK"
redis> BITPOS mykey 0
(integer) 12
redis> SET mykey "\x00\xff\xf0"
"OK"
redis> BITPOS mykey 1 0
(integer) 8
redis> BITPOS mykey 1 2
(integer) 16
redis> set mykey "\x00\x00\x00"
"OK"
redis> BITPOS mykey 1
(integer) -1
```

查找字符串中第一个已设置或清除的位

### DECR

```{.wrap}
DECR key
```

#### 示例

```shell script
redis> SET mykey "10"
"OK"
redis> DECR mykey
(integer) 9
redis> SET mykey "234293482390480948029348230948"
"OK"
redis> DECR mykey
ERR ERR value is not an integer or out of range
```

将键的整数值减一

### DECRBY

```{.wrap}
DECRBY key decrement
```

#### 示例

```shell script
redis> SET mykey "10"
"OK"
redis> DECRBY mykey 3
(integer) 7
```

将键的整数值减去给定数量

### GET

```{.wrap}
GET key
```

#### 示例

```shell script
redis> GET nonexisting
(nil)
redis> SET mykey "Hello"
"OK"
redis> GET mykey
"Hello"
```

获取键的值

### GETBIT

```{.wrap}
GETBIT key offset
```

#### 示例

```shell script
redis> SETBIT mykey 7 1
(integer) 0
redis> GETBIT mykey 0
(integer) 0
redis> GETBIT mykey 7
(integer) 1
redis> GETBIT mykey 100
(integer) 0
```

返回存储在键中的字符串值在偏移量处的位值

### GETRANGE

```{.wrap}
GETRANGE key start end
```

#### 示例

```shell script
redis> SET mykey "This is a string"
"OK"
redis> GETRANGE mykey 0 3
"This"
redis> GETRANGE mykey -3 -1
"ing"
redis> GETRANGE mykey 0 -1
"This is a string"
redis> GETRANGE mykey 10 100
"string"
```

获取存储在键中的字符串的子串

### GETSET

```{.wrap}
GETSET key value
```

#### 示例

```shell script
redis> INCR mycounter
(integer) 1
redis> GETSET mycounter "0"
"1"
redis> GET mycounter
"0"
```

设置键的字符串值并返回其旧值

### INCR

```{.wrap}
INCR key
```

#### 示例

```shell script
redis> SET mykey "10"
"OK"
redis> INCR mykey
(integer) 11
redis> GET mykey
"11"
```

将键的整数值加一

### MSETNX

```{.wrap}
MSETNX key value [key value ...]
```

#### 示例

```shell script
redis> MSETNX key1 "Hello" key2 "there"
(integer) 1
redis> MSETNX key2 "new" key3 "world"
(integer) 0
redis> MGET key1 key2 key3
1) "Hello"
2) "there"
3) (nil)
```

将多个键设置为多个值，仅当所有键都不存在时

### INCRBYFLOAT

```{.wrap}
INCRBYFLOAT key increment
```

#### 示例

```shell script
redis> SET mykey 10.50
"OK"
redis> INCRBYFLOAT mykey 0.1
"10.6"
redis> INCRBYFLOAT mykey -5
"5.6"
redis> SET mykey 5.0e3
"OK"
redis> INCRBYFLOAT mykey 2.0e2
"5200"
```

将键的浮点值增加给定数量

### MGET

```{.wrap}
MGET key [key ...]
```

#### 示例

```shell script
redis> SET key1 "Hello"
"OK"
redis> SET key2 "World"
"OK"
redis> MGET key1 key2 nonexisting
1) "Hello"
2) "World"
3) (nil)
```

获取所有给定键的值

### MSET

```{.wrap}
MSET key value [key value ...]
```

#### 示例

```shell script
redis> MSET key1 "Hello" key2 "World"
"OK"
redis> GET key1
"Hello"
redis> GET key2
"World"
```

将多个键设置为多个值

### INCRBY

```{.wrap}
INCRBY key increment
```

#### 示例

```shell script
redis> SET mykey "10"
"OK"
redis> INCRBY mykey 5
(integer) 15
```

将键的整数值增加给定数量

### PSETEX

```{.wrap}
PSETEX key milliseconds value
```

#### 示例

```shell script
redis> PSETEX mykey 1000 "Hello"
"OK"
redis> PTTL mykey
(integer) 1000
redis> GET mykey
"Hello"
```

设置键的值和以毫秒为单位的过期时间

### SET

```{.wrap}
SET key value [EX seconds|PX milliseconds|KEEPTTL] [NX|XX] [GET]
```

#### 示例

```shell script
redis> SET mykey "Hello"
"OK"
redis> GET mykey
"Hello"
redis> SET anotherkey "will expire in a minute" EX 60
"OK"
```

设置键的字符串值

### SETBIT

```{.wrap}
SETBIT key offset value
```

#### 示例

```shell script
redis> SETBIT mykey 7 1
(integer) 0
redis> SETBIT mykey 7 0
(integer) 1
redis> GET mykey
"\u0000"
```

设置或清除存储在键中的字符串值在偏移量处的位

### SETEX

```{.wrap}
SETEX key seconds value
```

#### 示例

```shell script
redis> SETEX mykey 10 "Hello"
"OK"
redis> TTL mykey
(integer) 10
redis> GET mykey
"Hello"
```

设置键的值和过期时间

### SETNX

```{.wrap}
SETNX key value
```

#### 示例

```shell script
redis> SETNX mykey "Hello"
(integer) 1
redis> SETNX mykey "World"
(integer) 0
redis> GET mykey
"Hello"
```

设置键的值，仅当键不存在时

### SETRANGE

```{.wrap}
SETRANGE key offset value
```

#### 示例

```shell script
redis> SET key1 "Hello World"
"OK"
redis> SETRANGE key1 6 "Redis"
(integer) 11
redis> GET key1
"Hello Redis"
```

从指定偏移量开始覆盖键中字符串的一部分

### STRLEN

```{.wrap}
STRLEN key
```

#### 示例

```shell script
redis> SET mykey "Hello world"
"OK"
redis> STRLEN mykey
(integer) 11
redis> STRLEN nonexisting
(integer) 0
```

获取存储在键中的值的长度

### STRALGO

```{.wrap}
STRALGO LCS algo-specific-argument [algo-specific-argument ...]
```

#### 示例

```shell script
redis> STRALGO LCS KEYS key1 key2 IDX
1) "matches"
2) 1) 1) 1) (integer) 4
         2) (integer) 7
      2) 1) (integer) 5
         2) (integer) 8
   2) 1) 1) (integer) 2
         2) (integer) 3
      2) 1) (integer) 0
         2) (integer) 1
3) "len"
4) (integer) 6
```

对字符串运行算法（当前为 LCS）

## Redis 集合命令

### SADD

```{.wrap}
SADD key member [member ...]
```

#### 示例

```shell script
redis> SADD myset "Hello"
(integer) 1
redis> SADD myset "World"
(integer) 1
redis> SADD myset "World"
(integer) 0
redis> SMEMBERS myset
1) "Hello"
2) "World"
```

向集合添加一个或多个成员

### SCARD

```{.wrap}
SCARD key
```

#### 示例

```shell script
redis> SADD myset "Hello"
(integer) 1
redis> SADD myset "World"
(integer) 1
redis> SCARD myset
(integer) 2
```

获取集合中的成员数量

### SDIFF

```{.wrap}
SDIFF key [key ...]
```

#### 示例

```shell script
redis> SADD key1 "a"
(integer) 1
redis> SADD key1 "b"
(integer) 1
redis> SADD key1 "c"
(integer) 1
redis> SADD key2 "c"
(integer) 1
redis> SADD key2 "d"
(integer) 1
redis> SADD key2 "e"
(integer) 1
redis> SDIFF key1 key2
1) "a"
2) "b"
```

计算多个集合的差集

### SDIFFSTORE

```{.wrap}
SDIFFSTORE destination key [key ...]
```

#### 示例

```shell script
redis> SADD key1 "a"
(integer) 1
redis> SADD key1 "b"
(integer) 1
redis> SADD key1 "c"
(integer) 1
redis> SADD key2 "c"
(integer) 1
redis> SADD key2 "d"
(integer) 1
redis> SADD key2 "e"
(integer) 1
redis> SDIFFSTORE key key1 key2
(integer) 2
redis> SMEMBERS key
1) "a"
2) "b"
```

计算多个集合的差集并将结果集存储在一个键中

### SINTER

```{.wrap}
SINTER key [key ...]
```

#### 示例

```shell script
redis> SADD key1 "a"
(integer) 1
redis> SADD key1 "b"
(integer) 1
redis> SADD key1 "c"
(integer) 1
redis> SADD key2 "c"
(integer) 1
redis> SADD key2 "d"
(integer) 1
redis> SADD key2 "e"
(integer) 1
redis> SINTER key1 key2
1) "c"
```

计算多个集合的交集

### SINTERSTORE

```{.wrap}
SINTERSTORE destination key [key ...]
```

#### 示例

```shell script
redis> SADD key1 "a"
(integer) 1
redis> SADD key1 "b"
(integer) 1
redis> SADD key1 "c"
(integer) 1
redis> SADD key2 "c"
(integer) 1
redis> SADD key2 "d"
(integer) 1
redis> SADD key2 "e"
(integer) 1
redis> SINTERSTORE key key1 key2
(integer) 1
redis> SMEMBERS key
1) "c"
```

计算多个集合的交集并将结果集存储在一个键中

### SISMEMBER

```{.wrap}
SISMEMBER key member
```

#### 示例

```shell script
redis> SADD myset "one"
(integer) 1
redis> SISMEMBER myset "one"
(integer) 1
redis> SISMEMBER myset "two"
(integer) 0
```

判断给定值是否是集合的成员

### SMISMEMBER

```{.wrap}
SMISMEMBER key member [member ...]
```

#### 示例

```shell script
redis> SADD myset "one"
(integer) 1
redis> SADD myset "one"
(integer) 0
redis> SMISMEMBER myset "one" "notamember"
1) (integer) 1
2) (integer) 0
```

返回给定元素对于一个集合的成员关系

### SMEMBERS

```{.wrap}
SMEMBERS key
```

#### 示例

```shell script
redis> SADD myset "Hello"
(integer) 1
redis> SADD myset "World"
(integer) 1
redis> SMEMBERS myset
1) "Hello"
2) "World"
```

获取集合中的所有成员

### SMOVE

```{.wrap}
SMOVE source destination member
```

#### 示例

```shell script
redis> SADD myset "one"
(integer) 1
redis> SADD myset "two"
(integer) 1
redis> SADD myotherset "three"
(integer) 1
redis> SMOVE myset myotherset "two"
(integer) 1
redis> SMEMBERS myset
1) "one"
redis> SMEMBERS myotherset
1) "two"
2) "three"
```

将一个成员从一个集合移动到另一个集合

### SPOP

```{.wrap}
SPOP key [count]
```

#### 示例

```shell script
redis> SADD myset "one"
(integer) 1
redis> SADD myset "two"
(integer) 1
redis> SADD myset "three"
(integer) 1
redis> SPOP myset
"two"
redis> SMEMBERS myset
1) "one"
2) "three"
redis> SADD myset "four"
(integer) 1
redis> SADD myset "five"
(integer) 1
redis> SPOP myset 3
1) "four"
2) "five"
3) "three"
redis> SMEMBERS myset
1) "one"
```

从集合中移除并返回一个或多个随机成员

### SRANDMEMBER

```{.wrap}
SRANDMEMBER key [count]
```

#### 示例

```shell script
redis> SADD myset one two three
(integer) 3
redis> SRANDMEMBER myset
"three"
redis> SRANDMEMBER myset 2
1) "two"
2) "three"
redis> SRANDMEMBER myset -5
1) "one"
2) "two"
3) "three"
4) "three"
5) "one"
```

从集合中获取一个或多个随机成员

### SREM

```{.wrap}
SREM key member [member ...]
```

#### 示例

```shell script
redis> SADD myset "one"
(integer) 1
redis> SADD myset "two"
(integer) 1
redis> SADD myset "three"
(integer) 1
redis> SREM myset "one"
(integer) 1
redis> SREM myset "four"
(integer) 0
redis> SMEMBERS myset
1) "two"
2) "three"
```

从集合中移除一个或多个成员

### SUNION

```{.wrap}
SUNION key [key ...]
```

#### 示例

```shell script
redis> SADD key1 "a"
(integer) 1
redis> SADD key1 "b"
(integer) 1
redis> SADD key1 "c"
(integer) 1
redis> SADD key2 "c"
(integer) 1
redis> SADD key2 "d"
(integer) 1
redis> SADD key2 "e"
(integer) 1
redis> SUNION key1 key2
1) "a"
2) "c"
3) "e"
4) "b"
5) "d"
```

计算多个集合的并集

### SUNIONSTORE

```{.wrap}
SUNIONSTORE destination key [key ...]
```

#### 示例

```shell script
redis> SADD key1 "a"
(integer) 1
redis> SADD key1 "b"
(integer) 1
redis> SADD key1 "c"
(integer) 1
redis> SADD key2 "c"
(integer) 1
redis> SADD key2 "d"
(integer) 1
redis> SADD key2 "e"
(integer) 1
redis> SUNIONSTORE key key1 key2
(integer) 5
redis> SMEMBERS key
1) "a"
2) "c"
3) "e"
4) "b"
5) "d"
```

计算多个集合的并集并将结果集存储在一个键中

## Redis 列表命令

### Misc

| -                                                   | -                                                                                                  |
| --------------------------------------------------- | -------------------------------------------------------------------------------------------------- |
| [BRPOPLPUSH ](https://redis.io/commands/brpoplpush) | 从列表中弹出一个元素，将其推送到另一个列表并返回它；或阻塞直到有可用元素                               |
| [BLMOVE ](https://redis.io/commands/blmove)         | 从列表中弹出一个元素，将其推送到另一个列表并返回它；或阻塞直到有可用元素                               |

### BLPOP

```{.wrap}
BLPOP key [key ...] timeout
```

#### 示例

```shell script
redis> DEL list1 list2
(integer) 0
redis> RPUSH list1 a b c
(integer) 3
redis> BLPOP list1 list2 0
1) "list1"
2) "a"
```

移除并获取列表中的第一个元素，或阻塞直到有可用元素 |

### BRPOP

```{.wrap}
BRPOP key [key ...] timeout
```

#### 示例

```shell script
redis> DEL list1 list2
(integer) 0
redis> RPUSH list1 a b c
(integer) 3
redis> BRPOP list1 list2 0
1) "list1"
2) "c"
```

移除并获取列表中的最后一个元素，或阻塞直到有可用元素 |

### LINDEX

```{.wrap}
LINDEX key index
```

#### 示例

```shell script
redis> LPUSH mylist "World"
(integer) 1
redis> LPUSH mylist "Hello"
(integer) 2
redis> LINDEX mylist 0
"Hello"
redis> LINDEX mylist -1
"World"
redis> LINDEX mylist 3
(nil)
```

通过索引从列表中获取一个元素

### LINSERT

```{.wrap}
LINSERT key BEFORE|AFTER pivot element
```

#### 示例

```shell script
redis> RPUSH mylist "Hello"
(integer) 1
redis> RPUSH mylist "World"
(integer) 2
redis> LINSERT mylist BEFORE "World" "There"
(integer) 3
redis> LRANGE mylist 0 -1
1) "Hello"
2) "There"
3) "World"
```

在列表中的另一个元素之前或之后插入一个元素

### LLEN

```{.wrap}
LLEN key
```

#### 示例

```shell script
redis> LPUSH mylist "World"
(integer) 1
redis> LPUSH mylist "Hello"
(integer) 2
redis> LLEN mylist
(integer) 2
```

获取列表的长度

### LPOP

```{.wrap}
LPOP key [count]
```

#### 示例

```shell script
redis> RPUSH mylist "one"
(integer) 1
redis> RPUSH mylist "two"
(integer) 2
redis> RPUSH mylist "three"
(integer) 3
redis> LPOP mylist
"one"
redis> LRANGE mylist 0 -1
1) "two"
2) "three"
```

移除并获取列表中的第一个元素

### LPOS

```{.wrap}
LPOS key element [RANK rank] [COUNT num-matches] [MAXLEN len]
```

#### 示例

```shell script
redis> RPUSH mylist a b c d 1 2 3 4 3 3 3
(integer) 11
redis> LPOS mylist 3
(integer) 6
redis> LPOS mylist 3 COUNT 0 RANK 2
1) (integer) 8
2) (integer) 9
3) (integer) 10
```

返回列表中匹配元素的索引

### LPUSH

```{.wrap}
LPUSH key element [element ...]
```

#### 示例

```shell script
redis> LPUSH mylist "world"
(integer) 1
redis> LPUSH mylist "hello"
(integer) 2
redis> LRANGE mylist 0 -1
1) "hello"
2) "world"
```

将一个或多个元素前置到列表

### LPUSHX

```{.wrap}
LPUSHX key element [element ...]
```

#### 示例

```shell script
redis> LPUSH mylist "World"
(integer) 1
redis> LPUSHX mylist "Hello"
(integer) 2
redis> LPUSHX myotherlist "Hello"
(integer) 0
redis> LRANGE mylist 0 -1
1) "Hello"
2) "World"
redis> LRANGE myotherlist 0 -1
(empty list or set)
```

将一个元素前置到列表，仅当列表存在时

### LRANGE

```{.wrap}
LRANGE key start stop
```

#### 示例

```shell script
redis> RPUSH mylist "one"
(integer) 1
redis> RPUSH mylist "two"
(integer) 2
redis> RPUSH mylist "three"
(integer) 3
redis> LRANGE mylist 0 0
1) "one"
redis> LRANGE mylist -3 2
1) "one"
2) "two"
3) "three"
redis> LRANGE mylist -100 100
1) "one"
2) "two"
3) "three"
redis> LRANGE mylist 5 10
(empty list or set)
```

从列表中获取一个范围的元素

### LREM

```{.wrap}
LREM key count element
```

#### 示例

```shell script
redis> RPUSH mylist "hello"
(integer) 1
redis> RPUSH mylist "hello"
(integer) 2
redis> RPUSH mylist "foo"
(integer) 3
redis> RPUSH mylist "hello"
(integer) 4
redis> LREM mylist -2 "hello"
(integer) 2
redis> LRANGE mylist 0 -1
1) "hello"
2) "foo"
```

从列表中移除元素

### LSET

```{.wrap}
LSET key index element
```

#### 示例

```shell script
redis> RPUSH mylist "one"
(integer) 1
redis> RPUSH mylist "two"
(integer) 2
redis> RPUSH mylist "three"
(integer) 3
redis> LSET mylist 0 "four"
"OK"
redis> LSET mylist -2 "five"
"OK"
redis> LRANGE mylist 0 -1
1) "four"
2) "five"
3) "three"
```

通过索引设置列表中元素的值

### LTRIM

```{.wrap}
LTRIM key start stop
```

#### 示例

```shell script
redis> RPUSH mylist "one"
(integer) 1
redis> RPUSH mylist "two"
(integer) 2
redis> RPUSH mylist "three"
(integer) 3
redis> LTRIM mylist 1 -1
"OK"
redis> LRANGE mylist 0 -1
1) "two"
2) "three"
```

将列表修剪到指定范围

### RPOP

```{.wrap}
RPOP key [count]
```

#### 示例

```shell script
redis> RPUSH mylist "one"
(integer) 1
redis> RPUSH mylist "two"
(integer) 2
redis> RPUSH mylist "three"
(integer) 3
redis> RPOP mylist
"three"
redis> LRANGE mylist 0 -1
1) "one"
2) "two"
```

移除并获取列表中的最后一个元素

### RPOPLPUSH

```{.wrap}
RPOPLPUSH source destination
```

#### 示例

```shell script
redis> RPUSH mylist "one"
(integer) 1
redis> RPUSH mylist "two"
(integer) 2
redis> RPUSH mylist "three"
(integer) 3
redis> RPOPLPUSH mylist myotherlist
"three"
redis> LRANGE mylist 0 -1
1) "one"
2) "two"
redis> LRANGE myotherlist 0 -1
1) "three"
```

移除列表中的最后一个元素，将其前置到另一个列表并返回它

### LMOVE

```{.wrap}
LMOVE source destination LEFT|RIGHT LEFT|RIGHT
```

#### 示例

```shell script
redis> RPUSH mylist "one"
(integer) 1
redis> RPUSH mylist "two"
(integer) 2
redis> RPUSH mylist "three"
(integer) 3
redis> LMOVE mylist myotherlist RIGHT LEFT
"three"
redis> LMOVE mylist myotherlist LEFT RIGHT
"one"
redis> LRANGE mylist 0 -1
1) "two"
redis> LRANGE myotherlist 0 -1
1) "three"
2) "one"
```

从列表中弹出一个元素，将其推送到另一个列表并返回它

### RPUSH

```{.wrap}
RPUSH key element [element ...]
```

#### 示例

```shell script
redis> RPUSH mylist "hello"
(integer) 1
redis> RPUSH mylist "world"
(integer) 2
redis> LRANGE mylist 0 -1
1) "hello"
2) "world"
```

将一个或多个元素追加到列表

### RPUSHX

```{.wrap}
RPUSHX key element [element ...]
```

#### 示例

```shell script
redis> RPUSH mylist "Hello"
(integer) 1
redis> RPUSHX mylist "World"
(integer) 2
redis> RPUSHX myotherlist "World"
(integer) 0
redis> LRANGE mylist 0 -1
1) "Hello"
2) "World"
redis> LRANGE myotherlist 0 -1
(empty list or set)
```

将一个元素追加到列表，仅当列表存在时

## Redis 哈希命令

### HDEL

```{.wrap}
HDEL key field [field ...]
```

#### 示例

```shell script
redis> HSET myhash field1 "foo"
(integer) 1
redis> HDEL myhash field1
(integer) 1
redis> HDEL myhash field2
(integer) 0
```

删除一个或多个哈希字段

### HEXISTS

```{.wrap}
HEXISTS key field
```

#### 示例

```shell script
redis> HSET myhash field1 "foo"
(integer) 1
redis> HEXISTS myhash field1
(integer) 1
redis> HEXISTS myhash field2
(integer) 0
```

判断哈希字段是否存在

### HGET

```{.wrap}
HGET key field
```

#### 示例

```shell script
redis> HSET myhash field1 "foo"
(integer) 1
redis> HGET myhash field1
"foo"
redis> HGET myhash field2
(nil)
```

获取哈希字段的值

### HGETALL

```{.wrap}
HGETALL key
```

#### 示例

```shell script
redis> HSET myhash field1 "Hello"
(integer) 1
redis> HSET myhash field2 "World"
(integer) 1
redis> HGETALL myhash
1) "field1"
2) "Hello"
3) "field2"
4) "World"
```

获取哈希中的所有字段和值

### HINCRBY

```{.wrap}
HINCRBY key field increment
```

#### 示例

```shell script
redis> HSET myhash field 5
(integer) 1
redis> HINCRBY myhash field 1
(integer) 6
redis> HINCRBY myhash field -1
(integer) 5
redis> HINCRBY myhash field -10
(integer) -5
```

将哈希字段的整数值增加给定数量

### HINCRBYFLOAT

```{.wrap}
HINCRBYFLOAT key field increment
```

#### 示例

```shell script
redis> HSET mykey field 10.50
(integer) 1
redis> HINCRBYFLOAT mykey field 0.1
"10.6"
redis> HINCRBYFLOAT mykey field -5
"5.6"
redis> HSET mykey field 5.0e3
(integer) 0
redis> HINCRBYFLOAT mykey field 2.0e2
"5200"
```

将哈希字段的浮点值增加给定数量

### HKEYS

```{.wrap}
HKEYS key
```

#### 示例

```shell script
redis> HSET myhash field1 "Hello"
(integer) 1
redis> HSET myhash field2 "World"
(integer) 1
redis> HKEYS myhash
1) "field1"
2) "field2"
```

获取哈希中的所有字段

### HLEN

```{.wrap}
HLEN key
```

#### 示例

```shell script
redis> HSET myhash field1 "Hello"
(integer) 1
redis> HSET myhash field2 "World"
(integer) 1
redis> HLEN myhash
(integer) 2
```

获取哈希中的字段数量

### HMGET

```{.wrap}
HMGET key field [field ...]
```

#### 示例

```shell script
redis> HSET myhash field1 "Hello"
(integer) 1
redis> HSET myhash field2 "World"
(integer) 1
redis> HMGET myhash field1 field2 nofield
1) "Hello"
2) "World"
3) (nil)
```

获取所有给定哈希字段的值

### HMSET

```{.wrap}
HMSET key field value [field value ...]
```

#### 示例

```shell script
redis> HMSET myhash field1 "Hello" field2 "World"
"OK"
redis> HGET myhash field1
"Hello"
redis> HGET myhash field2
"World"
```

将多个哈希字段设置为多个值

### HSET

```{.wrap}
HSET key field value [field value ...]
```

#### 示例

```shell script
redis> HSET myhash field1 "Hello"
(integer) 1
redis> HGET myhash field1
"Hello"
```

设置哈希字段的字符串值

### HSETNX

```{.wrap}
HSETNX key field value
```

#### 示例

```shell script
redis> HSETNX myhash field "Hello"
(integer) 1
redis> HSETNX myhash field "World"
(integer) 0
redis> HGET myhash field
"Hello"
```

设置哈希字段的值，仅当字段不存在时

### HSTRLEN

```{.wrap}
HSTRLEN key field
```

#### 示例

```shell script
redis> HMSET myhash f1 HelloWorld f2 99 f3 -256
"OK"
redis> HSTRLEN myhash f1
(integer) 10
redis> HSTRLEN myhash f2
(integer) 2
redis> HSTRLEN myhash f3
(integer) 4
```

获取哈希字段值的长度

### HVALS

```{.wrap}
HVALS key
```

#### 示例

```shell script
redis> HSET myhash field1 "Hello"
(integer) 1
redis> HSET myhash field2 "World"
(integer) 1
redis> HVALS myhash
1) "Hello"
2) "World"
```

获取哈希中的所有值

## Redis 有序集合命令

### BZPOPMIN

```{.wrap}
BZPOPMIN key [key ...] timeout
```

#### 示例

```shell script
redis> DEL zset1 zset2
(integer) 0
redis> ZADD zset1 0 a 1 b 2 c
(integer) 3
redis> BZPOPMIN zset1 zset2 0
1) "zset1"
2) "a"
3) "0"
```

从一个或多个有序集合中移除并返回得分最低的成员，或阻塞直到有可用成员

### BZPOPMAX

```{.wrap}
BZPOPMAX key [key ...] timeout
```

#### 示例

```shell script
redis> DEL zset1 zset2
(integer) 0
redis> ZADD zset1 0 a 1 b 2 c
(integer) 3
redis> BZPOPMAX zset1 zset2 0
1) "zset1"
2) "c"
3) "2"
```

从一个或多个有序集合中移除并返回得分最高的成员，或阻塞直到有可用成员

### ZADD {.row-span-2}

```{.wrap}
ZADD key [NX|XX] [GT|LT] [CH] [INCR] score member [score member ...]
```

#### 示例

```shell script
redis> ZADD myzset 1 "one"
(integer) 1
redis> ZADD myzset 1 "uno"
(integer) 1
redis> ZADD myzset 2 "two" 3 "three"
(integer) 2
redis> ZRANGE myzset 0 -1 WITHSCORES
1) "one"
2) "1"
3) "uno"
4) "1"
5) "two"
6) "2"
7) "three"
8) "3"
```

向有序集合添加一个或多个成员，如果成员已存在则更新其得分

### ZCARD

```{.wrap}
ZCARD key
```

#### 示例

```shell script
redis> ZADD myzset 1 "one"
(integer) 1
redis> ZADD myzset 2 "two"
(integer) 1
redis> ZCARD myzset
(integer) 2
```

获取有序集合中的成员数量

### ZSCORE

```{.wrap}
ZSCORE key member
```

#### 示例

```shell script
redis> ZADD myzset 1 "one"
(integer) 1
redis> ZSCORE myzset "one"
"1"
```

获取有序集合中给定成员的得分

### ZCOUNT

```{.wrap}
ZCOUNT key min max
```

#### 示例

```shell script
redis> ZADD myzset 1 "one"
(integer) 1
redis> ZADD myzset 2 "two"
(integer) 1
redis> ZADD myzset 3 "three"
(integer) 1
redis> ZCOUNT myzset -inf +inf
(integer) 3
redis> ZCOUNT myzset (1 3
(integer) 2
```

计算有序集合中得分在给定范围内的成员数量

### ZDIFF

```{.wrap}
ZDIFF numkeys key [key ...] [WITHSCORES]
```

#### 示例

```shell script
redis> ZADD zset1 1 "one"
(integer) 1
redis> ZADD zset1 2 "two"
(integer) 1
redis> ZADD zset1 3 "three"
(integer) 1
redis> ZADD zset2 1 "one"
(integer) 1
redis> ZADD zset2 2 "two"
(integer) 1
redis> ZDIFF 2 zset1 zset2
1) "three"
redis> ZDIFF 2 zset1 zset2 WITHSCORES
1) "three"
2) "3"
```

计算多个有序集合的差集

### ZDIFFSTORE

```{.wrap}
ZDIFFSTORE destination numkeys key [key ...]
```

#### 示例

```shell script
redis> ZADD zset1 1 "one"
(integer) 1
redis> ZADD zset1 2 "two"
(integer) 1
redis> ZADD zset1 3 "three"
(integer) 1
redis> ZADD zset2 1 "one"
(integer) 1
redis> ZADD zset2 2 "two"
(integer) 1
redis> ZDIFFSTORE out 2 zset1 zset2
(integer) 1
redis> ZRANGE out 0 -1 WITHSCORES
1) "three"
2) "3"
```

计算多个有序集合的差集并将结果有序集合存储在新键中

### ZINCRBY

```{.wrap}
ZINCRBY key increment member
```

#### 示例

```shell script
redis> ZADD myzset 1 "one"
(integer) 1
redis> ZADD myzset 2 "two"
(integer) 1
redis> ZINCRBY myzset 2 "one"
"3"
redis> ZRANGE myzset 0 -1 WITHSCORES
1) "two"
2) "2"
3) "one"
4) "3"
```

增加有序集合中成员的得分

### ZINTER

```{.wrap}
ZINTER numkeys key [key ...] [WEIGHTS weight [weight ...]] [AGGREGATE SUM|MIN|MAX] [WITHSCORES]
```

#### 示例

```shell script
redis> ZADD zset1 1 "one"
(integer) 1
redis> ZADD zset1 2 "two"
(integer) 1
redis> ZADD zset2 1 "one"
(integer) 1
redis> ZADD zset2 2 "two"
(integer) 1
redis> ZADD zset2 3 "three"
(integer) 1
redis> ZINTER 2 zset1 zset2
1) "one"
2) "two"
redis> ZINTER 2 zset1 zset2 WITHSCORES
1) "one"
2) "2"
3) "two"
4) "4"
```

计算多个有序集合的交集

### ZINTERSTORE

```{.wrap}
ZINTERSTORE destination numkeys key [key ...] [WEIGHTS weight [weight ...]] [AGGREGATE SUM|MIN|MAX]
```

#### 示例

```shell script
redis> ZADD zset1 1 "one"
(integer) 1
redis> ZADD zset1 2 "two"
(integer) 1
redis> ZADD zset2 1 "one"
(integer) 1
redis> ZADD zset2 2 "two"
(integer) 1
redis> ZADD zset2 3 "three"
(integer) 1
redis> ZINTERSTORE out 2 zset1 zset2 WEIGHTS 2 3
(integer) 2
redis> ZRANGE out 0 -1 WITHSCORES
1) "one"
2) "5"
3) "two"
4) "10"
```

计算多个有序集合的交集并将结果有序集合存储在新键中

### ZLEXCOUNT

```{.wrap}
ZLEXCOUNT key min max
```

#### 示例

```shell script
redis> ZADD myzset 0 a 0 b 0 c 0 d 0 e
(integer) 5
redis> ZADD myzset 0 f 0 g
(integer) 2
redis> ZLEXCOUNT myzset - +
(integer) 7
redis> ZLEXCOUNT myzset [b [f
(integer) 5
```

计算有序集合中在给定字典序范围内的成员数量

### ZPOPMAX

```{.wrap}
ZPOPMAX key [count]
```

#### 示例

```shell script
redis> ZADD myzset 1 "one"
(integer) 1
redis> ZADD myzset 2 "two"
(integer) 1
redis> ZADD myzset 3 "three"
(integer) 1
redis> ZPOPMAX myzset
1) "three"
2) "3"
```

移除并返回有序集合中得分最高的成员

### ZPOPMIN

```{.wrap}
ZPOPMIN key [count]
```

#### 示例

```shell script
redis> ZADD myzset 1 "one"
(integer) 1
redis> ZADD myzset 2 "two"
(integer) 1
redis> ZADD myzset 3 "three"
(integer) 1
redis> ZPOPMIN myzset
1) "one"
2) "1"
```

移除并返回有序集合中得分最低的成员

### ZRANGE

```{.wrap}
ZRANGE key start stop [WITHSCORES]
```

#### 示例

```shell script
redis> ZADD myzset 1 "one"
(integer) 1
redis> ZADD myzset 2 "two"
(integer) 1
redis> ZADD myzset 3 "three"
(integer) 1
redis> ZRANGE myzset 0 -1
1) "one"
2) "two"
3) "three"
redis> ZRANGE myzset 2 3
1) "three"
redis> ZRANGE myzset -2 -1
1) "two"
2) "three"
```

按索引返回有序集合中的成员范围

### ZRANGEBYLEX

```{.wrap}
ZRANGEBYLEX key min max [LIMIT offset count]
```

#### 示例

```shell script
redis> ZADD myzset 0 a 0 b 0 c 0 d 0 e 0 f 0 g
(integer) 7
redis> ZRANGEBYLEX myzset - [c
1) "a"
2) "b"
3) "c"
redis> ZRANGEBYLEX myzset - (c
1) "a"
2) "b"
redis> ZRANGEBYLEX myzset [aaa (g
1) "b"
2) "c"
3) "d"
4) "e"
5) "f"
```

按字典序范围返回有序集合中的成员范围

### ZREVRANGEBYLEX

```{.wrap}
ZREVRANGEBYLEX key max min [LIMIT offset count]
```

#### 示例

```shell script
redis> ZADD myzset 0 a 0 b 0 c 0 d 0 e 0 f 0 g
(integer) 7
redis> ZREVRANGEBYLEX myzset [c -
1) "c"
2) "b"
3) "a"
redis> ZREVRANGEBYLEX myzset (c -
1) "b"
2) "a"
redis> ZREVRANGEBYLEX myzset (g [aaa
1) "f"
2) "e"
3) "d"
4) "c"
5) "b"
```

按字典序范围返回有序集合中的成员范围，按从高到低的字符串顺序排列。

### ZRANGEBYSCORE

```{.wrap}
ZRANGEBYSCORE key min max [WITHSCORES] [LIMIT offset count]
```

#### 示例

```shell script
redis> ZADD myzset 1 "one"
(integer) 1
redis> ZADD myzset 2 "two"
(integer) 1
redis> ZADD myzset 3 "three"
(integer) 1
redis> ZRANGEBYSCORE myzset -inf +inf
1) "one"
2) "two"
3) "three"
redis> ZRANGEBYSCORE myzset 1 2
1) "one"
2) "two"
redis> ZRANGEBYSCORE myzset (1 2
1) "two"
redis> ZRANGEBYSCORE myzset (1 (2
(empty list or set)
```

按得分返回有序集合中的成员范围

### ZRANK

```{.wrap}
ZRANK key member
```

#### 示例

```shell script
redis> ZADD myzset 1 "one"
(integer) 1
redis> ZADD myzset 2 "two"
(integer) 1
redis> ZADD myzset 3 "three"
(integer) 1
redis> ZRANK myzset "three"
(integer) 2
redis> ZRANK myzset "four"
(nil)
```

确定成员在有序集合中的索引

### ZREM

```{.wrap}
ZREM key member [member ...]
```

#### 示例

```shell script
redis> ZADD myzset 1 "one"
(integer) 1
redis> ZADD myzset 2 "two"
(integer) 1
redis> ZADD myzset 3 "three"
(integer) 1
redis> ZREM myzset "two"
(integer) 1
redis> ZRANGE myzset 0 -1 WITHSCORES
1) "one"
2) "1"
3) "three"
4) "3"
```

从有序集合中移除一个或多个成员

### ZREMRANGEBYLEX

```{.wrap}
ZREMRANGEBYLEX key min max
```

#### 示例

```shell script
redis> ZADD myzset 0 aaaa 0 b 0 c 0 d 0 e
(integer) 5
redis> ZADD myzset 0 foo 0 zap 0 zip 0 ALPHA 0 alpha
(integer) 5
redis> ZRANGE myzset 0 -1
1) "ALPHA"
 2) "aaaa"
 3) "alpha"
 4) "b"
 5) "c"
 6) "d"
 7) "e"
 8) "foo"
 9) "zap"
10) "zip"
redis> ZREMRANGEBYLEX myzset [alpha [omega
(integer) 6
redis> ZRANGE myzset 0 -1
1) "ALPHA"
2) "aaaa"
3) "zap"
4) "zip"
```

移除有序集合中给定字典序范围内的所有成员

### ZREMRANGEBYRANK

```{.wrap}
ZREMRANGEBYRANK key start stop
```

#### 示例

```shell script
redis> ZADD myzset 1 "one"
(integer) 1
redis> ZADD myzset 2 "two"
(integer) 1
redis> ZADD myzset 3 "three"
(integer) 1
redis> ZREMRANGEBYRANK myzset 0 1
(integer) 2
redis> ZRANGE myzset 0 -1 WITHSCORES
1) "three"
2) "3"
```

移除有序集合中给定索引范围内的所有成员

### ZREMRANGEBYSCORE

```{.wrap}
ZREMRANGEBYSCORE key min max
```

#### 示例

```shell script
redis> ZADD myzset 1 "one"
(integer) 1
redis> ZADD myzset 2 "two"
(integer) 1
redis> ZADD myzset 3 "three"
(integer) 1
redis> ZREMRANGEBYSCORE myzset -inf (2
(integer) 1
redis> ZRANGE myzset 0 -1 WITHSCORES
1) "two"
2) "2"
3) "three"
4) "3"
```

移除有序集合中给定得分范围内的所有成员

### ZREVRANGE

```{.wrap}
ZREVRANGE key start stop [WITHSCORES]
```

#### 示例

```shell script
redis> ZADD myzset 1 "one"
(integer) 1
redis> ZADD myzset 2 "two"
(integer) 1
redis> ZADD myzset 3 "three"
(integer) 1
redis> ZREVRANGE myzset 0 -1
1) "three"
2) "two"
3) "one"
redis> ZREVRANGE myzset 2 3
1) "one"
redis> ZREVRANGE myzset -2 -1
1) "two"
2) "one"
```

按索引返回有序集合中的成员范围，得分从高到低排序

### ZREVRANGEBYSCORE

```{.wrap}
ZREVRANGEBYSCORE key max min [WITHSCORES] [LIMIT offset count]
```

#### 示例

```shell script
redis> ZADD myzset 1 "one"
(integer) 1
redis> ZADD myzset 2 "two"
(integer) 1
redis> ZADD myzset 3 "three"
(integer) 1
redis> ZREVRANGEBYSCORE myzset +inf -inf
1) "three"
2) "two"
3) "one"
redis> ZREVRANGEBYSCORE myzset 2 1
1) "two"
2) "one"
redis> ZREVRANGEBYSCORE myzset 2 (1
1) "two"
redis> ZREVRANGEBYSCORE myzset (2 (1
(empty list or set)
```

按得分返回有序集合中的成员范围，得分从高到低排序

### ZREVRANK

```{.wrap}
ZREVRANK key member
```

#### 示例

```shell script
redis> ZADD myzset 1 "one"
(integer) 1
redis> ZADD myzset 2 "two"
(integer) 1
redis> ZADD myzset 3 "three"
(integer) 1
redis> ZREVRANK myzset "one"
(integer) 2
redis> ZREVRANK myzset "four"
(nil)
```

确定成员在有序集合中的索引，得分从高到低排序

### ZUNION

```{.wrap}
ZUNION numkeys key [key ...] [WEIGHTS weight [weight ...]] [AGGREGATE SUM|MIN|MAX] [WITHSCORES]
```

#### 示例

```shell script
redis> ZADD zset1 1 "one"
(integer) 1
redis> ZADD zset1 2 "two"
(integer) 1
redis> ZADD zset2 1 "one"
(integer) 1
redis> ZADD zset2 2 "two"
(integer) 1
redis> ZADD zset2 3 "three"
(integer) 1
redis> ZUNION 2 zset1 zset2
1) "one"
2) "three"
3) "two"
redis> ZUNION 2 zset1 zset2 WITHSCORES
1) "one"
2) "2"
3) "three"
4) "3"
5) "two"
6) "4"
```

计算多个有序集合的并集

### ZMSCORE

```{.wrap}
ZMSCORE key member [member ...]
```

#### 示例

```shell script
redis> ZADD myzset 1 "one"
(integer) 1
redis> ZADD myzset 2 "two"
(integer) 1
redis> ZMSCORE myzset "one" "two" "nofield"
1) "1"
2) "2"
3) (nil)
```

获取有序集合中给定成员的得分

### ZUNIONSTORE

```{.wrap}
ZUNIONSTORE destination numkeys key [key ...] [WEIGHTS weight [weight ...]] [AGGREGATE SUM|MIN|MAX]
```

#### 示例

```shell script
redis> ZADD zset1 1 "one"
(integer) 1
redis> ZADD zset1 2 "two"
(integer) 1
redis> ZADD zset2 1 "one"
(integer) 1
redis> ZADD zset2 2 "two"
(integer) 1
redis> ZADD zset2 3 "three"
(integer) 1
redis> ZUNIONSTORE out 2 zset1 zset2 WEIGHTS 2 3
(integer) 3
redis> ZRANGE out 0 -1 WITHSCORES
1) "one"
2) "5"
3) "three"
4) "9"
5) "two"
6) "10"
```

计算多个有序集合的并集并将结果有序集合存储在新键中

## Redis 地理空间命令{.cols-2}

### GEOADD

```{.wrap}
GEOADD key longitude latitude member [longitude latitude member ...]
```

#### 示例

```shell script
redis> GEOADD Sicily 13.361389 38.115556 "Palermo" 15.087269 37.502669 "Catania"
(integer) 2
redis> GEODIST Sicily Palermo Catania
"166274.1516"
redis> GEORADIUS Sicily 15 37 100 km
1) "Catania"
redis> GEORADIUS Sicily 15 37 200 km
1) "Palermo"
2) "Catania"
```

将一个或多个地理空间项添加到使用有序集合表示的地理空间索引中

### GEOHASH

```{.wrap}
GEOHASH key member [member ...]
```

#### 示例

```shell script
redis> GEOADD Sicily 13.361389 38.115556 "Palermo" 15.087269 37.502669 "Catania"
(integer) 2
redis> GEOHASH Sicily Palermo Catania
1) "sqc8b49rny0"
2) "sqdtr74hyu0"
```

以标准 geohash 字符串形式返回地理空间索引的成员

### GEOPOS

```{.wrap}
GEOPOS key member [member ...]
```

#### 示例

```shell script
redis> GEOADD Sicily 13.361389 38.115556 "Palermo" 15.087269 37.502669 "Catania"
(integer) 2
redis> GEOPOS Sicily Palermo Catania NonExisting
1) 1) "13.36138933897018433"
   2) "38.11555639549629859"
2) 1) "15.08726745843887329"
   2) "37.50266842333162032"
3) (nil)
```

返回地理空间索引成员的经度和纬度

### GEODIST

```{.wrap}
GEODIST key member1 member2 [m|km|ft|mi]
```

#### 示例

```shell script
redis> GEOADD Sicily 13.361389 38.115556 "Palermo" 15.087269 37.502669 "Catania"
(integer) 2
redis> GEODIST Sicily Palermo Catania
"166274.1516"
redis> GEODIST Sicily Palermo Catania km
"166.2742"
redis> GEODIST Sicily Palermo Catania mi
"103.3182"
redis> GEODIST Sicily Foo Bar
(nil)
```

返回地理空间索引中两个成员之间的距离

### GEORADIUS

```{.wrap}
GEORADIUS key longitude latitude radius m|km|ft|mi [WITHCOORD] [WITHDIST] [WITHHASH] [COUNT count] [ASC|DESC] [STORE key] [STOREDIST key]
```

#### 示例

```shell script
redis> GEOADD Sicily 13.361389 38.115556 "Palermo" 15.087269 37.502669 "Catania"
(integer) 2
redis> GEORADIUS Sicily 15 37 200 km WITHDIST
1) 1) "Palermo"
   2) "190.4424"
2) 1) "Catania"
   2) "56.4413"
redis> GEORADIUS Sicily 15 37 200 km WITHCOORD
1) 1) "Palermo"
   2) 1) "13.36138933897018433"
      2) "38.11555639549629859"
2) 1) "Catania"
   2) 1) "15.08726745843887329"
      2) "37.50266842333162032"
redis> GEORADIUS Sicily 15 37 200 km WITHDIST WITHCOORD
1) 1) "Palermo"
   2) "190.4424"
   3) 1) "13.36138933897018433"
      2) "38.11555639549629859"
2) 1) "Catania"
   2) "56.4413"
   3) 1) "15.08726745843887329"
      2) "37.50266842333162032"
```

查询表示地理空间索引的有序集合，以获取与给定点最大距离匹配的成员

### GEORADIUSBYMEMBER

```{.wrap}
GEORADIUSBYMEMBER key member radius m|km|ft|mi [WITHCOORD] [WITHDIST] [WITHHASH] [COUNT count] [ASC|DESC] [STORE key] [STOREDIST key]
```

#### 示例

```shell script
redis> GEOADD Sicily 13.583333 37.316667 "Agrigento"
(integer) 1
redis> GEOADD Sicily 13.361389 38.115556 "Palermo" 15.087269 37.502669 "Catania"
(integer) 2
redis> GEORADIUSBYMEMBER Sicily Agrigento 100 km
1) "Agrigento"
2) "Palermo"
```

查询表示地理空间索引的有序集合，以获取与给定成员最大距离匹配的成员

### GEOSEARCH

```{.wrap}
GEOSEARCH key [FROMMEMBER member] [FROMLONLAT longitude latitude] [BYRADIUS radius m|km|ft|mi] [BYBOX width height m|km|ft|mi] [ASC|DESC] [COUNT count] [WITHCOORD] [WITHDIST] [WITHHASH]
```

#### 示例

```shell script
redis> GEOADD Sicily 13.361389 38.115556 "Palermo" 15.087269 37.502669 "Catania"
(integer) 2
redis> GEOADD Sicily 12.758489 38.788135 "edge1"   17.241510 38.788135 "edge2"
(integer) 2
redis> GEOSEARCH Sicily FROMLONLAT 15 37 BYRADIUS 200 km ASC
1) "Catania"
2) "Palermo"
redis> GEOSEARCH Sicily FROMLONLAT 15 37 BYBOX 400 400 km ASC
1) "Catania"
2) "Palermo"
3) "edge2"
4) "edge1"
```

查询表示地理空间索引的有序集合，以获取在矩形或圆形区域内的成员。

### Misc

| -                                                           | -                                                                                                                                             |
| ----------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------- |
| [GEOSEARCHSTORE ](https://redis.io/commands/geosearchstore) | 查询表示地理空间索引的有序集合，以获取在矩形或圆形区域内的成员，并将结果存储在另一个键中。                                                              |

## Redis HyperLogLog 命令{.cols-3}

### PFADD

```{.wrap}
PFADD key element [element ...]
```

#### 示例

```shell script
redis> PFADD hll a b c d e f g
(integer) 1
redis> PFCOUNT hll
(integer) 7
```

将指定元素添加到指定的 HyperLogLog。

### PFCOUNT

```{.wrap}
PFCOUNT key [key ...]
```

#### 示例

```shell script
redis> PFADD hll foo bar zap
(integer) 1
redis> PFADD hll zap zap zap
(integer) 0
redis> PFADD hll foo bar
(integer) 0
redis> PFCOUNT hll
(integer) 3
redis> PFADD some-other-hll 1 2 3
(integer) 1
redis> PFCOUNT hll some-other-hll
(integer) 6
```

返回 HyperLogLog 在键处观察到的集合的近似基数。

### PFMERGE

```{.wrap}
PFMERGE destkey sourcekey [sourcekey ...]
```

#### 示例

```shell script
redis> PFADD hll1 foo bar zap a
(integer) 1
redis> PFADD hll2 a b c foo
(integer) 1
redis> PFMERGE hll3 hll1 hll2
"OK"
redis> PFCOUNT hll3
(integer) 6
```

将 N 个不同的 HyperLogLog 合并为一个。

## Redis 服务器命令{.cols-3}

### COMMAND

```{.wrap}
COMMAND
```

#### 示例

```shell script
redis> COMMAND
1) 1) "georadius_ro"
     2) (integer) -6
     3) 1) "readonly"
        2) "movablekeys"
     4) (integer) 1
     5) (integer) 1
     6) (integer) 1
     7) 1) "@read"
        2) "@geo"
        3) "@slow"
  2) 1) "zpopmin"
     2) (integer) -2
     3) 1) "write"
        2) "fast"
  ........
```

获取 Redis 命令详细信息的数组

### Misc {.col-span-2 .row-span-4}

| -                                                                    | -                                                                                                                                |
| -------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------- |
| [ACL LOAD](https://redis.io/commands/acl-load)                       | 从配置的 ACL 文件重新加载 ACL                                                                                                      |
| [ACL SAVE](https://redis.io/commands/acl-save)                       | 将当前 ACL 规则保存在配置的 ACL 文件中                                                                                               |
| [ACL LIST](https://redis.io/commands/acl-list)                       | 以 ACL 配置文件格式列出当前 ACL 规则                                                                                               |
| [ACL USERS](https://redis.io/commands/acl-users)                     | 列出所有已配置 ACL 规则的用户名                                                                                                    |
| [ACL GETUSER ](https://redis.io/commands/acl-getuser)                | 获取特定 ACL 用户的规则                                                                                                          |
| [ACL SETUSER ](https://redis.io/commands/acl-setuser)                | 修改或创建特定 ACL 用户的规则                                                                                                      |
| [ACL DELUSER ](https://redis.io/commands/acl-deluser)                | 删除指定的 ACL 用户和关联规则                                                                                                      |
| [ACL CAT ](https://redis.io/commands/acl-cat)                        | 列出 ACL 类别或类别中的命令                                                                                                        |
| [ACL GENPASS ](https://redis.io/commands/acl-genpass)                | 生成一个伪随机安全密码供 ACL 用户使用                                                                                                |
| [ACL WHOAMI](https://redis.io/commands/acl-whoami)                   | 返回与当前连接关联的用户名                                                                                                         |
| [ACL LOG ](https://redis.io/commands/acl-log)                        | 列出由于 ACL 规则而被拒绝的最新事件                                                                                                  |
| [ACL HELP](https://redis.io/commands/acl-help)                       | 显示有关不同子命令的帮助文本                                                                                                       |
| [BGREWRITEAOF](https://redis.io/commands/bgrewriteaof)               | 异步重写仅追加文件                                                                                                               |
| [BGSAVE ](https://redis.io/commands/bgsave)                          | 异步将数据集保存到磁盘                                                                                                             |
| [CONFIG GET ](https://redis.io/commands/config-get)                  | 获取配置参数的值                                                                                                                 |
| [CONFIG REWRITE](https://redis.io/commands/config-rewrite)           | 使用内存中的配置重写配置文件                                                                                                       |
| [CONFIG SET ](https://redis.io/commands/config-set)                  | 将配置参数设置为给定值                                                                                                             |
| [CONFIG RESETSTAT](https://redis.io/commands/config-resetstat)       | 重置 INFO 返回的统计信息                                                                                                           |
| [DBSIZE](https://redis.io/commands/dbsize)                           | 返回所选数据库中的键数                                                                                                             |
| [DEBUG OBJECT ](https://redis.io/commands/debug-object)              | 获取有关键的调试信息                                                                                                               |
| [DEBUG SEGFAULT](https://redis.io/commands/debug-segfault)           | 使服务器崩溃                                                                                                                     |
| [FLUSHALL ](https://redis.io/commands/flushall)                      | 从所有数据库中删除所有键                                                                                                           |
| [FLUSHDB ](https://redis.io/commands/flushdb)                        | 从当前数据库中删除所有键                                                                                                           |
| [LOLWUT ](https://redis.io/commands/lolwut)                          | 显示一些计算机艺术和 Redis 版本                                                                                                    |
| [LASTSAVE](https://redis.io/commands/lastsave)                       | 获取上次成功保存到磁盘的 UNIX 时间戳                                                                                                 |
| [MEMORY DOCTOR](https://redis.io/commands/memory-doctor)             | 输出内存问题报告                                                                                                                 |
| [MEMORY HELP](https://redis.io/commands/memory-help)                 | 显示有关不同子命令的帮助文本                                                                                                       |
| [MEMORY MALLOC-STATS](https://redis.io/commands/memory-malloc-stats) | 显示分配器内部统计信息                                                                                                             |
| [MEMORY PURGE](https://redis.io/commands/memory-purge)               | 要求分配器释放内存                                                                                                               |
| [MEMORY STATS](https://redis.io/commands/memory-stats)               | 显示内存使用情况详细信息                                                                                                           |
| [MEMORY USAGE ](https://redis.io/commands/memory-usage)              | 估计键的内存使用情况                                                                                                               |
| [MODULE LIST](https://redis.io/commands/module-list)                 | 列出服务器加载的所有模块                                                                                                           |
| [MODULE LOAD ](https://redis.io/commands/module-load)                | 加载模块                                                                                                                         |
| [MODULE UNLOAD ](https://redis.io/commands/module-unload)            | 卸载模块                                                                                                                         |
| [MONITOR](https://redis.io/commands/monitor)                         | 实时侦听服务器收到的所有请求                                                                                                       |
| [SAVE](https://redis.io/commands/save)                               | 同步将数据集保存到磁盘                                                                                                             |
| [SHUTDOWN ](https://redis.io/commands/shutdown)                      | 同步将数据集保存到磁盘，然后关闭服务器                                                                                               |
| [SLAVEOF ](https://redis.io/commands/slaveof)                        | 使服务器成为另一个实例的副本，或将其提升为主服务器。从 Redis 5 开始弃用。请改用 REPLICAOF。                                                  |
| [REPLICAOF ](https://redis.io/commands/replicaof)                    | 使服务器成为另一个实例的副本，或将其提升为主服务器。                                                                                     |
| [SLOWLOG ](https://redis.io/commands/slowlog)                        | 管理 Redis 慢查询日志                                                                                                              |
| [SWAPDB ](https://redis.io/commands/swapdb)                          | 交换两个 Redis 数据库                                                                                                              |
| [SYNC](https://redis.io/commands/sync)                               | 用于复制的内部命令                                                                                                               |
| [PSYNC ](https://redis.io/commands/psync)                            | 用于复制的内部命令                                                                                                               |
| [LATENCY DOCTOR](https://redis.io/commands/latency-doctor)           | 返回人类可读的延迟分析报告。                                                                                                       |
| [LATENCY GRAPH ](https://redis.io/commands/latency-graph)            | 返回事件的延迟图。                                                                                                               |
| [LATENCY HISTORY ](https://redis.io/commands/latency-history)        | 返回事件的时间戳延迟样本。                                                                                                         |
| [LATENCY LATEST](https://redis.io/commands/latency-latest)           | 返回所有事件的最新延迟样本。                                                                                                       |
| [LATENCY RESET ](https://redis.io/commands/latency-reset)            | 重置一个或多个事件的延迟数据。                                                                                                     |
| [LATENCY HELP](https://redis.io/commands/latency-help)               | 显示有关不同子命令的帮助文本。                                                                                                     |

### COMMAND COUNT

```{.wrap}
COMMAND COUNT
```

#### 示例

```shell script
redis> COMMAND COUNT
(integer) 217
```

获取 Redis 命令总数

### COMMAND GETKEYS

```{.wrap}
COMMAND GETKEYS
```

#### 示例

```shell script
redis> COMMAND GETKEYS MSET a b c d e f
1) "a"
2) "c"
3) "e"
redis> COMMAND GETKEYS EVAL "not consulted" 3 key1 key2 key3 arg1 arg2 arg3 argN
1) "key1"
2) "key2"
3) "key3"
redis> COMMAND GETKEYS SORT mylist ALPHA STORE outlist
1) "mylist"
2) "outlist"
```

给定完整的 Redis 命令，提取键

### COMMAND INFO

```{.wrap}
COMMAND INFO command-name [command-name ...]
```

#### 示例

```shell script
redis> COMMAND INFO get set eval
1) 1) "get"
   2) (integer) 2
   3) 1) "readonly"
      2) "fast"
   4) (integer) 1
   5) (integer) 1
   6) (integer) 1
   7) 1) "@read"
      2) "@string"
      3) "@fast"
2) 1) "set"
   2) (integer) -3
   3) 1) "write"
      2) "denyoom"
   4) (integer) 1
   5) (integer) 1
   6) (integer) 1
   7) 1) "@write"
      2) "@string"
      3) "@slow"
3) 1) "eval"
   2) (integer) -3
   3) 1) "noscript"
      2) "movablekeys"
   4) (integer) 0
   5) (integer) 0
   6) (integer) 0
   7) 1) "@slow"
      2) "@scripting"
```

获取特定 Redis 命令详细信息的数组

### INFO

```{.wrap}
INFO [section]
```

#### 示例

```shell script
redis> INFO
# Server
redis_version:6.1.240
redis_git_sha1:00000000
redis_git_dirty:0
redis_build_id:a26db646ea64a07c
redis_mode:standalone
os:Linux 5.4.0-1017-aws x86_64
......
```

获取有关服务器的信息和统计信息

### ROLE

```{.wrap}
ROLE
```

#### 示例

```shell script
redis> ROLE
1) "master"
2) (integer) 0
3) (empty list or set)
```

返回实例在复制上下文中的角色

### TIME

```{.wrap}
TIME
```

#### 示例

```shell script
redis> TIME
1) "1609040690"
2) "558952"
redis> TIME
1) "1609040690"
2) "559206"
```

返回当前服务器时间

## Redis 通用命令{.cols-3}

### Misc

| -                                             | -                                                                                                            |
| --------------------------------------------- | ------------------------------------------------------------------------------------------------------------ |
| [COPY ](https://redis.io/commands/copy)       | 复制一个键                                                                                                   |
| [MIGRATE ](https://redis.io/commands/migrate) | 原子地将一个键从一个 Redis 实例传输到另一个实例。                                                                |
| [MOVE ](https://redis.io/commands/move)       | 将一个键移动到另一个数据库                                                                                       |
| [OBJECT ](https://redis.io/commands/object)   | 检查 Redis 对象的内部结构                                                                                      |
| [RESTORE ](https://redis.io/commands/restore) | 使用提供的序列化值创建一个键，该值先前使用 DUMP 获取。                                                               |
| [SORT ](https://redis.io/commands/sort)       | 对列表、集合或有序集合中的元素进行排序                                                                               |
| [WAIT ](https://redis.io/commands/wait)       | 等待当前连接上下文中发送的所有写命令的同步复制                                                                       |
| [SCAN ](https://redis.io/commands/scan)       | 增量迭代键空间                                                                                                 |

### DEL

```{.wrap}
DEL key [key ...]
```

#### 示例

```shell script
redis> SET key1 "Hello"
"OK"
redis> SET key2 "World"
"OK"
redis> DEL key1 key2 key3
(integer) 2
```

删除一个键

### DUMP

```{.wrap}
DUMP key
```

#### 示例

```shell script
redis> SET mykey 10
"OK"
redis> DUMP mykey
"\u0000\xC0\n\t\u0000\xBEm\u0006\x89Z(\u0000\n"
```

返回存储在指定键处的值的序列化版本。

### EXISTS

```{.wrap}
EXISTS key [key ...]
```

#### 示例

```shell script
redis> SET key1 "Hello"
"OK"
redis> EXISTS key1
(integer) 1
redis> EXISTS nosuchkey
(integer) 0
redis> SET key2 "World"
"OK"
redis> EXISTS key1 key2 nosuchkey
(integer) 2
```

判断一个键是否存在

### EXPIRE

```{.wrap}
EXPIRE key seconds
```

#### 示例

```shell script
redis> SET mykey "Hello"
"OK"
redis> EXPIRE mykey 10
(integer) 1
redis> TTL mykey
(integer) 10
redis> SET mykey "Hello World"
"OK"
redis> TTL mykey
(integer) -1
```

以秒为单位设置键的生存时间

### EXPIREAT

```{.wrap}
EXPIREAT key timestamp
```

#### 示例

```shell script
redis> SET mykey "Hello"
"OK"
redis> EXISTS mykey
(integer) 1
redis> EXPIREAT mykey 1293840000
(integer) 1
redis> EXISTS mykey
(integer) 0
```

以 UNIX 时间戳设置键的过期时间

### KEYS

```{.wrap}
KEYS pattern
```

#### 示例

```shell script
redis> MSET firstname Jack lastname Stuntman age 35
"OK"
redis> KEYS *name*
1) "firstname"
2) "lastname"
redis> KEYS a??
1) "age"
redis> KEYS *
1) "firstname"
2) "age"
3) "lastname"
```

查找所有匹配给定模式的键

### PERSIST

```{.wrap}
PERSIST key
```

#### 示例

```shell script
redis> SET mykey "Hello"
"OK"
redis> EXPIRE mykey 10
(integer) 1
redis> TTL mykey
(integer) 10
redis> PERSIST mykey
(integer) 1
redis> TTL mykey
(integer) -1
```

移除键的过期时间

### PEXPIRE

```{.wrap}
PEXPIRE key milliseconds
```

#### 示例

```shell script
redis> SET mykey "Hello"
"OK"
redis> PEXPIRE mykey 1500
(integer) 1
redis> TTL mykey
(integer) 1
redis> PTTL mykey
(integer) 1499
```

以毫秒为单位设置键的生存时间

### PEXPIREAT

```{.wrap}
PEXPIREAT key milliseconds-timestamp
```

#### 示例

```shell script
redis> SET mykey "Hello"
"OK"
redis> PEXPIREAT mykey 1555555555005
(integer) 1
redis> TTL mykey
(integer) -2
redis> PTTL mykey
(integer) -2
```

以毫秒为单位的 UNIX 时间戳设置键的过期时间

### PTTL

```{.wrap}
PTTL key
```

#### 示例

```shell script
redis> SET mykey "Hello"
"OK"
redis> EXPIRE mykey 1
(integer) 1
redis> PTTL mykey
(integer) 1000
```

以毫秒为单位获取键的生存时间

### RENAME

```{.wrap}
RENAME key newkey
```

#### 示例

```shell script
redis> SET mykey "Hello"
"OK"
redis> RENAME mykey myotherkey
"OK"
redis> GET myotherkey
"Hello"
```

重命名一个键

### RENAMENX

```{.wrap}
RENAMENX key newkey
```

#### 示例

```shell script
redis> SET mykey "Hello"
"OK"
redis> SET myotherkey "World"
"OK"
redis> RENAMENX mykey myotherkey
(integer) 0
redis> GET myotherkey
"World"
```

重命名一个键，仅当新键不存在时

### TOUCH

```{.wrap}
TOUCH key [key ...]
```

#### 示例

```shell script
redis> SET key1 "Hello"
"OK"
redis> SET key2 "World"
"OK"
redis> TOUCH key1 key2
(integer) 2
```

更改一个或多个键的最后访问时间。返回指定的现有键的数量。

### TTL

```{.wrap}
TTL key
```

#### 示例

```shell script
redis> SET mykey "Hello"
"OK"
redis> EXPIRE mykey 10
(integer) 1
redis> TTL mykey
(integer) 10
```

获取键的生存时间

### TYPE

```{.wrap}
TYPE key
```

#### 示例

```shell script
redis> SET key1 "value"
"OK"
redis> LPUSH key2 "value"
(integer) 1
redis> SADD key3 "value"
(integer) 1
redis> TYPE key1
"string"
redis> TYPE key2
"list"
redis> TYPE key3
"set"
```

确定存储在键处的类型

### UNLINK

```{.wrap}
UNLINK key [key ...]
```

#### 示例

```shell script
redis> SET key1 "Hello"
"OK"
redis> SET key2 "World"
"OK"
redis> UNLINK key1 key2 key3
(integer) 2
```

在另一个线程中异步删除一个键。否则它与 DEL 一样，但是非阻塞的。

## Redis 连接命令{.cols-3}

### Misc

| -                                                             | -                                                                          |
| ------------------------------------------------------------- | -------------------------------------------------------------------------- |
| [AUTH ](https://redis.io/commands/auth)                       | 对服务器进行身份验证                                                               |
| [CLIENT CACHING ](https://redis.io/commands/client-caching)   | 指示服务器在下一个请求中是否跟踪键                                                       |
| [CLIENT KILL ](https://redis.io/commands/client-kill)         | 终止客户端的连接                                                                 |
| [CLIENT LIST ](https://redis.io/commands/client-list)         | 获取客户端连接列表                                                               |
| [CLIENT GETNAME](https://redis.io/commands/client-getname)    | 获取当前连接名称                                                                 |
| [CLIENT GETREDIR](https://redis.io/commands/client-getredir)  | 获取跟踪通知重定向客户端 ID（如果有）                                                    |
| [CLIENT PAUSE ](https://redis.io/commands/client-pause)       | 在一段时间内停止处理来自客户端的命令                                                       |
| [CLIENT REPLY ](https://redis.io/commands/client-reply)       | 指示服务器是否回复命令                                                               |
| [CLIENT SETNAME ](https://redis.io/commands/client-setname)   | 设置当前连接名称                                                                 |
| [CLIENT TRACKING ](https://redis.io/commands/client-tracking) | 启用或禁用服务器辅助的客户端缓存支持                                                       |
| [CLIENT UNBLOCK ](https://redis.io/commands/client-unblock)   | 从不同连接解除在阻塞命令中被阻塞的客户端                                                     |
| [HELLO ](https://redis.io/commands/hello)                     | 切换 Redis 协议                                                              |
| [QUIT](https://redis.io/commands/quit)                        | 关闭连接                                                                   |
| [RESET](https://redis.io/commands/reset)                      | 重置连接                                                                   |
| [SELECT ](https://redis.io/commands/select)                   | 更改当前连接的所选数据库                                                               |

### CLIENT ID

```{.wrap}
CLIENT ID
```

#### 示例

```shell script
redis> CLIENT ID
ERR Unknown or disabled command 'CLIENT'
```

返回当前连接的客户端 ID

### CLIENT INFO

```{.wrap}
CLIENT INFO
```

#### 示例

```shell script
redis> CLIENT INFO
"id=55542 addr=127.0.0.1:58710 laddr=127.0.0.1:6379 fd=8 name= age=114920 idle=0 flags=N db=0 sub=0 psub=0 multi=-1 qbuf=26 qbuf-free=40928 argv-mem=10 obl=0 oll=0 omem=0 tot-mem=61466 events=r cmd=client user=default redir=-1\n"
```

返回有关当前客户端连接的信息。

### ECHO

```{.wrap}
ECHO message
```

#### 示例

```shell script
redis> ECHO "Hello World!"
"Hello World!"
```

回显给定的字符串

### PING

```{.wrap}
PING [message]
```

#### 示例

```shell script
redis> PING
"PONG"
redis> PING "hello world"
"hello world"
```

Ping 服务器

## Redis 流命令{.cols-2}

### Misc

| -                                                   | -                                                                                                                                                                                  |
| --------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [XINFO ](https://redis.io/commands/xinfo)           | 获取有关流和消费者组的信息                                                                                                                                                           |
| [XDEL ](https://redis.io/commands/xdel)             | 从流中删除指定的条目。返回实际删除的项目数，如果某些 ID 不存在，则可能与传递的 ID 数不同。                                                                                                   |
| [XREAD ](https://redis.io/commands/xread)           | 在多个流中返回从未见过的元素，其 ID 大于调用者为每个流报告的 ID。可以阻塞。                                                                                                                |
| [XGROUP ](https://redis.io/commands/xgroup)         | 创建、销毁和管理消费者组。                                                                                                                                                           |
| [XREADGROUP ](https://redis.io/commands/xreadgroup) | 使用消费者组从流中返回新条目，或访问给定消费者的待处理条目历史记录。可以阻塞。                                                                                                             |
| [XCLAIM ](https://redis.io/commands/xclaim)         | 更改（或获取）消费者组中消息的所有权，就像消息已传递给指定的消费者一样。                                                                                                                   |
| [XPENDING ](https://redis.io/commands/xpending)     | 从流消费者组待处理条目列表中返回信息和条目，这些条目是已获取但从未确认的消息。                                                                                                             |

### XADD

```{.wrap}
XADD key [MAXLEN [=|~] length] [NOMKSTREAM] *|ID field value [field value ...]
```

#### 示例

```shell script
redis> XADD mystream * name Sara surname OConnor
"1609040574632-0"
redis> XADD mystream * field1 value1 field2 value2 field3 value3
"1609040574632-1"
redis> XLEN mystream
(integer) 2
redis> XRANGE mystream - +
1) 1) "1609040574632-0"
   2) 1) "name"
      2) "Sara"
      3) "surname"
      4) "OConnor"
2) 1) "1609040574632-1"
   2) 1) "field1"
      2) "value1"
      3) "field2"
      4) "value2"
      5) "field3"
      6) "value3"
```

向流中追加一个新条目

### XTRIM

```{.wrap}
XTRIM key MAXLEN [=|~] length
```

#### 示例

```shell script
redis> XADD mystream * field1 A field2 B field3 C field4 D
"1609040575750-0"
redis> XTRIM mystream MAXLEN 2
(integer) 0
redis> XRANGE mystream - +
1) 1) "1609040575750-0"
   2) 1) "field1"
      2) "A"
      3) "field2"
      4) "B"
      5) "field3"
      6) "C"
      7) "field4"
      8) "D"
```

将流修剪到（如果传递了“~”，则近似）一定大小

### XRANGE

```{.wrap}
XRANGE key start end [COUNT count]
```

#### 示例

```shell script
redis> XADD writers * name Virginia surname Woolf
"1609040578002-0"
redis> XADD writers * name Jane surname Austen
"1609040578002-1"
redis> XADD writers * name Toni surname Morrison
"1609040578003-0"
redis> XADD writers * name Agatha surname Christie
"1609040578003-1"
redis> XADD writers * name Ngozi surname Adichie
"1609040578003-2"
redis> XLEN writers
(integer) 5
redis> XRANGE writers - + COUNT 2
1) 1) "1609040578002-0"
   2) 1) "name"
      2) "Virginia"
      3) "surname"
      4) "Woolf"
2) 1) "1609040578002-1"
   2) 1) "name"
      2) "Jane"
      3) "surname"
      4) "Austen"
```

返回流中元素的范围，其 ID 与指定的 ID 间隔匹配

### XREVRANGE

```{.wrap}
XREVRANGE key end start [COUNT count]
```

#### 示例

```shell script
redis> XADD writers * name Virginia surname Woolf
"1609040579130-0"
redis> XADD writers * name Jane surname Austen
"1609040579130-1"
redis> XADD writers * name Toni surname Morrison
"1609040579130-2"
redis> XADD writers * name Agatha surname Christie
"1609040579131-0"
redis> XADD writers * name Ngozi surname Adichie
"1609040579131-1"
redis> XLEN writers
(integer) 5
redis> XREVRANGE writers + - COUNT 1
1) 1) "1609040579131-1"
   2) 1) "name"
      2) "Ngozi"
      3) "surname"
      4) "Adichie"
```

返回流中元素的范围，其 ID 与指定的 ID 间隔匹配，与 XRANGE 相比顺序相反（从较大到较小的 ID）

### XLEN

```{.wrap}
XLEN key
```

#### 示例

```shell script
redis> XADD mystream * item 1
"1609040580250-0"
redis> XADD mystream * item 2
"1609040580250-1"
redis> XADD mystream * item 3
"1609040580251-0"
redis> XLEN mystream
(integer) 3
```

返回流中的条目数

### XACK

```{.wrap}
XACK key group ID [ID ...]
```

#### 示例

```shell script
redis> XACK mystream mygroup 1526569495631-0
ERR Unknown or disabled command 'XACK'
```

将待处理消息标记为已正确处理，有效地将其从消费者组的待处理条目列表中删除。命令的返回值是成功确认的消息数，即我们实际能够在 PEL 中解析的 ID 数。

## 其他 {.cols-2}

### 集群

| -                                                                                         | -                                                                |
| ----------------------------------------------------------------------------------------- | ---------------------------------------------------------------- |
| [CLUSTER ADDSLOTS ](https://redis.io/commands/cluster-addslots)                           | 将新的哈希槽分配给接收节点                                                 |
| [CLUSTER BUMPEPOCH](https://redis.io/commands/cluster-bumpepoch)                          | 推进集群配置纪元                                                   |
| [CLUSTER COUNT-FAILURE-REPORTS ](https://redis.io/commands/cluster-count-failure-reports) | 返回给定节点的活动故障报告数                                             |
| [CLUSTER COUNTKEYSINSLOT ](https://redis.io/commands/cluster-countkeysinslot)             | 返回指定哈希槽中的本地键数                                               |
| [CLUSTER DELSLOTS ](https://redis.io/commands/cluster-delslots)                           | 在接收节点中将哈希槽设置为未绑定                                           |
| [CLUSTER FAILOVER ](https://redis.io/commands/cluster-failover)                           | 强制副本执行其主节点的手动故障转移。                                       |
| [CLUSTER FLUSHSLOTS](https://redis.io/commands/cluster-flushslots)                        | 删除节点自己的槽信息                                                 |
| [CLUSTER FORGET ](https://redis.io/commands/cluster-forget)                               | 从节点表中删除一个节点                                                 |
| [CLUSTER GETKEYSINSLOT ](https://redis.io/commands/cluster-getkeysinslot)                 | 返回指定哈希槽中的本地键名                                               |
| [CLUSTER INFO](https://redis.io/commands/cluster-info)                                    | 提供有关 Redis 集群节点状态的信息                                        |
| [CLUSTER KEYSLOT ](https://redis.io/commands/cluster-keyslot)                             | 返回指定键的哈希槽                                                   |
| [CLUSTER MEET ](https://redis.io/commands/cluster-meet)                                   | 强制节点集群与另一个节点握手                                             |
| [CLUSTER MYID](https://redis.io/commands/cluster-myid)                                    | 返回节点 ID                                                        |
| [CLUSTER NODES](https://redis.io/commands/cluster-nodes)                                  | 获取节点的集群配置                                                   |
| [CLUSTER REPLICATE ](https://redis.io/commands/cluster-replicate)                         | 将节点重新配置为指定主节点的副本                                           |
| [CLUSTER RESET ](https://redis.io/commands/cluster-reset)                                 | 重置 Redis 集群节点                                                |
| [CLUSTER SAVECONFIG](https://redis.io/commands/cluster-saveconfig)                        | 强制节点将集群状态保存到磁盘                                             |
| [CLUSTER SET-CONFIG-EPOCH ](https://redis.io/commands/cluster-set-config-epoch)           | 在新节点中设置配置纪元                                                 |
| [CLUSTER SETSLOT ](https://redis.io/commands/cluster-setslot)                             | 将哈希槽绑定到特定节点                                                 |
| [CLUSTER SLAVES ](https://redis.io/commands/cluster-slaves)                               | 列出指定主节点的副本节点                                               |
| [CLUSTER REPLICAS ](https://redis.io/commands/cluster-replicas)                           | 列出指定主节点的副本节点                                               |
| [CLUSTER SLOTS](https://redis.io/commands/cluster-slots)                                  | 获取集群槽到节点映射的数组                                               |
| [READONLY](https://redis.io/commands/readonly)                                            | 为到集群副本节点的连接启用读取查询                                         |
| [READWRITE](https://redis.io/commands/readwrite)                                          | 为到集群副本节点的连接禁用读取查询                                         |

### 事务

| -                                            | -                                                                   |
| -------------------------------------------- | ------------------------------------------------------------------- |
| [DISCARD](https://redis.io/commands/discard) | 放弃 MULTI 之后发出的所有命令                                           |
| [EXEC](https://redis.io/commands/exec)       | 执行 MULTI 之后发出的所有命令                                           |
| [MULTI](https://redis.io/commands/multi)     | 标记事务块的开始                                                      |
| [UNWATCH](https://redis.io/commands/unwatch) | 忘记所有被监视的键                                                      |
| [WATCH ](https://redis.io/commands/watch)    | 监视给定的键以确定 MULTI/EXEC 块的执行                                  |

### 脚本

| -                                                         | -                                                    |
| --------------------------------------------------------- | ---------------------------------------------------- |
| [EVAL ](https://redis.io/commands/eval)                   | 在服务器端执行 Lua 脚本                                  |
| [EVALSHA ](https://redis.io/commands/evalsha)             | 在服务器端执行 Lua 脚本                                  |
| [SCRIPT DEBUG ](https://redis.io/commands/script-debug)   | 设置已执行脚本的调试模式。                                   |
| [SCRIPT EXISTS ](https://redis.io/commands/script-exists) | 检查脚本缓存中是否存在脚本。                                 |
| [SCRIPT FLUSH](https://redis.io/commands/script-flush)    | 从脚本缓存中删除所有脚本。                                   |
| [SCRIPT KILL](https://redis.io/commands/script-kill)      | 终止当前正在执行的脚本。                                   |
| [SCRIPT LOAD ](https://redis.io/commands/script-load)     | 将指定的 Lua 脚本加载到脚本缓存中。                            |

### 发布/订阅

| -                                                       | -                                                                          |
| ------------------------------------------------------- | -------------------------------------------------------------------------- |
| [PSUBSCRIBE ](https://redis.io/commands/psubscribe)     | 侦听发布到与给定模式匹配的频道的消息                                             |
| [PUBSUB ](https://redis.io/commands/pubsub)             | 检查发布/订阅子系统的状态                                                      |
| [PUBLISH ](https://redis.io/commands/publish)           | 向频道发布消息                                                               |
| [PUNSUBSCRIBE ](https://redis.io/commands/punsubscribe) | 停止侦听发布到与给定模式匹配的频道的消息                                         |
| [SUBSCRIBE ](https://redis.io/commands/subscribe)       | 侦听发布到给定频道的消息                                                       |
| [UNSUBSCRIBE ](https://redis.io/commands/unsubscribe)   | 停止侦听发布到给定频道的消息                                                     |

