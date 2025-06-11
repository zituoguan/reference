---
title: MySQL
date: 2020-12-16 18:28:43
background: bg-[#2a6387]
tags:
  - RDBMS
  - DB
categories:
  - 数据库
intro: SQL速查表为您提供了最常用的SQL语句以供参考。
plugins:
  - tooltip
  - copyCode
---

## 入门 {.cols-2}

### 连接 MySQL

```
mysql -u <user> -p

mysql [db_name]

mysql -h <host> -P <port> -u <user> -p [db_name]

mysql -h <host> -u <user> -p [db_name]
```

### 常用命令 {.row-span-2}

#### 数据库

| -                        | -        |
| ------------------------ | -------- |
| `CREATE DATABASE` db `;` | 创建数据库 |
| `SHOW DATABASES;`        | 列出数据库 |
| `USE` db`;`              | 切换数据库 |
| `CONNECT` db `;`         | 切换数据库 |
| `DROP DATABASE` db`;`    | 删除数据库 |

#### 表

| -                        | -              |
| ------------------------ | -------------- |
| `SHOW TABLES;`           | 列出当前数据库的表 |
| `SHOW FIELDS FROM` t`;`  | 列出表的字段     |
| `DESC` t`;`              | 显示表结构       |
| `SHOW CREATE TABLE `t`;` | 显示创建表的SQL  |
| `TRUNCATE TABLE `t`;`    | 删除表中的所有数据 |
| `DROP TABLE `t`;`        | 删除表         |

#### 进程

| -                   | -      |
| ------------------- | ------ |
| `show processlist;` | 列出进程 |
| `kill` pid`;`       | 杀死进程 |

#### 其他

| -              | -          |
| -------------- | ---------- |
| `exit` 或 `\q` | 退出MySQL会话 |

### 备份

创建备份

```sql
mysqldump -u user -p db_name > db.sql
```

导出不带模式的数据库

```{.wrap}
mysqldump -u user -p db_name --no-data=true --add-drop-table=false > db.sql
```

恢复备份

```
mysql -u user -p db_name < db.sql
```

## MySQL 示例

### 管理表

创建一个包含三列的新表

```sql
CREATE TABLE t (
     id    INT,
     name  VARCHAR DEFAULT NOT NULL,
     price INT DEFAULT 0
     PRIMARY KEY(id)
);
```

从数据库中删除表

```sql
DROP TABLE t ;
```

向表中添加新列

```sql
ALTER TABLE t ADD column;
```

从表中删除列 c

```sql
ALTER TABLE t DROP COLUMN c ;
```

添加约束

```sql
ALTER TABLE t ADD constraint;
```

删除约束

```sql
ALTER TABLE t DROP constraint;
```

将表 t1 重命名为 t2

```sql
ALTER TABLE t1 RENAME TO t2;
```

将列 c1 重命名为 c2

```sql
ALTER TABLE t1 RENAME c1 TO c2 ;
```

删除表中的所有数据

```sql
TRUNCATE TABLE t;
```

### 从表中查询数据

查询表中 c1, c2 列的数据

```sql
SELECT c1, c2 FROM t
```

查询表中的所有行和列

```sql
SELECT * FROM t
```

查询数据并使用条件过滤行

```sql
SELECT c1, c2 FROM t
WHERE condition
```

查询表中的不同行

```sql
SELECT DISTINCT c1 FROM t
WHERE condition
```

按升序或降序对结果集进行排序

```sql
SELECT c1, c2 FROM t
ORDER BY c1 ASC [DESC]
```

跳过 offset 行并返回接下来的 n 行

```sql
SELECT c1, c2 FROM t
ORDER BY c1
LIMIT n OFFSET offset
```

使用聚合函数对行进行分组

```sql
SELECT c1, aggregate(c2)
FROM t
GROUP BY c1
```

使用 HAVING 子句过滤组

```sql
SELECT c1, aggregate(c2)
FROM t
GROUP BY c1
HAVING condition
```

### 从多个表查询 {.row-span-2}

内连接 t1 和 t2

```sql
SELECT c1, c2
FROM t1
INNER JOIN t2 ON condition
```

左连接 t1 和 t1

```sql
SELECT c1, c2
FROM t1
LEFT JOIN t2 ON condition
```

右连接 t1 和 t2

```sql
SELECT c1, c2
FROM t1
RIGHT JOIN t2 ON condition
```

执行全外连接

```sql
SELECT c1, c2
FROM t1
FULL OUTER JOIN t2 ON condition
```

生成表中行的笛卡尔积

```sql
SELECT c1, c2
FROM t1
CROSS JOIN t2
```

执行交叉连接的另一种方法

```sql
SELECT c1, c2
FROM t1, t2
```

使用 INNER JOIN 子句将 t1 连接到自身

```sql
SELECT c1, c2
FROM t1 A
INNER JOIN t1 B ON condition
```

使用 SQL 运算符组合来自两个查询的行

```sql
SELECT c1, c2 FROM t1
UNION [ALL]
SELECT c1, c2 FROM t2
```

返回两个查询的交集

```sql
SELECT c1, c2 FROM t1
INTERSECT
SELECT c1, c2 FROM t2
```

从另一个结果集中减去一个结果集

```sql
SELECT c1, c2 FROM t1
MINUS
SELECT c1, c2 FROM t2
```

使用模式匹配查询行 %, \_

```sql
SELECT c1, c2 FROM t1
WHERE c1 [NOT] LIKE pattern
```

查询列表中的行

```sql
SELECT c1, c2 FROM t
WHERE c1 [NOT] IN value_list
```

查询两个值之间的行

```sql
SELECT c1, c2 FROM t
WHERE  c1 BETWEEN low AND high
```

检查表中的值是否为 NULL

```sql
SELECT c1, c2 FROM t
WHERE  c1 IS [NOT] NULL
```

### 使用 SQL 约束

将 c1 和 c2 设置为主键

```sql
CREATE TABLE t(
    c1 INT, c2 INT, c3 VARCHAR,
    PRIMARY KEY (c1,c2)
);
```

将 c2 列设置为外键

```sql
CREATE TABLE t1(
    c1 INT PRIMARY KEY,
    c2 INT,
    FOREIGN KEY (c2) REFERENCES t2(c2)
);
```

使 c1 和 c2 中的值唯一

```sql
CREATE TABLE t(
    c1 INT, c1 INT,
    UNIQUE(c2,c3)
);
```

确保 c1 > 0 且 c1 中的值 >= c2

```sql
CREATE TABLE t(
  c1 INT, c2 INT,
  CHECK(c1> 0 AND c1 >= c2)
);
```

将 c2 列中的值设置为 NOT NULL

```sql
CREATE TABLE t(
     c1 INT PRIMARY KEY,
     c2 VARCHAR NOT NULL
);
```

### 修改数据

向表中插入一行

```sql
INSERT INTO t(column_list)
VALUES(value_list);
```

向表中插入多行

```sql
INSERT INTO t(column_list)
VALUES (value_list),
       (value_list), …;
```

将 t2 中的行插入到 t1 中

```sql
INSERT INTO t1(column_list)
SELECT column_list
FROM t2;
```

更新所有行中 c1 列的新值

```sql
UPDATE t
SET c1 = new_value;
```

更新与条件匹配的 c1, c2 列中的值

```sql
UPDATE t
SET c1 = new_value,
        c2 = new_value
WHERE condition;
```

删除表中的所有数据

```sql
DELETE FROM t;
```

删除表中的行子集

```sql
DELETE FROM t
WHERE condition;
```

### 管理视图

创建一个由 c1 和 c2 组成的新视图

```sql
CREATE VIEW v(c1,c2)
AS
SELECT c1, c2
FROM t;
```

创建一个带检查选项的新视图

```sql
CREATE VIEW v(c1,c2)
AS
SELECT c1, c2
FROM t;
WITH [CASCADED | LOCAL] CHECK OPTION;
```

创建递归视图

```sql
CREATE RECURSIVE VIEW v
AS
select-statement -- anchor part
UNION [ALL]
select-statement; -- recursive part
```

创建临时视图

```sql
CREATE TEMPORARY VIEW v
AS
SELECT c1, c2
FROM t;
```

删除视图

```sql
DROP VIEW view_name;
```

### 管理触发器

创建或修改触发器

```sql
CREATE OR MODIFY TRIGGER trigger_name
WHEN EVENT
ON table_name TRIGGER_TYPE
EXECUTE stored_procedure;
```

#### WHEN

| -        | -                |
| -------- | ---------------- |
| `BEFORE` | 事件发生前调用     |
| `AFTER`  | 事件发生后调用     |

#### EVENT

| -        | -                   |
| -------- | ------------------- |
| `INSERT` | 为 INSERT 调用     |
| `UPDATE` | 为 UPDATE 调用     |
| `DELETE` | 为 DELETE 调用     |

#### TRIGGER_TYPE

| -                    | -   |
| -------------------- | --- |
| `FOR EACH ROW`       |     |
| `FOR EACH STATEMENT` |     |

### 管理索引

在 t 表的 c1 和 c2 上创建索引

```sql
CREATE INDEX idx_name
ON t(c1,c2);
```

在 t 表的 c3, c4 上创建唯一索引

```sql
CREATE UNIQUE INDEX idx_name
ON t(c3,c4)
```

删除索引

```sql
DROP INDEX idx_name ON t;
```

## MySQL 数据类型

### 字符串

| -            | -                           |
| ------------ | --------------------------- |
| `CHAR`       | 字符串 (0 - 255)            |
| `VARCHAR`    | 字符串 (0 - 255)            |
| `TINYTEXT`   | 字符串 (0 - 255)            |
| `TEXT`       | 字符串 (0 - 65535)          |
| `BLOB`       | 字符串 (0 - 65535)          |
| `MEDIUMTEXT` | 字符串 (0 - 16777215)       |
| `MEDIUMBLOB` | 字符串 (0 - 16777215)       |
| `LONGTEXT`   | 字符串 (0 - 429496­7295)    |
| `LONGBLOB`   | 字符串 (0 - 429496­7295)    |
| `ENUM`       | 预设选项之一                 |
| `SET`        | 预设选项的选择               |

### 日期和时间

| 数据类型    | 格式                |
| ----------- | ------------------- |
| `DATE     ` | yyyy-MM-dd          |
| `TIME     ` | hh:mm:ss            |
| `DATETIME ` | yyyy-MM-dd hh:mm:ss |
| `TIMESTAMP` | yyyy-MM-dd hh:mm:ss |
| `YEAR     ` | yyyy                |

### 数字

| -             | -                                                             |
| ------------- | ------------------------------------------------------------- |
| `TINYINT x`   | 整数 (-128 到 127)                                         |
| `SMALLINT x`  | 整数 (-32768 到 32767)                                     |
| `MEDIUMINT x` | 整数 (-8388608 到 8388607)                                 |
| `INT x`       | 整数 (-2147­483648 到 214748­3647)                         |
| `BIGINT x`    | 整数 (-9223­372­036­854­775808 到 922337­203­685­477­5807) |
| `FLOAT`       | 小数 (精确到 23 位)                                |
| `DOUBLE`      | 小数 (24 到 53 位)                                     |
| `DECIMAL`     | 作为字符串存储的 "­DOU­BLE­"                                  |

## MySQL 函数和运算符

### 字符串 {.row-span-2}

<!-- prettier-ignore -->
- [ASCII()](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_ascii){data-tooltip="返回最左边字符的数值"}
- [BIN()](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_bin){data-tooltip="返回包含数字二进制表示的字符串"}
- [BIT_LENGTH()](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_bit-length){data-tooltip="返回参数的位数长度"}
- [CHAR()](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_char){data-tooltip="返回传递的每个整数对应的字符"}
- [CHARACTER_LENGTH()](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_character-length){data-tooltip="CHAR_LENGTH() 的同义词"}
- [CHAR_LENGTH()](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_char-length){data-tooltip="返回参数中的字符数"}
- [CONCAT()](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_concat){data-tooltip="返回连接后的字符串"}
- [CONCAT_WS()](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_concat-ws){data-tooltip="返回带分隔符的连接字符串"}
- [ELT()](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_elt){data-tooltip="返回索引号处的字符串"}
- [EXPORT_SET()](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_export-set){data-tooltip="返回一个字符串，使得对于值位中设置的每个位，您都会得到一个 on 字符串，对于每个未设置的位，您都会得到一个 off 字符串"}
- [FIELD()](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_field){data-tooltip="后续参数中第一个参数的索引（位置）"}
- [FIND_IN_SET()](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_find-in-set){data-tooltip="第二个参数中第一个参数的索引（位置）"}
- [FORMAT()](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_format){data-tooltip="返回格式化为指定小数位数的数字"}
- [FROM_BASE64()](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_from-base64){data-tooltip="解码 base64 编码的字符串并返回结果"}
- [HEX()](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_hex){data-tooltip="十进制或字符串值的十六进制表示"}
- [INSERT()](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_insert){data-tooltip="在指定位置插入子字符串，最多指定字符数"}
- [INSTR()](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_instr){data-tooltip="返回子字符串第一次出现的索引"}
- [LCASE()](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_lcase){data-tooltip="LOWER() 的同义词"}
- [LEFT()](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_left){data-tooltip="返回指定的最左边字符数"}
- [LENGTH()](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_length){data-tooltip="返回字符串的字节长度"}
- [LIKE](https://dev.mysql.com/doc/refman/8.0/en/string-comparison-functions.html#operator_like){data-tooltip="简单模式匹配"}
- [LOAD_FILE()](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_load-file){data-tooltip="加载指定文件"}
- [LOCATE()](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_locate){data-tooltip="返回子字符串第一次出现的位置"}
- [LOWER()](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_lower){data-tooltip="返回小写参数"}
- [LPAD()](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_lpad){data-tooltip="返回字符串参数，左边用指定字符串填充"}
- [LTRIM()](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_ltrim){data-tooltip="删除前导空格"}
- [MAKE_SET()](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_make-set){data-tooltip="返回一组逗号分隔的字符串，这些字符串在位中设置了相应的位"}
- [MATCH](https://dev.mysql.com/doc/refman/8.0/en/fulltext-search.html#function_match){data-tooltip="执行全文搜索"}
- [MID()](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_mid){data-tooltip="返回从指定位置开始的子字符串"}
- [NOT LIKE](https://dev.mysql.com/doc/refman/8.0/en/string-comparison-functions.html#operator_not-like){data-tooltip="简单模式匹配的否定"}
- [NOT REGEXP](https://dev.mysql.com/doc/refman/8.0/en/regexp.html#operator_not-regexp){data-tooltip="REGEXP 的否定"}
- [OCT()](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_oct){data-tooltip="返回包含数字八进制表示的字符串"}
- [OCTET_LENGTH()](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_octet-length){data-tooltip="LENGTH() 的同义词"}
- [ORD()](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_ord){data-tooltip="返回参数最左边字符的字符代码"}
- [POSITION()](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_position){data-tooltip="LOCATE() 的同义词"}
- [QUOTE()](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_quote){data-tooltip="转义参数以在 SQL 语句中使用"}
- [REGEXP](https://dev.mysql.com/doc/refman/8.0/en/regexp.html#operator_regexp){data-tooltip="字符串是否匹配正则表达式"}
- [REGEXP_INSTR()](https://dev.mysql.com/doc/refman/8.0/en/regexp.html#function_regexp-instr){data-tooltip="匹配正则表达式的子字符串的起始索引"}
- [REGEXP_LIKE()](https://dev.mysql.com/doc/refman/8.0/en/regexp.html#function_regexp-like){data-tooltip="字符串是否匹配正则表达式"}
- [REGEXP_REPLACE()](https://dev.mysql.com/doc/refman/8.0/en/regexp.html#function_regexp-replace){data-tooltip="替换匹配正则表达式的子字符串"}
- [REGEXP_SUBSTR()](https://dev.mysql.com/doc/refman/8.0/en/regexp.html#function_regexp-substr){data-tooltip="返回匹配正则表达式的子字符串"}
- [REPEAT()](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_repeat){data-tooltip="将字符串重复指定次数"}
- [REPLACE()](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_replace){data-tooltip="替换指定字符串的出现次数"}
- [REVERSE()](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_reverse){data-tooltip="反转字符串中的字符"}
- [RIGHT()](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_right){data-tooltip="返回指定的最右边字符数"}
- [RLIKE](https://dev.mysql.com/doc/refman/8.0/en/regexp.html#operator_regexp){data-tooltip="字符串是否匹配正则表达式"}
- [RPAD()](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_rpad){data-tooltip="将字符串附加指定次数"}
- [RTRIM()](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_rtrim){data-tooltip="删除尾随空格"}
- [SOUNDEX()](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_soundex){data-tooltip="返回 soundex 字符串"}
- [SOUNDS LIKE](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#operator_sounds-like){data-tooltip="比较声音"}
- [SPACE()](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_space){data-tooltip="返回指定数量空格的字符串"}
- [STRCMP()](https://dev.mysql.com/doc/refman/8.0/en/string-comparison-functions.html#function_strcmp){data-tooltip="比较两个字符串"}
- [SUBSTR()](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_substr){data-tooltip="按指定方式返回子字符串"}
- [SUBSTRING()](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_substring){data-tooltip="按指定方式返回子字符串"}
- [SUBSTRING_INDEX()](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_substring-index){data-tooltip="在分隔符出现指定次数之前从字符串返回子字符串"}
- [TO_BASE64()](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_to-base64){data-tooltip="返回转换为 base-64 字符串的参数"}
- [TRIM()](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_trim){data-tooltip="删除前导和尾随空格"}
- [UCASE()](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_ucase){data-tooltip="UPPER() 的同义词"}
- [UNHEX()](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_unhex){data-tooltip="返回包含数字十六进制表示的字符串"}
- [UPPER()](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_upper){data-tooltip="转换为大写"}
- [WEIGHT_STRING()](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_weight-string){data-tooltip="返回字符串的权重字符串"}

{.cols-2 .marker-none}

### 日期和时间 {.row-span-2}

<!-- prettier-ignore -->
- [ADDDATE()](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_adddate){data-tooltip="向日期值添加时间值（间隔）"}
- [ADDTIME()](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_addtime){data-tooltip="添加时间"}
- [CONVERT_TZ()](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_convert-tz){data-tooltip="从一个时区转换为另一个时区"}
- [CURDATE()](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_curdate){data-tooltip="返回当前日期"}
- [CURRENT_DATE()](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_current-date){data-tooltip="CURDATE() 的同义词"}
- [CURRENT_TIME()](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_current-time){data-tooltip="CURTIME() 的同义词"}
- [CURRENT_TIMESTAMP()](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_current-timestamp){data-tooltip="NOW() 的同义词"}
- [CURTIME()](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_curtime){data-tooltip="返回当前时间"}
- [DATE()](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_date){data-tooltip="提取日期或日期时间表达式的日期部分"}
- [DATE_ADD()](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_date-add){data-tooltip="向日期值添加时间值（间隔）"}
- [DATE_FORMAT()](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_date-format){data-tooltip="按指定格式化日期"}
- [DATE_SUB()](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_date-sub){data-tooltip="从日期中减去时间值（间隔）"}
- [DATEDIFF()](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_datediff){data-tooltip="减去两个日期"}
- [DAY()](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_day){data-tooltip="DAYOFMONTH() 的同义词"}
- [DAYNAME()](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_dayname){data-tooltip="返回工作日的名称"}
- [DAYOFMONTH()](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_dayofmonth){data-tooltip="返回月份中的第几天 (0-31)"}
- [DAYOFWEEK()](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_dayofweek){data-tooltip="返回参数的工作日索引"}
- [DAYOFYEAR()](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_dayofyear){data-tooltip="返回一年中的第几天 (1-366)"}
- [EXTRACT()](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_extract){data-tooltip="提取日期的一部分"}
- [FROM_DAYS()](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_from-days){data-tooltip="将天数转换为日期"}
- [FROM_UNIXTIME()](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_from-unixtime){data-tooltip="将 Unix 时间戳格式化为日期"}
- [GET_FORMAT()](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_get-format){data-tooltip="返回日期格式字符串"}
- [HOUR()](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_hour){data-tooltip="提取小时"}
- [LAST_DAY](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_last-day){data-tooltip="返回参数月份的最后一天"}
- [LOCALTIME()](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_localtime){data-tooltip="NOW() 的同义词"}
- [LOCALTIMESTAMP()](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_localtimestamp){data-tooltip="NOW() 的同义词"}
- [MAKEDATE()](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_makedate){data-tooltip="从年份和一年中的第几天创建日期"}
- [MAKETIME()](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_maketime){data-tooltip="从小时、分钟、秒创建时间"}
- [MICROSECOND()](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_microsecond){data-tooltip="从参数返回微秒"}
- [MINUTE()](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_minute){data-tooltip="从参数返回分钟"}
- [MONTH()](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_month){data-tooltip="从传递的日期返回月份"}
- [MONTHNAME()](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_monthname){data-tooltip="返回月份的名称"}
- [NOW()](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_now){data-tooltip="返回当前日期和时间"}
- [PERIOD_ADD()](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_period-add){data-tooltip="向年月添加一个周期"}
- [PERIOD_DIFF()](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_period-diff){data-tooltip="返回周期之间的月数"}
- [QUARTER()](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_quarter){data-tooltip="从日期参数返回季度"}
- [SEC_TO_TIME()](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_sec-to-time){data-tooltip="将秒转换为 'hh:mm:ss' 格式"}
- [SECOND()](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_second){data-tooltip="返回秒 (0-59)"}
- [STR_TO_DATE()](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_str-to-date){data-tooltip="将字符串转换为日期"}
- [SUBDATE()](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_subdate){data-tooltip="当使用三个参数调用时，是 DATE_SUB() 的同义词"}
- [SUBTIME()](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_subtime){data-tooltip="减去时间"}
- [SYSDATE()](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_sysdate){data-tooltip="返回函数执行的时间"}
- [TIME()](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_time){data-tooltip="提取传递的表达式的时间部分"}
- [TIME_FORMAT()](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_time-format){data-tooltip="格式化为时间"}
- [TIME_TO_SEC()](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_time-to-sec){data-tooltip="返回转换为秒的参数"}
- [TIMEDIFF()](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_timediff){data-tooltip="减去时间"}
- [TIMESTAMP()](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_timestamp){data-tooltip="使用单个参数时，此函数返回日期或日期时间表达式；使用两个参数时，返回参数的总和"}
- [TIMESTAMPADD()](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_timestampadd){data-tooltip="向日期时间表达式添加一个间隔"}
- [TIMESTAMPDIFF()](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_timestampdiff){data-tooltip="从日期时间表达式中减去一个间隔"}
- [TO_DAYS()](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_to-days){data-tooltip="返回转换为天数的日期参数"}
- [TO_SECONDS()](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_to-seconds){data-tooltip="返回自公元 0 年以来转换为秒的日期或日期时间参数"}
- [UNIX_TIMESTAMP()](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_unix-timestamp){data-tooltip="返回 Unix 时间戳"}
- [UTC_DATE()](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_utc-date){data-tooltip="返回当前 UTC 日期"}
- [UTC_TIME()](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_utc-time){data-tooltip="返回当前 UTC 时间"}
- [UTC_TIMESTAMP()](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_utc-timestamp){data-tooltip="返回当前 UTC 日期和时间"}
- [WEEK()](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_week){data-tooltip="返回周数"}
- [WEEKDAY()](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_weekday){data-tooltip="返回工作日索引"}
- [WEEKOFYEAR()](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_weekofyear){data-tooltip="返回日期的日历周 (1-53)"}
- [YEAR()](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_year){data-tooltip="返回年份"}
- [YEARWEEK()](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_yearweek){data-tooltip="返回年份和周"}
- [GET_FORMAT()](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_get-format){data-tooltip="'%m.%d.%Y'"}

{.cols-2 .marker-none}

### 数字

<!-- prettier-ignore -->
- [%, MOD](https://dev.mysql.com/doc/refman/8.0/en/arithmetic-functions.html#operator_mod){data-tooltip="模运算符"}
- [*](https://dev.mysql.com/doc/refman/8.0/en/arithmetic-functions.html#operator_times){data-tooltip="乘法运算符"}
- [+ ](https://dev.mysql.com/doc/refman/8.0/en/arithmetic-functions.html#operator_plus){data-tooltip="加法运算符"}
- [-](https://dev.mysql.com/doc/refman/8.0/en/arithmetic-functions.html#operator_minus){data-tooltip="减法运算符"}
- [-](https://dev.mysql.com/doc/refman/8.0/en/arithmetic-functions.html#operator_unary-minus){data-tooltip="更改参数的符号"}
- [/](https://dev.mysql.com/doc/refman/8.0/en/arithmetic-functions.html#operator_divide){data-tooltip="除法运算符"}
- [ABS()](https://dev.mysql.com/doc/refman/8.0/en/mathematical-functions.html#function_abs){data-tooltip="返回绝对值"}
- [ACOS()](https://dev.mysql.com/doc/refman/8.0/en/mathematical-functions.html#function_acos){data-tooltip="返回反余弦"}
- [ASIN()](https://dev.mysql.com/doc/refman/8.0/en/mathematical-functions.html#function_asin){data-tooltip="返回反正弦"}
- [ATAN()](https://dev.mysql.com/doc/refman/8.0/en/mathematical-functions.html#function_atan){data-tooltip="返回反正切"}
- [ATAN2(), ATAN()](https://dev.mysql.com/doc/refman/8.0/en/mathematical-functions.html#function_atan2){data-tooltip="返回两个参数的反正切"}
- [CEIL()](https://dev.mysql.com/doc/refman/8.0/en/mathematical-functions.html#function_ceil){data-tooltip="返回不小于参数的最小整数值"}
- [CEILING()](https://dev.mysql.com/doc/refman/8.0/en/mathematical-functions.html#function_ceiling){data-tooltip="返回不小于参数的最小整数值"}
- [CONV()](https://dev.mysql.com/doc/refman/8.0/en/mathematical-functions.html#function_conv){data-tooltip="在不同数字基数之间转换数字"}
- [COS()](https://dev.mysql.com/doc/refman/8.0/en/mathematical-functions.html#function_cos){data-tooltip="返回余弦"}
- [COT()](https://dev.mysql.com/doc/refman/8.0/en/mathematical-functions.html#function_cot){data-tooltip="返回余切"}
- [CRC32()](https://dev.mysql.com/doc/refman/8.0/en/mathematical-functions.html#function_crc32){data-tooltip="计算循环冗余校验值"}
- [DEGREES()](https://dev.mysql.com/doc/refman/8.0/en/mathematical-functions.html#function_degrees){data-tooltip="将弧度转换为度"}
- [DIV](https://dev.mysql.com/doc/refman/8.0/en/arithmetic-functions.html#operator_div){data-tooltip="整数除法"}
- [EXP()](https://dev.mysql.com/doc/refman/8.0/en/mathematical-functions.html#function_exp){data-tooltip="求幂"}
- [FLOOR()](https://dev.mysql.com/doc/refman/8.0/en/mathematical-functions.html#function_floor){data-tooltip="返回不大于参数的最大整数值"}
- [LN()](https://dev.mysql.com/doc/refman/8.0/en/mathematical-functions.html#function_ln){data-tooltip="返回参数的自然对数"}
- [LOG()](https://dev.mysql.com/doc/refman/8.0/en/mathematical-functions.html#function_log){data-tooltip="返回第一个参数的自然对数"}
- [LOG10()](https://dev.mysql.com/doc/refman/8.0/en/mathematical-functions.html#function_log10){data-tooltip="返回参数的以 10 为底的对数"}
- [LOG2()](https://dev.mysql.com/doc/refman/8.0/en/mathematical-functions.html#function_log2){data-tooltip="返回参数的以 2 为底的对数"}
- [MOD()](https://dev.mysql.com/doc/refman/8.0/en/mathematical-functions.html#function_mod){data-tooltip="返回余数"}
- [PI()](https://dev.mysql.com/doc/refman/8.0/en/mathematical-functions.html#function_pi){data-tooltip="返回 pi 的值"}
- [POW()](https://dev.mysql.com/doc/refman/8.0/en/mathematical-functions.html#function_pow){data-tooltip="返回参数的指定次幂"}
- [POWER()](https://dev.mysql.com/doc/refman/8.0/en/mathematical-functions.html#function_power){data-tooltip="返回参数的指定次幂"}
- [RADIANS()](https://dev.mysql.com/doc/refman/8.0/en/mathematical-functions.html#function_radians){data-tooltip="返回转换为弧度的参数"}
- [RAND()](https://dev.mysql.com/doc/refman/8.0/en/mathematical-functions.html#function_rand){data-tooltip="返回一个随机浮点值"}
- [ROUND()](https://dev.mysql.com/doc/refman/8.0/en/mathematical-functions.html#function_round){data-tooltip="四舍五入参数"}
- [SIGN()](https://dev.mysql.com/doc/refman/8.0/en/mathematical-functions.html#function_sign){data-tooltip="返回参数的符号"}
- [SIN()](https://dev.mysql.com/doc/refman/8.0/en/mathematical-functions.html#function_sin){data-tooltip="返回参数的正弦"}
- [SQRT()](https://dev.mysql.com/doc/refman/8.0/en/mathematical-functions.html#function_sqrt){data-tooltip="返回参数的平方根"}
- [TAN()](https://dev.mysql.com/doc/refman/8.0/en/mathematical-functions.html#function_tan){data-tooltip="返回参数的正切"}
- [TRUNCATE()](https://dev.mysql.com/doc/refman/8.0/en/mathematical-functions.html#function_truncate){data-tooltip="截断到指定的小数位数"}

{.cols-2 .marker-none}

### 聚合

<!-- prettier-ignore -->
- [AVG()](https://dev.mysql.com/doc/refman/8.0/en/aggregate-functions.html#function_avg){data-tooltip="返回参数的平均值"}
- [BIT_AND()](https://dev.mysql.com/doc/refman/8.0/en/aggregate-functions.html#function_bit-and){data-tooltip="返回按位与"}
- [BIT_OR()](https://dev.mysql.com/doc/refman/8.0/en/aggregate-functions.html#function_bit-or){data-tooltip="返回按位或"}
- [BIT_XOR()](https://dev.mysql.com/doc/refman/8.0/en/aggregate-functions.html#function_bit-xor){data-tooltip="返回按位异或"}
- [COUNT()](https://dev.mysql.com/doc/refman/8.0/en/aggregate-functions.html#function_count){data-tooltip="返回返回的行数计数"}
- [COUNT(DISTINCT)](https://dev.mysql.com/doc/refman/8.0/en/aggregate-functions.html#function_count-distinct){data-tooltip="返回不同值的计数"}
- [GROUP_CONCAT()](https://dev.mysql.com/doc/refman/8.0/en/aggregate-functions.html#function_group-concat){data-tooltip="返回连接的字符串"}
- [JSON_ARRAYAGG()](https://dev.mysql.com/doc/refman/8.0/en/aggregate-functions.html#function_json-arrayagg){data-tooltip="将结果集作为单个 JSON 数组返回"}
- [JSON_OBJECTAGG()](https://dev.mysql.com/doc/refman/8.0/en/aggregate-functions.html#function_json-objectagg){data-tooltip="将结果集作为单个 JSON 对象返回"}
- [MAX()](https://dev.mysql.com/doc/refman/8.0/en/aggregate-functions.html#function_max){data-tooltip="返回最大值"}
- [MIN()](https://dev.mysql.com/doc/refman/8.0/en/aggregate-functions.html#function_min){data-tooltip="返回最小值"}
- [STD()](https://dev.mysql.com/doc/refman/8.0/en/aggregate-functions.html#function_std){data-tooltip="返回总体标准差"}
- [STDDEV()](https://dev.mysql.com/doc/refman/8.0/en/aggregate-functions.html#function_stddev){data-tooltip="返回总体标准差"}
- [STDDEV_POP()](https://dev.mysql.com/doc/refman/8.0/en/aggregate-functions.html#function_stddev-pop){data-tooltip="返回总体标准差"}
- [STDDEV_SAMP()](https://dev.mysql.com/doc/refman/8.0/en/aggregate-functions.html#function_stddev-samp){data-tooltip="返回样本标准差"}
- [SUM()](https://dev.mysql.com/doc/refman/8.0/en/aggregate-functions.html#function_sum){data-tooltip="返回总和"}
- [VAR_POP()](https://dev.mysql.com/doc/refman/8.0/en/aggregate-functions.html#function_var-pop){data-tooltip="返回总体标准方差"}
- [VAR_SAMP()](https://dev.mysql.com/doc/refman/8.0/en/aggregate-functions.html#function_var-samp){data-tooltip="返回样本方差"}
- [VARIANCE()](https://dev.mysql.com/doc/refman/8.0/en/aggregate-functions.html#function_variance){data-tooltip="返回总体标准方差"}

{.cols-2 .marker-none}

### JSON {.row-span-4}

<!-- prettier-ignore -->
- [->](https://dev.mysql.com/doc/refman/8.0/en/json-search-functions.html#operator_json-column-path){data-tooltip="评估路径后从 JSON 列返回值；等效于 JSON_EXTRACT()。"}
- [->>](https://dev.mysql.com/doc/refman/8.0/en/json-search-functions.html#operator_json-inline-path){data-tooltip="评估路径并取消引用结果后从 JSON 列返回值；等效于 JSON_UNQUOTE(JSON_EXTRACT())。"}
- [JSON_ARRAY()](https://dev.mysql.com/doc/refman/8.0/en/json-creation-functions.html#function_json-array){data-tooltip="创建 JSON 数组"}
- [JSON_ARRAY_APPEND()](https://dev.mysql.com/doc/refman/8.0/en/json-modification-functions.html#function_json-array-append){data-tooltip="向 JSON 文档追加数据"}
- [JSON_ARRAY_INSERT()](https://dev.mysql.com/doc/refman/8.0/en/json-modification-functions.html#function_json-array-insert){data-tooltip="插入到 JSON 数组"}
- [JSON_CONTAINS()](https://dev.mysql.com/doc/refman/8.0/en/json-search-functions.html#function_json-contains){data-tooltip="JSON 文档是否在路径中包含特定对象"}
- [JSON_CONTAINS_PATH()](https://dev.mysql.com/doc/refman/8.0/en/json-search-functions.html#function_json-contains-path){data-tooltip="JSON 文档是否在路径中包含任何数据"}
- [JSON_DEPTH()](https://dev.mysql.com/doc/refman/8.0/en/json-attribute-functions.html#function_json-depth){data-tooltip="JSON 文档的最大深度"}
- [JSON_EXTRACT()](https://dev.mysql.com/doc/refman/8.0/en/json-search-functions.html#function_json-extract){data-tooltip="从 JSON 文档返回数据"}
- [JSON_INSERT()](https://dev.mysql.com/doc/refman/8.0/en/json-modification-functions.html#function_json-insert){data-tooltip="向 JSON 文档插入数据"}
- [JSON_KEYS()](https://dev.mysql.com/doc/refman/8.0/en/json-search-functions.html#function_json-keys){data-tooltip="JSON 文档中的键数组"}
- [JSON_LENGTH()](https://dev.mysql.com/doc/refman/8.0/en/json-attribute-functions.html#function_json-length){data-tooltip="JSON 文档中的元素数量"}
- [JSON_MERGE() (已弃用)](https://dev.mysql.com/doc/refman/8.0/en/json-modification-functions.html#function_json-merge){data-tooltip="合并 JSON 文档，保留重复键。JSON_MERGE_PRESERVE() 的已弃用同义词"}
- [JSON_MERGE_PATCH()](https://dev.mysql.com/doc/refman/8.0/en/json-modification-functions.html#function_json-merge-patch){data-tooltip="合并 JSON 文档，替换重复键的值"}
- [JSON_MERGE_PRESERVE()](https://dev.mysql.com/doc/refman/8.0/en/json-modification-functions.html#function_json-merge-preserve){data-tooltip="合并 JSON 文档，保留重复键"}
- [JSON_OBJECT()](https://dev.mysql.com/doc/refman/8.0/en/json-creation-functions.html#function_json-object){data-tooltip="创建 JSON 对象"}
- [JSON_OVERLAPS() (8.0.17 引入)](https://dev.mysql.com/doc/refman/8.0/en/json-search-functions.html#function_json-overlaps){data-tooltip="比较两个 JSON 文档，如果它们有任何共同的键值对或数组成员，则返回 TRUE (1)，否则返回 FALSE (0)"}
- [JSON_PRETTY()](https://dev.mysql.com/doc/refman/8.0/en/json-utility-functions.html#function_json-pretty){data-tooltip="以人类可读的格式打印 JSON 文档"}
- [JSON_QUOTE()](https://dev.mysql.com/doc/refman/8.0/en/json-creation-functions.html#function_json-quote){data-tooltip="引用 JSON 文档"}
- [JSON_REMOVE()](https://dev.mysql.com/doc/refman/8.0/en/json-modification-functions.html#function_json-remove){data-tooltip="从 JSON 文档中删除数据"}
- [JSON_REPLACE()](https://dev.mysql.com/doc/refman/8.0/en/json-modification-functions.html#function_json-replace){data-tooltip="替换 JSON 文档中的值"}
- [JSON_SCHEMA_VALID() (8.0.17 引入)](https://dev.mysql.com/doc/refman/8.0/en/json-validation-functions.html#function_json-schema-valid){data-tooltip="根据 JSON 模式验证 JSON 文档；如果文档根据模式验证通过，则返回 TRUE/1，否则返回 FALSE/0"}
- [JSON_SCHEMA_VALIDATION_REPORT() (8.0.17 引入)](https://dev.mysql.com/doc/refman/8.0/en/json-validation-functions.html#function_json-schema-validation-report){data-tooltip="根据 JSON 模式验证 JSON 文档；以 JSON 格式返回验证结果报告，包括成功或失败以及失败原因"}
- [JSON_SEARCH()](https://dev.mysql.com/doc/refman/8.0/en/json-search-functions.html#function_json-search){data-tooltip="JSON 文档中值的路径"}
- [JSON_SET()](https://dev.mysql.com/doc/refman/8.0/en/json-modification-functions.html#function_json-set){data-tooltip="向 JSON 文档插入数据"}
- [JSON_STORAGE_FREE()](https://dev.mysql.com/doc/refman/8.0/en/json-utility-functions.html#function_json-storage-free){data-tooltip="部分更新后 JSON 列值的二进制表示中释放的空间"}
- [JSON_STORAGE_SIZE()](https://dev.mysql.com/doc/refman/8.0/en/json-utility-functions.html#function_json-storage-size){data-tooltip="用于存储 JSON 文档二进制表示的空间"}
- [JSON_TABLE()](https://dev.mysql.com/doc/refman/8.0/en/json-table-functions.html#function_json-table){data-tooltip="将 JSON 表达式中的数据作为关系表返回"}
- [JSON_TYPE()](https://dev.mysql.com/doc/refman/8.0/en/json-attribute-functions.html#function_json-type){data-tooltip="JSON 值的类型"}
- [JSON_UNQUOTE()](https://dev.mysql.com/doc/refman/8.0/en/json-modification-functions.html#function_json-unquote){data-tooltip="取消引用 JSON 值"}
- [JSON_VALID()](https://dev.mysql.com/doc/refman/8.0/en/json-attribute-functions.html#function_json-valid){data-tooltip="JSON 值是否有效"}
- [JSON_VALUE() (8.0.21 引入)](https://dev.mysql.com/doc/refman/8.0/en/json-search-functions.html#function_json-value){data-tooltip="从提供的路径指向的 JSON 文档位置提取值；将此值作为 VARCHAR(512) 或指定类型返回"}
- [MEMBER OF() (8.0.17 引入)](https://dev.mysql.com/doc/refman/8.0/en/json-search-functions.html#operator_member-of){data-tooltip="如果第一个操作数匹配作为第二个操作数传递的 JSON 数组的任何元素，则返回 true (1)，否则返回 false (0)"}

{.cols-1 .marker-none}

### 类型转换

<!-- prettier-ignore -->
- [BINARY](https://dev.mysql.com/doc/refman/8.0/en/cast-functions.html#operator_binary){data-tooltip="将字符串转换为二进制字符串"}
- [CAST()](https://dev.mysql.com/doc/refman/8.0/en/cast-functions.html#function_cast){data-tooltip="将值转换为特定类型"}
- [CONVERT()](https://dev.mysql.com/doc/refman/8.0/en/cast-functions.html#function_convert){data-tooltip="将值转换为特定类型"}

{.cols-2 .marker-none}

### 流程控制

<!-- prettier-ignore -->
- [CASE](https://dev.mysql.com/doc/refman/8.0/en/flow-control-functions.html#operator_case){data-tooltip="Case 运算符"}
- [IF()](https://dev.mysql.com/doc/refman/8.0/en/flow-control-functions.html#function_if){data-tooltip="If/else 结构"}
- [IFNULL()](https://dev.mysql.com/doc/refman/8.0/en/flow-control-functions.html#function_ifnull){data-tooltip="Null if/else 结构"}
- [NULLIF()](https://dev.mysql.com/doc/refman/8.0/en/flow-control-functions.html#function_nullif){data-tooltip="如果 expr1 = expr2 则返回 NULL"}

{.cols-2 .marker-none}

### 信息

<!-- prettier-ignore -->
- [BENCHMARK()](https://dev.mysql.com/doc/refman/8.0/en/information-functions.html#function_benchmark){data-tooltip="重复执行表达式"}
- [CHARSET()](https://dev.mysql.com/doc/refman/8.0/en/information-functions.html#function_charset){data-tooltip="返回参数的字符集"}
- [COERCIBILITY()](https://dev.mysql.com/doc/refman/8.0/en/information-functions.html#function_coercibility){data-tooltip="返回字符串参数的排序规则强制性值"}
- [COLLATION()](https://dev.mysql.com/doc/refman/8.0/en/information-functions.html#function_collation){data-tooltip="返回字符串参数的排序规则"}
- [CONNECTION_ID()](https://dev.mysql.com/doc/refman/8.0/en/information-functions.html#function_connection-id){data-tooltip="返回连接的连接 ID（线程 ID）"}
- [CURRENT_ROLE()](https://dev.mysql.com/doc/refman/8.0/en/information-functions.html#function_current-role){data-tooltip="返回当前活动角色"}
- [CURRENT_USER()](https://dev.mysql.com/doc/refman/8.0/en/information-functions.html#function_current-user){data-tooltip="已验证的用户名和主机名"}
- [DATABASE()](https://dev.mysql.com/doc/refman/8.0/en/information-functions.html#function_database){data-tooltip="返回默认（当前）数据库名称"}
- [FOUND_ROWS()](https://dev.mysql.com/doc/refman/8.0/en/information-functions.html#function_found-rows){data-tooltip="对于带有 LIMIT 子句的 SELECT，如果没有 LIMIT 子句将返回的行数"}
- [ICU_VERSION()](https://dev.mysql.com/doc/refman/8.0/en/information-functions.html#function_icu-version){data-tooltip="ICU 库版本"}
- [LAST_INSERT_ID()](https://dev.mysql.com/doc/refman/8.0/en/information-functions.html#function_last-insert-id){data-tooltip="最后一次 INSERT 的 AUTOINCREMENT 列的值"}
- [ROLES_GRAPHML()](https://dev.mysql.com/doc/refman/8.0/en/information-functions.html#function_roles-graphml){data-tooltip="返回表示内存角色子图的 GraphML 文档"}
- [ROW_COUNT()](https://dev.mysql.com/doc/refman/8.0/en/information-functions.html#function_row-count){data-tooltip="更新的行数"}
- [SCHEMA()](https://dev.mysql.com/doc/refman/8.0/en/information-functions.html#function_schema){data-tooltip="DATABASE() 的同义词"}
- [SESSION_USER()](https://dev.mysql.com/doc/refman/8.0/en/information-functions.html#function_session-user){data-tooltip="USER() 的同义词"}
- [SYSTEM_USER()](https://dev.mysql.com/doc/refman/8.0/en/information-functions.html#function_system-user){data-tooltip="USER() 的同义词"}
- [USER()](https://dev.mysql.com/doc/refman/8.0/en/information-functions.html#function_user){data-tooltip="客户端提供的用户名和主机名"}
- [VERSION()](https://dev.mysql.com/doc/refman/8.0/en/information-functions.html#function_version){data-tooltip="返回指示 MySQL 服务器版本的字符串"}

{.cols-2 .marker-none}

### 加密和压缩

<!-- prettier-ignore -->
- [AES_DECRYPT()](https://dev.mysql.com/doc/refman/8.0/en/encryption-functions.html#function_aes-decrypt){data-tooltip="使用 AES 解密"}
- [AES_ENCRYPT()](https://dev.mysql.com/doc/refman/8.0/en/encryption-functions.html#function_aes-encrypt){data-tooltip="使用 AES 加密"}
- [COMPRESS()](https://dev.mysql.com/doc/refman/8.0/en/encryption-functions.html#function_compress){data-tooltip="以二进制字符串形式返回结果"}
- [MD5()](https://dev.mysql.com/doc/refman/8.0/en/encryption-functions.html#function_md5){data-tooltip="计算 MD5 校验和"}
- [RANDOM_BYTES()](https://dev.mysql.com/doc/refman/8.0/en/encryption-functions.html#function_random-bytes){data-tooltip="返回随机字节向量"}
- [SHA1(), SHA()](https://dev.mysql.com/doc/refman/8.0/en/encryption-functions.html#function_sha1){data-tooltip="计算 SHA-1 160 位校验和"}
- [SHA2()](https://dev.mysql.com/doc/refman/8.0/en/encryption-functions.html#function_sha2){data-tooltip="计算 SHA-2 校验和"}
- [STATEMENT_DIGEST()](https://dev.mysql.com/doc/refman/8.0/en/encryption-functions.html#function_statement-digest){data-tooltip="计算语句摘要哈希值"}
- [STATEMENT_DIGEST_TEXT()](https://dev.mysql.com/doc/refman/8.0/en/encryption-functions.html#function_statement-digest-text){data-tooltip="计算规范化语句摘要"}
- [UNCOMPRESS()](https://dev.mysql.com/doc/refman/8.0/en/encryption-functions.html#function_uncompress){data-tooltip="解压缩已压缩的字符串"}
- [UNCOMPRESSED_LENGTH()](https://dev.mysql.com/doc/refman/8.0/en/encryption-functions.html#function_uncompressed-length){data-tooltip="返回压缩前字符串的长度"}
- [VALIDATE_PASSWORD_STRENGTH()](https://dev.mysql.com/doc/refman/8.0/en/encryption-functions.html#function_validate-password-strength){data-tooltip="确定密码强度"}

{.cols-1 .marker-none}

### 锁定

<!-- prettier-ignore -->
- [GET_LOCK()](https://dev.mysql.com/doc/refman/8.0/en/locking-functions.html#function_get-lock){data-tooltip="获取命名锁"}
- [IS_FREE_LOCK()](https://dev.mysql.com/doc/refman/8.0/en/locking-functions.html#function_is-free-lock){data-tooltip="命名锁是否空闲"}
- [IS_USED_LOCK()](https://dev.mysql.com/doc/refman/8.0/en/locking-functions.html#function_is-used-lock){data-tooltip="命名锁是否正在使用；如果为 true，则返回连接标识符"}
- [RELEASE_ALL_LOCKS()](https://dev.mysql.com/doc/refman/8.0/en/locking-functions.html#function_release-all-locks){data-tooltip="释放所有当前命名锁"}
- [RELEASE_LOCK()](https://dev.mysql.com/doc/refman/8.0/en/locking-functions.html#function_release-lock){data-tooltip="释放命名锁"}

{.cols-1 .marker-none}

### 位运算

<!-- prettier-ignore -->
- [& ](https://dev.mysql.com/doc/refman/8.0/en/bit-functions.html#operator_bitwise-and){data-tooltip="按位与"}
- [>>](https://dev.mysql.com/doc/refman/8.0/en/bit-functions.html#operator_right-shift){data-tooltip="右移"}
- [<<](https://dev.mysql.com/doc/refman/8.0/en/bit-functions.html#operator_left-shift){data-tooltip="左移"}
- [^](https://dev.mysql.com/doc/refman/8.0/en/bit-functions.html#operator_bitwise-xor){data-tooltip="按位异或"}
- [BIT_COUNT()](https://dev.mysql.com/doc/refman/8.0/en/bit-functions.html#function_bit-count){data-tooltip="返回设置的位数"}
- [|](https://dev.mysql.com/doc/refman/8.0/en/bit-functions.html#operator_bitwise-or){data-tooltip="按位或"}
- [~](https://dev.mysql.com/doc/refman/8.0/en/bit-functions.html#operator_bitwise-invert){data-tooltip="按位取反"}

{.cols-2 .marker-none}

### 其他

<!-- prettier-ignore -->
- [ANY_VALUE()](https://dev.mysql.com/doc/refman/8.0/en/miscellaneous-functions.html#function_any-value){data-tooltip="抑制 ONLY_FULL_GROUP_BY 值拒绝"}
- [BIN_TO_UUID()](https://dev.mysql.com/doc/refman/8.0/en/miscellaneous-functions.html#function_bin-to-uuid){data-tooltip="将二进制 UUID 转换为字符串"}
- [DEFAULT()](https://dev.mysql.com/doc/refman/8.0/en/miscellaneous-functions.html#function_default){data-tooltip="返回表列的默认值"}
- [GROUPING()](https://dev.mysql.com/doc/refman/8.0/en/miscellaneous-functions.html#function_grouping){data-tooltip="区分超聚合 ROLLUP 行和常规行"}
- [INET_ATON()](https://dev.mysql.com/doc/refman/8.0/en/miscellaneous-functions.html#function_inet-aton){data-tooltip="返回 IP 地址的数值"}
- [INET_NTOA()](https://dev.mysql.com/doc/refman/8.0/en/miscellaneous-functions.html#function_inet-ntoa){data-tooltip="从数值返回 IP 地址"}
- [INET6_ATON()](https://dev.mysql.com/doc/refman/8.0/en/miscellaneous-functions.html#function_inet6-aton){data-tooltip="返回 IPv6 地址的数值"}
- [INET6_NTOA()](https://dev.mysql.com/doc/refman/8.0/en/miscellaneous-functions.html#function_inet6-ntoa){data-tooltip="从数值返回 IPv6 地址"}
- [IS_IPV4()](https://dev.mysql.com/doc/refman/8.0/en/miscellaneous-functions.html#function_is-ipv4){data-tooltip="参数是否为 IPv4 地址"}
- [IS_IPV4_COMPAT()](https://dev.mysql.com/doc/refman/8.0/en/miscellaneous-functions.html#function_is-ipv4-compat){data-tooltip="参数是否为 IPv4 兼容地址"}
- [IS_IPV4_MAPPED()](https://dev.mysql.com/doc/refman/8.0/en/miscellaneous-functions.html#function_is-ipv4-mapped){data-tooltip="参数是否为 IPv4 映射地址"}
- [IS_IPV6()](https://dev.mysql.com/doc/refman/8.0/en/miscellaneous-functions.html#function_is-ipv6){data-tooltip="参数是否为 IPv6 地址"}
- [IS_UUID()](https://dev.mysql.com/doc/refman/8.0/en/miscellaneous-functions.html#function_is-uuid){data-tooltip="参数是否为有效的 UUID"}
- [MASTER_POS_WAIT()](https://dev.mysql.com/doc/refman/8.0/en/miscellaneous-functions.html#function_master-pos-wait){data-tooltip="阻塞直到副本读取并应用所有更新到指定位置"}
- [NAME_CONST()](https://dev.mysql.com/doc/refman/8.0/en/miscellaneous-functions.html#function_name-const){data-tooltip="使列具有给定名称"}
- [SLEEP()](https://dev.mysql.com/doc/refman/8.0/en/miscellaneous-functions.html#function_sleep){data-tooltip="休眠指定的秒数"}
- [UUID()](https://dev.mysql.com/doc/refman/8.0/en/miscellaneous-functions.html#function_uuid){data-tooltip="返回通用唯一标识符 (UUID)"}
- [UUID_SHORT()](https://dev.mysql.com/doc/refman/8.0/en/miscellaneous-functions.html#function_uuid-short){data-tooltip="返回整数值的通用标识符"}
- [UUID_TO_BIN()](https://dev.mysql.com/doc/refman/8.0/en/miscellaneous-functions.html#function_uuid-to-bin){data-tooltip="将字符串 UUID 转换为二进制"}
- [VALUES()](https://dev.mysql.com/doc/refman/8.0/en/miscellaneous-functions.html#function_values){data-tooltip="定义 INSERT 期间要使用的值"}

{.cols-2 .marker-none}

## 另请参阅 {.cols-1}

- [MySQL 中的正则表达式](/regex#regex-in-mysql) _(r3f.cn)_
