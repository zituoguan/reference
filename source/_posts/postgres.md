---
title: PostgreSQL
background: bg-[#3d6488]
tags:
  - DB
  - RDBMS
categories:
  - 数据库
date: 2021-01-11 14:19:24
intro: |
  [PostgreSQL](https://www.postgresql.org/docs/current/) 速查表为您提供了常用的 PostgreSQL 命令和语句。
plugins:
  - copyCode
---

## 入门指南

### 快速入门

切换并连接

```shell script
$ sudo -u postgres psql
```

列出所有数据库

```shell script
postgres=# \l
```

连接到名为 postgres 的数据库

```shell script
postgres=# \c postgres
```

断开连接

```shell script
postgres=# \q
postgres=# \!
```

### psql 命令 {.col-span-2}

| 选项                | 示例                                         | 描述                       |
| ------------------- | -------------------------------------------- | :------------------------- |
| `[-d] <数据库>`     | psql -d mydb                                 | 连接到数据库               |
| `-U`                | psql -U john mydb                            | 以特定用户身份连接         |
| `-h` `-p`           | psql -h localhost -p 5432 mydb               | 连接到主机/端口            |
| `-U` `-h` `-p` `-d` | psql -U admin -h 192.168.1.5 -p 2506 -d mydb | 连接远程 PostgreSQL        |
| `-W`                | psql -W mydb                                 | 强制输入密码               |
| `-c`                | psql -c '\c postgres' -c '\dt'               | 执行 SQL 查询或命令        |
| `-H`                | psql -c "\l+" -H postgres > database.html    | 生成 HTML 报告             |
| `-l`                | psql -l                                      | 列出所有数据库             |
| `-f`                | psql mydb -f file.sql                        | 从文件执行命令             |
| `-V`                | psql -V                                      | 打印 psql 版本             |

{.show-header}

### 获取帮助

| -           | -                              |
| ----------- | :----------------------------- |
| `\h`        | SQL 命令语法帮助               |
| `\h` DELETE | DELETE SQL 语句语法            |
| `\?`        | PostgreSQL 命令列表            |

在 PostgreSQL 控制台中运行

## PostgreSQL 操作

### 侦察

显示版本

```
SHOW SERVER_VERSION;
```

显示系统状态

```sql {.wrap}
\conninfo
```

显示环境变量

```sql {.wrap}
SHOW ALL;
```

列出用户

```sql {.wrap}
SELECT rolname FROM pg_roles;
```

显示当前用户

```sql {.wrap}
SELECT current_user;
```

显示当前用户的权限

```
\du
```

显示当前数据库

```sql {.wrap}
SELECT current_database();
```

显示数据库中的所有表

```sql {.wrap}
\dt
```

列出函数

```sql {.wrap}
\df <模式名>
```

### 数据库

列出数据库

```sql {.wrap}
\l
```

连接到数据库

```sql {.wrap}
\c <数据库名>
```

显示当前数据库

```sql {.wrap}
SELECT current_database();
```

[创建数据库](http://www.postgresql.org/docs/current/static/sql-createdatabase.html)

```sql {.wrap}
CREATE DATABASE <数据库名> WITH OWNER <用户名>;
```

[删除数据库](http://www.postgresql.org/docs/current/static/sql-dropdatabase.html)

```sql {.wrap}
DROP DATABASE IF EXISTS <数据库名>;
```

[重命名数据库](http://www.postgresql.org/docs/current/static/sql-alterdatabase.html)

```sql {.wrap}
ALTER DATABASE <旧名称> RENAME TO <新名称>;
```

### 表

列出当前数据库中的表

```sql {.wrap}
\dt

SELECT table_schema,table_name FROM information_schema.tables ORDER BY table_schema,table_name;
```

全局列出表

```sql {.wrap}
\dt *.*.

SELECT * FROM pg_catalog.pg_tables
```

列出表结构

```sql {.wrap}
\d <表名>
\d+ <表名>

SELECT column_name, data_type, character_maximum_length
FROM INFORMATION_SCHEMA.COLUMNS
WHERE table_name = '<表名>';
```

[创建表](http://www.postgresql.org/docs/current/static/sql-createtable.html)

```sql {.wrap}
CREATE TABLE <表名>(
  <列名> <列类型>,
  <列名> <列类型>
);
```

创建带自增主键的表

```sql {.wrap}
CREATE TABLE <表名> (
  <列名> SERIAL PRIMARY KEY
);
```

[删除表](http://www.postgresql.org/docs/current/static/sql-droptable.html)

```sql {.wrap}
DROP TABLE IF EXISTS <表名> CASCADE;
```

### 权限

如果遇到权限错误，成为 postgres 用户

```shell
sudo su - postgres
psql
```

[授予](http://www.postgresql.org/docs/current/static/sql-grant.html)数据库所有权限

```sql {.wrap}
GRANT ALL PRIVILEGES ON DATABASE <数据库名> TO <用户名>;
```

授予数据库连接权限

```sql {.wrap}
GRANT CONNECT ON DATABASE <数据库名> TO <用户名>;
```

授予模式权限

```sql {.wrap}
GRANT USAGE ON SCHEMA public TO <用户名>;
```

授予函数权限

```sql {.wrap}
GRANT EXECUTE ON ALL FUNCTIONS IN SCHEMA public TO <用户名>;
```

授予对所有表的选择、更新、插入、删除权限

```sql {.wrap}
GRANT SELECT, UPDATE, INSERT ON ALL TABLES IN SCHEMA public TO <用户名>;
```

授予对表的权限

```sql {.wrap}
GRANT SELECT, UPDATE, INSERT ON <表名> TO <用户名>;
```

授予对表选择的权限

```sql {.wrap}
GRANT SELECT ON ALL TABLES IN SCHEMA public TO <用户名>;
```

### 列

[添加列](http://www.postgresql.org/docs/current/static/sql-altertable.html)

```sql {.wrap}
ALTER TABLE <表名> IF EXISTS
ADD <列名> <数据类型> [<约束>];
```

更新列

```sql {.wrap}
ALTER TABLE <表名> IF EXISTS
ALTER <列名> TYPE <数据类型> [<约束>];
```

删除列

```sql {.wrap}
ALTER TABLE <表名> IF EXISTS
DROP <列名>;
```

更新列为自增主键

```sql {.wrap}
ALTER TABLE <表名>
ADD COLUMN <列名> SERIAL PRIMARY KEY;
```

向带自增主键的表中插入数据

```sql {.wrap}
INSERT INTO <表名>
VALUES (DEFAULT, <值1>);


INSERT INTO <表名> (<列1名>,<列2名>)
VALUES ( <值1>,<值2> );
```

### 数据

[选择](http://www.postgresql.org/docs/current/static/sql-select.html)所有数据

```sql {.wrap}
SELECT * FROM <表名>;
```

读取一行数据

```sql {.wrap}
SELECT * FROM <表名> LIMIT 1;
```

搜索数据

```sql {.wrap}
SELECT * FROM <表名> WHERE <列名> = <值>;
```

[插入](http://www.postgresql.org/docs/current/static/sql-insert.html)数据

```sql {.wrap}
INSERT INTO <表名> VALUES( <值1>, <值2> );
```

[更新](http://www.postgresql.org/docs/current/static/sql-update.html)数据

```sql {.wrap}
UPDATE <表名>
SET <列1> = <值1>, <列2> = <值2>
WHERE <列1> = <值>;
```

[删除](http://www.postgresql.org/docs/current/static/sql-delete.html)所有数据

```sql {.wrap}
DELETE FROM <表名>;
```

删除特定数据

```sql {.wrap}
DELETE FROM <表名>
WHERE <列名> = <值>;
```

### 用户

列出角色

```sql {.wrap}
SELECT rolname FROM pg_roles;
```

[创建用户](http://www.postgresql.org/docs/current/static/sql-createuser.html)

```sql {.wrap}
CREATE USER <用户名> WITH PASSWORD '<密码>';
```

[删除用户](http://www.postgresql.org/docs/current/static/sql-dropuser.html)

```sql {.wrap}
DROP USER IF EXISTS <用户名>;
```

[修改](http://www.postgresql.org/docs/current/static/sql-alterrole.html)用户密码

```sql {.wrap}
ALTER ROLE <用户名> WITH PASSWORD '<密码>';
```

### 模式

列出模式

```sql {.wrap}
\dn

SELECT schema_name FROM information_schema.schemata;

SELECT nspname FROM pg_catalog.pg_namespace;
```

[创建模式](http://www.postgresql.org/docs/current/static/sql-createschema.html)

```sql {.wrap}
CREATE SCHEMA IF NOT EXISTS <模式名>;
```

[删除模式](http://www.postgresql.org/docs/current/static/sql-dropschema.html)

```sql {.wrap}
DROP SCHEMA IF EXISTS <模式名> CASCADE;
```

### 日期

显示[当前日期](https://www.postgresql.org/docs/15/functions-datetime.html#FUNCTIONS-DATETIME-CURRENT) YYYY-MM-DD

```sql {.wrap}
SELECT current_date;
```

计算两个日期之间的[年龄](<https://www.postgresql.org/docs/15/functions-datetime.html#:~:text=age%20(%20timestamp%2C%20timestamp%20)%20%E2%86%92%20interval>)

```sql {.wrap}
SELECT age(timestamp, timestamp);
```

显示带时区的[当前时间](https://www.postgresql.org/docs/15/functions-datetime.html#FUNCTIONS-DATETIME-CURRENT)

```sql {.wrap}
SELECT current_time;
```

使用整数[创建](<https://www.postgresql.org/docs/15/functions-datetime.html#:~:text=make_date%20(%20year%20int%2C%20month%20int%2C%20day%20int%20)%20%E2%86%92%20date>)日期

```sql {.wrap}
SELECT make_date(2021,03,25);
```

## PostgreSQL 命令

### 表

| -                | -                               |
| ---------------- | :------------------------------ |
| `\d <表>`        | 描述表                          |
| `\d+ <表>`       | 描述表（带详细信息）            |
| `\dt`            | 列出当前模式的表                |
| `\dt *.*`        | 列出所有模式的表                |
| `\dt <模式>.*`   | 列出指定模式的表                |
| `\dp`            | 列出表访问权限                  |
| `\det[+]`        | 列出外部表                      |

### 查询缓冲区

| -            | -                                  |
| ------------ | :--------------------------------- |
| `\e [文件]`  | 编辑查询缓冲区（或文件）           |
| `\ef [函数]` | 编辑函数定义                       |
| `\p`         | 显示内容                           |
| `\r`         | 重置（清除）查询缓冲区             |
| `\s [文件]`  | 显示历史记录或将其保存到文件       |
| `\w 文件`    | 将查询缓冲区写入文件               |

### 信息性 {.row-span-4}

| -               | -                               |
| --------------- | :------------------------------ |
| `\l[+]`         | 列出所有数据库                  |
| `\dn[S+]`       | 列出模式                        |
| `\di[S+]`       | 列出索引                        |
| `\du[+]`        | 列出角色                        |
| `\ds[S+]`       | 列出序列                        |
| `\df[antw][S+]` | 列出函数                        |
| `\deu[+]`       | 列出用户映射                    |
| `\dv[S+]`       | 列出视图                        |
| `\dl`           | 列出大对象                      |
| `\dT[S+]`       | 列出数据类型                    |
| `\da[S]`        | 列出聚合函数                    |
| `\db[+]`        | 列出表空间                      |
| `\dc[S+]`       | 列出转换                        |
| `\dC[+]`        | 列出类型转换                    |
| `\ddp`          | 列出默认权限                    |
| `\dd[S]`        | 显示对象描述                    |
| `\dD[S+]`       | 列出域                          |
| `\des[+]`       | 列出外部服务器                  |
| `\dew[+]`       | 列出外部数据包装器              |
| `\dF[+]`        | 列出文本搜索配置                |
| `\dFd[+]`       | 列出文本搜索字典                |
| `\dFp[+]`       | 列出文本搜索解析器              |
| `\dFt[+]`       | 列出文本搜索模板                |
| `\dL[S+]`       | 列出过程语言                    |
| `\do[S]`        | 列出操作符                      |
| `\dO[S+]`       | 列出排序规则                    |
| `\drds`         | 列出每个数据库的角色设置        |
| `\dx[+]`        | 列出扩展                        |

`S`: 显示系统对象, `+`: 附加详细信息

### 连接

| -                      | -                           |
| ---------------------- | :-------------------------- |
| `\c [数据库名]`        | 连接到新数据库              |
| `\encoding [编码]`     | 显示或设置客户端编码        |
| `\password [用户]`     | 更改密码                    |
| `\conninfo`            | 显示连接信息                |

### 格式化

| -                         | -                                          |
| ------------------------- | :----------------------------------------- |
| `\a`                      | 在未对齐和对齐之间切换                     |
| `\C [字符串]`             | 设置表标题，如果无则取消设置               |
| `\f [字符串]`             | 显示或设置未对齐输出的字段分隔符           |
| `\H`                      | 切换 HTML 输出模式                         |
| <code>\t [on\|off]</code> | 仅显示行                                   |
| `\T [字符串]`             | 设置或取消设置 HTML \<table\> 标签属性     |
| <code>\x [on\|off]</code> | 切换扩展输出模式                           |

### 输入/输出

| -                 | -                                                              |
| ----------------- | :------------------------------------------------------------- |
| `\copy ...`       | 导入/导出表<br> _另请参阅:_ [copy](#导入导出-csv)               |
| `\echo [字符串]`  | 打印字符串                                                     |
| `\i 文件`         | 执行文件                                                       |
| `\o [文件]`       | 将所有结果导出到文件                                           |
| `\qecho [字符串]` | 将字符串输出到输出流                                           |

### 变量

| -                     | -                                             |
| --------------------- | :-------------------------------------------- |
| `\prompt [文本] 名称` | 设置变量                                      |
| `\set [名称 [值]]`    | 设置变量 _（如果没有参数则列出所有变量）_       |
| `\unset 名称`         | 删除变量                                      |

### 其他

| -                              | -                    |
| ------------------------------ | :------------------- |
| `\cd [目录]`                   | 更改目录             |
| <code>\timing [on\|off]</code> | 切换计时             |
| `\! [命令]`                    | 在 shell 中执行      |
| `\! ls -l`                     | 在 shell 中列出所有  |

### 大对象

- `\lo_export LOBOID 文件`
- `\lo_import 文件 [注释]`
- `\lo_list`
- `\lo_unlink LOBOID`

{.marker-none}

## 其他事项

### 备份

使用 pg_dumpall 备份所有数据库

```shell script
$ pg_dumpall -U postgres > all.sql
```

使用 pg_dump 备份数据库

```shell script
$ pg_dump -d mydb -f mydb_backup.sql
```

| -    | -                                              |
| ---- | :--------------------------------------------- |
| `-a` | 仅转储数据，不转储模式                         |
| `-s` | 仅转储模式，不转储数据                         |
| `-c` | 在重新创建之前删除数据库                       |
| `-C` | 在恢复之前创建数据库                           |
| `-t` | 仅转储指定的表                                 |
| `-F` | 格式 (`c`: 自定义, `d`: 目录, `t`: tar)        |

使用 `pg_dump -?` 获取完整的选项列表

### 恢复

使用 psql 恢复数据库

```shell script
$ psql -U user mydb < mydb_backup.sql
```

使用 pg_restore 恢复数据库

```shell script
$ pg_restore -d mydb mydb_backup.sql -c
```

| -    | -                                                                            |
| ---- | :--------------------------------------------------------------------------- |
| `-U` | 指定数据库用户                                                               |
| `-c` | 在重新创建之前删除数据库                                                     |
| `-C` | 在恢复之前创建数据库                                                         |
| `-e` | 如果遇到错误则退出                                                           |
| `-F` | 格式 (`c`: 自定义, `d`: 目录, `t`: tar, `p`: 纯文本 SQL (默认))              |

{.marker-none}

使用 `pg_restore -?` 获取完整的选项列表

### 远程访问

获取 postgresql.conf 的位置

```shell script
$ psql -U postgres -c 'SHOW config_file'
```

附加到 postgresql.conf

```shell script
listen_addresses = '*'
```

附加到 pg_hba.conf (与 postgresql.conf 位置相同)

```shell script
host  all  all  0.0.0.0/0  md5
host  all  all  ::/0       md5
```

重启 PostgreSQL 服务器

```shell script
$ sudo systemctl restart postgresql
```

### 导入/导出 CSV

将表导出到 CSV 文件

```shell script
\copy 表 TO '<路径>' CSV
\copy 表(列1,列2) TO '<路径>' CSV
\copy (SELECT...) TO '<路径>' CSV
```

将 CSV 文件导入到表

```shell script
\copy 表 FROM '<路径>' CSV
\copy 表(列1,列2) FROM '<路径>' CSV
```

另请参阅: [Copy](https://www.postgresql.org/docs/current/sql-copy.html)

## 另请参阅

- [Posgres-cheatsheet](https://gist.github.com/apolloclark/ea5466d5929e63043dcf#posgres-cheatsheet) _(gist.github.com)_
