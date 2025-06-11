---
title: Neo4j
date: 2021-08-23 12:34:56
background: bg-[#3b85ef]
tags:
  - 数据库
  - 图数据库
categories:
  - 数据库
intro: |
  一份 Neo4j 速查表，包含入门资源以及如何使用 Cypher 查询数据库的信息。
plugins:
  - copyCode
---

## 入门指南 {.cols-2}

### Neo4j 入门

Neo4j 是一个图数据库，由通过关系连接在一起的节点组成。如果您的数据集高度连接或查询包含许多连接操作，您可能会考虑使用图数据库。

- [下载 Neo4j 桌面版](https://neo4j.com/download) _下载 Neo4j 桌面版或服务器版_
- [Neo4j 沙盒](https://sandbox.neo4j.com) _选择一个数据集 - 无需安装_
- [Neo4j Aura](https://neo4j.com/aura) _云端免费 Neo4j 实例_
- [Neo4j 图学院](https://neo4j.com/graphacademy) _免费、自定进度、实践性在线培训_
- [GraphGists](https://neo4j.com/graphgists) _用例和行业特定示例图_

### 图数据库概念

|                       |                                                                                                                                                                                                                                          |
| --------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **节点 (Nodes)**      | 节点通常用于表示数据中的_实体_或_事物_。例如，一个**Person**（人）或**Movie**（电影）。                                                                                                                                                           |
| **关系 (Relationships)** | 关系用于将两个节点连接在一起，并将数据组织成结构。例如，一个人**参演 (acted in)**一部电影。关系具有_类型_和_方向_，尽管在查询时可以忽略方向。                                                                                                                             |
| **标签 (Labels)**       | 标签用于将节点分组到类别中。例如，一个人可能同时拥有 `Person` 和 `Actor` 标签。                                                                                                                                                               |
| **关系类型 (Relationship Type)** | 每个关系都有一个类型。关系允许您探索图的较小部分。                                                                                                                                                                                |
| **属性 (Properties)**   | 节点和关系都可以设置属性。属性是[键值对](https://neo4j.com/docs/cypher-manual/4.3/syntax/values/#cypher-values)。                                                                                                                            |

## Neo4j 语法

### 读取查询结构

```
[USE]
[MATCH WHERE]
[OPTIONAL MATCH WHERE]
[WITH [ORDER BY] [SKIP] [LIMIT]]
RETURN [ORDER BY] [SKIP] [LIMIT]
```

### 只写查询结构

```
[USE]
(CREATE | MERGE)*
[SET|DELETE|REMOVE|FOREACH]*
[RETURN [ORDER BY] [SKIP] [LIMIT]]
```

### 读写查询结构

```
[USE]
[MATCH WHERE]
[OPTIONAL MATCH WHERE]
[WITH [ORDER BY] [SKIP] [LIMIT]]
(CREATE | MERGE)*
[SET|DELETE|REMOVE|FOREACH]*
[RETURN [ORDER BY] [SKIP] [LIMIT]]
```

## Neo4j 读取数据

### MATCH

```
MATCH (n:Person)-[:KNOWS]->(m:Person)
WHERE n.name = 'Alice'
```

节点模式可以包含标签和属性。

```
MATCH (n)-->(m)
```

任何模式都可以在 MATCH 中使用。

```
MATCH (n {name: 'Alice'})-->(m)
```

带有节点属性的模式。

```
MATCH p = (n)-->(m)
```

将路径分配给 p。

```
OPTIONAL MATCH (n)-[r]->(m)
```

可选模式：对于缺失的部分将使用 null。

### WHERE

```
WHERE n.property <> $value
```

使用谓词进行筛选。请注意，WHERE 始终是 MATCH、OPTIONAL MATCH 或 WITH 子句的一部分。将其放在查询中不同子句之后会改变其功能。

```
WHERE EXISTS {
  MATCH (n)-->(m) WHERE n.age = m.age
}
```

使用存在子查询进行筛选。

### RETURN

```
RETURN *
```

返回所有变量的值。

```
RETURN n AS columnName
```

为结果列名使用别名。

```
RETURN DISTINCT n
```

返回唯一的行。

```
ORDER BY n.property
```

对结果进行排序。

```
ORDER BY n.property DESC
```

按降序对结果进行排序。

```
SKIP $skipNumber
```

跳过一定数量的结果。

```
LIMIT $limitNumber
```

限制结果的数量。

```
SKIP $skipNumber LIMIT $limitNumber
```

跳过顶部的结果并限制结果的数量。

```
RETURN count(*)
```

匹配行的数量。更多信息请参见聚合函数。

### WITH

```
MATCH (user)-[:FRIEND]-(friend)
WHERE user.name = $name
WITH user, count(friend) AS friends
WHERE friends > 10
RETURN user
```

WITH 语法与 RETURN 类似。它明确分隔查询的各个部分，允许您声明要传递到下一部分的变量。

```
MATCH (user)-[:FRIEND]-(friend)
WITH user, count(friend) AS friends
ORDER BY friends DESC
  SKIP 1
  LIMIT 3
RETURN user
```

ORDER BY、SKIP 和 LIMIT 也可以与 WITH 一起使用。

### UNION

```
MATCH (a)-[:KNOWS]->(b)
RETURN b.name
UNION
MATCH (a)-[:LOVES]->(b)
RETURN b.name
```

返回所有查询结果的去重并集。结果列的类型和名称必须匹配。

```
MATCH (a)-[:KNOWS]->(b)
RETURN b.name
UNION ALL
MATCH (a)-[:LOVES]->(b)
RETURN b.name
```

返回所有查询结果的并集，包括重复的行。

## Neo4j 写入数据

### CREATE

```
CREATE (n {name: $value})
```

使用给定的属性创建一个节点。

```
CREATE (n $map)
```

使用给定的属性创建一个节点。

```
UNWIND $listOfMaps AS properties
CREATE (n) SET n = properties
```

使用给定的属性创建多个节点。

```
CREATE (n)-[r:KNOWS]->(m)
```

创建具有给定类型和方向的关系；并将一个变量绑定到它。

```
CREATE (n)-[:LOVES {since: $value}]->(m)
```

创建具有给定类型、方向和属性的关系。

### SET

```
SET n.property1 = $value1,
    n.property2 = $value2
```

更新或创建一个属性。

```
SET n = $map
```

设置所有属性。这将删除任何现有的属性。

```
SET n += $map
```

添加和更新属性，同时保留现有的属性。

```
SET n:Person
```

向节点添加 Person 标签。

### MERGE

```
MERGE (n:Person {name: $value})
  ON CREATE SET n.created = timestamp()
  ON MATCH SET
    n.counter = coalesce(n.counter, 0) + 1,
    n.accessTime = timestamp()
```

匹配一个模式，如果不存在则创建它。使用 ON CREATE 和 ON MATCH 进行条件更新。

```
MATCH (a:Person {name: $value1}),
      (b:Person {name: $value2})
MERGE (a)-[r:LOVES]->(b)
```

MERGE 查找或创建节点之间的关系。

```
MATCH (a:Person {name: $value1})
MERGE
  (a)-[r:KNOWS]->(b:Person {name: $value3})
```

MERGE 查找或创建附加到节点的路径。

### DELETE

```
DELETE n, r
```

删除一个节点和一个关系。

```
DETACH DELETE n
```

删除一个节点及其连接的所有关系。

```
MATCH (n)
DETACH DELETE n
```

从数据库中删除所有节点和关系。

### REMOVE

```
REMOVE n:Person
```

从 n 中删除一个标签。

```
REMOVE n.property
```

删除一个属性。

### FOREACH

```
FOREACH (r IN relationships(path) |
  SET r.marked = true)
```

对路径中的每个关系执行一个修改操作。

```
FOREACH (value IN coll |
 CREATE (:Person {name: value}))
```

对列表中的每个元素执行一个修改操作。

### CALL 子查询

```
CALL {
  MATCH (p:Person)-[:FRIEND_OF]->(other:Person) RETURN p, other
  UNION
  MATCH (p:Child)-[:CHILD_OF]->(other:Parent) RETURN p, other
}
```

这会调用一个包含两个联合部分的子查询。子查询的结果随后可以进行后处理。

### CALL 过程

```
CALL db.labels() YIELD label
```

这显示了对内置过程 db.labels 的独立调用，以列出数据库中使用的所有标签。请注意，所需的过程参数在过程名称后的括号中明确给出。

```
CALL db.labels() YIELD *
```

独立调用可以使用 YIELD * 返回所有列。

```
CALL java.stored.procedureWithArgs
```

独立调用可以省略 YIELD，也可以通过语句参数隐式提供参数，例如，一个需要一个参数输入的独立调用可以通过传递参数映射 {input: 'foo'} 来运行。

```
CALL db.labels() YIELD label
RETURN count(label) AS count
```

在一个更大的查询中调用内置过程 db.labels，以计算数据库中使用的所有标签。在更大的查询中调用过程总是需要传递参数并使用 YIELD 显式命名结果。

### 导入

```
LOAD CSV FROM
'https://neo4j.com/docs/cypher-refcard/4.3/csv/artists.csv' AS line
CREATE (:Artist {name: line[1], year: toInteger(line[2])})
```

从 CSV 文件加载数据并创建节点。

```
LOAD CSV WITH HEADERS FROM
'https://neo4j.com/docs/cypher-refcard/4.3/csv/artists-with-headers.csv' AS line
CREATE (:Artist {name: line.Name, year: toInteger(line.Year)})
```

加载带有表头的 CSV 数据。

```
USING PERIODIC COMMIT 500
LOAD CSV WITH HEADERS FROM
'https://neo4j.com/docs/cypher-refcard/4.3/csv/artists-with-headers.csv' AS line
CREATE (:Artist {name: line.Name, year: toInteger(line.Year)})
```

导入大量数据时，每 500 行提交一次当前事务。

```
LOAD CSV FROM
'https://neo4j.com/docs/cypher-refcard/4.3/csv/artists-fieldterminator.csv'
AS line FIELDTERMINATOR ';'
CREATE (:Artist {name: line[1], year: toInteger(line[2])})
```

使用不同的字段终止符，而不是默认的逗号（周围没有空格）。

```
LOAD CSV FROM
'https://neo4j.com/docs/cypher-refcard/4.3/csv/artists.csv' AS line
RETURN DISTINCT file()
```

返回 LOAD CSV 正在处理的文件的绝对路径，如果在 LOAD CSV 上下文之外调用，则返回 null。

```
LOAD CSV FROM
'https://neo4j.com/docs/cypher-refcard/4.3/csv/artists.csv' AS line
RETURN linenumber()
```

返回 LOAD CSV 当前正在处理的行号，如果在 LOAD CSV 上下文之外调用，则返回 null。

### 运算符

|                        |                                           |
| ---------------------- | ----------------------------------------- |
| **通用 (General)**     | DISTINCT, ., []                           |
| **数学 (Mathematical)**  | +, -, \*, /, %, ^                         |
| **比较 (Comparison)**    | =, <>, <, >, <=, >=, IS NULL, IS NOT NULL |
| **布尔 (Boolean)**     | AND, OR, XOR, NOT                         |
| **字符串 (String)**    | +                                         |
| **列表 (List)**        | +, IN, [x], [x .. y]                      |
| **正则表达式 (Regular Expression)** | =~                                        |
| **字符串匹配 (String matching)** | STARTS WITH, ENDS WITH, CONTAINS          |

### null

- `null` 用于表示缺失/未定义的值。
- `null` 不等于 `null`。不知道两个值并不意味着它们是相同的值。因此，表达式 `null = null` 的结果是 `null` 而不是 `true`。要检查表达式是否为 `null`，请使用 `IS NULL`。
- 如果任何参数为 `null`，算术表达式、比较和函数调用（`coalesce` 除外）将返回 `null`。
- 尝试访问列表中缺失的元素或不存在的属性会产生 `null`。
- 在 `OPTIONAL MATCH` 子句中，`null` 将用于模式的缺失部分。

### 模式

```
(n:Person)
```

带有 Person 标签的节点。

```
(n:Person:Swedish)
```

同时带有 Person 和 Swedish 标签的节点。

```
(n:Person {name: $value})
```

带有声明属性的节点。

```
()-[r {name: $value}]-()
```

匹配具有声明属性的关系。

```
(n)-->(m)
```

从 n 到 m 的关系。

```
(n)--(m)
```

n 和 m 之间任意方向的关系。

```
(n:Person)-->(m)
```

标记为 Person 的节点 n 与 m 存在关系。

```
(m)<-[:KNOWS]-(n)
```

从 n 到 m 的 KNOWS 类型的关系。

```
(n)-[:KNOWS|:LOVES]->(m)
```

从 n 到 m 的 KNOWS 类型或 LOVES 类型的关系。

```
(n)-[r]->(m)
```

将关系绑定到变量 r。

```
(n)-[*1..5]->(m)
```

从 n 到 m 的长度在 1 到 5 个关系之间的可变长度路径。

```
(n)-[*]->(m)
```

从 n 到 m 的任意数量关系的可变长度路径。（请参见性能部分。）

```
(n)-[:KNOWS]->(m {property: $value})
```

从节点 n 到具有声明属性的节点 m 的 KNOWS 类型的关系。

```
shortestPath((n1:Person)-[*..6]-(n2:Person))
```

查找单个最短路径。

```
allShortestPaths((n1:Person)-[*..6]->(n2:Person))
```

查找所有最短路径。

```
size((n)-->()-->())
```

计算匹配模式的路径数量。

### USE

```
USE myDatabase
```

选择 myDatabase 以对其执行查询或查询部分。

```
USE neo4j
MATCH (n:Person)-[:KNOWS]->(m:Person)
WHERE n.name = 'Alice'
```

针对 neo4j 数据库执行的 MATCH 查询。

### SHOW 函数和过程

```
SHOW FUNCTIONS
```

列出所有可用的函数。

```
SHOW PROCEDURES EXECUTABLE YIELD name
```

列出当前用户可以执行的所有过程，并仅返回过程的名称。

### 标签

```
CREATE (n:Person {name: $value})
```

创建带有标签和属性的节点。

```
MERGE (n:Person {name: $value})
```

匹配或创建具有标签和属性的唯一节点。

```
SET n:Spouse:Parent:Employee
```

向节点添加标签。

```
MATCH (n:Person)
```

匹配标记为 Person 的节点。

```
MATCH (n:Person)
WHERE n.name = $value
```

匹配标记为 Person 且具有给定名称的节点。

```
WHERE (n:Person)
```

检查节点上标签的存在性。

```
labels(n)
```

节点的标签。

```
REMOVE n:Person
```

从节点中删除标签。

### 列表

```
['a', 'b', 'c'] AS list
```

字面量列表在方括号中声明。

```
size($list) AS len, $list[0] AS value
```

列表可以作为参数传入。

```
range($firstNum, $lastNum, $step) AS list
```

range() 创建一个数字列表（step 是可选的），其他返回列表的函数有：labels()、nodes()、relationships()。

```
MATCH p = (a)-[:KNOWS*]->()
RETURN relationships(p) AS r
```

包含可变长度路径的关系列表可以使用命名路径和 relationships() 返回。

```
RETURN matchedNode.list[0] AS value,
       size(matchedNode.list) AS len
```

属性可以是字符串、数字或布尔值的列表。

```
list[$idx] AS value,
list[$startIdx..$endIdx] AS slice
```

列表元素可以通过方括号中的 idx 下标访问。无效索引返回 null。可以使用从 start_idx 到 end_idx 的区间检索切片，其中每个索引都可以省略或为负数。超出范围的元素将被忽略。

```
UNWIND $names AS name
MATCH (n {name: name})
RETURN avg(n.age)
```

使用 UNWIND，任何列表都可以转换回单独的行。该示例匹配名称列表中的所有名称。

```
MATCH (a)
RETURN [(a)-->(b) WHERE b.name = 'Bob' | b.age]
```

模式推导可用于将匹配结果直接自定义投影到列表中。

```
MATCH (person)
RETURN person { .name, .age}
```

映射投影可以很容易地从节点、关系和其他映射值构建。

### 映射

```
{name: 'Alice', age: 38,
 address: {city: 'London', residential: true}}
```

字面量映射在花括号中声明，非常像属性映射。支持列表。

```
WITH {person: {name: 'Anne', age: 25}} AS p
RETURN p.person.name
```

访问嵌套映射的属性。

```
MERGE (p:Person {name: $map.name})
  ON CREATE SET p = $map
```

映射可以作为参数传入，并可以用作映射或通过访问键来使用。

```
MATCH (matchedNode:Person)
RETURN matchedNode
```

节点和关系作为其数据的映射返回。

```
map.name, map.age, map.children[0]
```

映射条目可以通过其键访问。无效的键会导致错误。

### 谓词

```
n.property <> $value
```

使用比较运算符。

```
toString(n.property) = $value
```

使用函数。

```
n.number >= 1 AND n.number <= 10
```

使用布尔运算符组合谓词。

```
1 <= n.number <= 10
```

使用链式运算符组合谓词。

```
n:Person
```

检查节点标签。

```
variable IS NOT NULL
```

检查某物是否不为 null，例如属性是否存在。

```
n.property IS NULL OR n.property = $value
```

属性不存在或谓词为真。

```
n.property = $value
```

不存在的属性返回 null，它不等于任何东西。

```
n["property"] = $value
```

属性也可以使用动态计算的属性名称进行访问。

```
n.property STARTS WITH 'Tim' OR
n.property ENDS WITH 'n' OR
n.property CONTAINS 'goodie'
```

字符串匹配。

```
n.property =~ 'Tim.*'
```

字符串正则表达式匹配。

```
(n)-[:KNOWS]->(m)
```

确保模式至少有一个匹配项。

```
NOT (n)-[:KNOWS]->(m)
```

从结果中排除与 (n)-[:KNOWS]->(m) 的匹配项。

```
n.property IN [$value1, $value2]
```

检查列表中是否存在元素。

### 列表谓词

```
all(x IN coll WHERE x.property IS NOT NULL)
```

如果列表中所有元素的谓词都为真，则返回 true。

```
any(x IN coll WHERE x.property IS NOT NULL)
```

如果列表中至少有一个元素的谓词为真，则返回 true。

```
none(x IN coll WHERE x.property IS NOT NULL)
```

如果列表中所有元素的谓词都为假，则返回 true。

```
single(x IN coll WHERE x.property IS NOT NULL)
```

如果列表中恰好有一个元素的谓词为真，则返回 true。

### CASE

```
CASE n.eyes
 WHEN 'blue' THEN 1
 WHEN 'brown' THEN 2
 ELSE 3
END
```

从匹配的 WHEN 值返回 THEN 值。ELSE 值是可选的，如果缺失则替换为 null。

```
CASE
 WHEN n.eyes = 'blue' THEN 1
 WHEN n.age < 40 THEN 2
 ELSE 3
END
```

从第一个计算结果为 true 的 WHEN 谓词返回 THEN 值。谓词按顺序评估。

### 列表表达式

```
size($list)
```

列表中的元素数量。

```
reverse($list)
```

反转列表中元素的顺序。

```
head($list), last($list), tail($list)
```

head() 返回列表的第一个元素，last() 返回最后一个元素。tail() 返回除第一个元素外的所有元素。对于空列表，所有这些函数都返回 null。

```
[x IN list | x.prop]
```

原始列表中每个元素的表达式值的列表。

```
[x IN list WHERE x.prop <> $value]
```

谓词为真的元素的筛选列表。

```
[x IN list WHERE x.prop <> $value | x.prop]
```

一个列表推导，它筛选列表并提取该列表中每个元素的表达式值。

```
reduce(s = "", x IN list | s + x.prop)
```

对列表中的每个元素评估表达式，并累积结果。

### 函数

```
coalesce(n.property, $defaultValue)
```

第一个非 null 表达式。

```
timestamp()
```

自 1970 年 1 月 1 日午夜 UTC 以来的毫秒数。

```
id(nodeOrRelationship)
```

关系或节点的内部 ID。

```
toInteger($expr)
```

如果可能，将给定输入转换为整数；否则返回 null。

```
toFloat($expr)
```

如果可能，将给定输入转换为浮点数；否则返回 null。

```
toBoolean($expr)
```

如果可能，将给定输入转换为布尔值；否则返回 null。

```
keys($expr)
```

返回节点、关系或映射的属性名称的字符串表示列表。

```
properties($expr)
```

返回包含节点或关系所有属性的映射。

### 路径函数

```
length(path)
```

路径中的关系数量。

```
nodes(path)
```

路径中的节点（作为列表）。

```
relationships(path)
```

路径中的关系（作为列表）。

```
[x IN nodes(path) | x.prop]
```

从路径中的节点提取属性。

### 空间函数

```
point({x: $x, y: $y})
```

返回二维笛卡尔坐标系中的一个点。

```
point({latitude: $y, longitude: $x})
```

返回二维地理坐标系中的一个点，坐标以十进制度指定。

```
point({x: $x, y: $y, z: $z})
```

返回三维笛卡尔坐标系中的一个点。

```
point({latitude: $y, longitude: $x, height: $z})
```

返回三维地理坐标系中的一个点，纬度和经度以十进制度指定，高度以米为单位。

```
distance(point({x: $x1, y: $y1}), point({x: $x2, y: $y2}))
```

返回表示两点之间线性距离的浮点数。返回的单位将与点坐标的单位相同，并且它适用于二维和三维笛卡尔点。

```
distance(point({latitude: $y1, longitude: $x1}), point({latitude: $y2, longitude: $x2}))
```

返回两点之间的测地距离（以米为单位）。它也可以用于三维地理点。

## Neo4j 函数

### 时间函数

```
date("2018-04-05")
```

从字符串解析并返回日期。

```
localtime("12:45:30.25")
```

返回没有时区的时间。

```
time("12:45:30.25+01:00")
```

返回指定时区的时间。

```
localdatetime("2018-04-05T12:34:00")
```

返回没有时区的日期时间。

```
datetime("2018-04-05T12:34:00[Europe/Berlin]")
```

返回指定时区的日期时间。

```
datetime({epochMillis: 3360000})
```

将 3360000 作为 UNIX Epoch 时间转换为正常的日期时间。

```
date({year: $year, month: $month, day: $day})
```

所有时间函数也可以使用命名组件的映射来调用。此示例从年、月和日组件返回日期。每个函数支持一组不同的可能组件。

```
datetime({date: $date, time: $time})
```

时间类型可以通过组合其他类型来创建。此示例从日期和时间创建日期时间。

```
date({date: $datetime, day: 5})
```

时间类型可以通过从更复杂的类型中选择以及覆盖单个组件来创建。此示例通过从日期时间中选择并覆盖日组件来创建日期。

```
WITH date("2018-04-05") AS d
RETURN d.year, d.month, d.day, d.week, d.dayOfWeek
```

访问器允许提取时间类型的组件。

### 持续时间函数

```
duration("P1Y2M10DT12H45M30.25S")
```

返回 1 年 2 个月 10 天 12 小时 45 分钟 30.25 秒的持续时间。

```
duration.between($date1,$date2)
```

返回两个时间实例之间的持续时间。

```
WITH duration("P1Y2M10DT12H45M") AS d
RETURN d.years, d.months, d.days, d.hours, d.minutes
```

返回 1 年、14 个月、10 天、12 小时和 765 分钟。

```
WITH duration("P1Y2M10DT12H45M") AS d
RETURN d.years, d.monthsOfYear, d.days, d.hours, d.minutesOfHour
```

返回 1 年、2 个月、10 天、12 小时和 45 分钟。

```
date("2015-01-01") + duration("P1Y1M1D")
```

返回日期 2016-02-02。也可以从时间实例中减去持续时间。

```
duration("PT30S") * 10
```

返回 5 分钟的持续时间。也可以将持续时间除以一个数字。

### 数学函数

```
abs($expr)
```

绝对值。

```
rand()
```

返回一个范围从 0（含）到 1（不含）的随机数，[0,1)。每次调用返回一个新值。也用于选择子集或随机排序。

```
round($expr)
```

四舍五入到最接近的整数；ceil() 和 floor() 分别向上或向下取整。

```
sqrt($expr)
```

平方根。

```
sign($expr)
```

如果为零则为 0，如果为负则为 -1，如果为正则为 1。

```
sin($expr)
```

三角函数还包括 cos()、tan()、cot()、asin()、acos()、atan()、atan2() 和 haversin()。除非另有说明，否则三角函数的所有参数都应以弧度为单位。

```
degrees($expr), radians($expr), pi()
```

将弧度转换为度；使用 radians() 进行反向转换，使用 pi() 表示 π。

```
log10($expr), log($expr), exp($expr), e()
```

以 10 为底的对数、自然对数、e 的参数次幂以及 e 的值。

### 字符串函数

```
toString($expression)
```

表达式的字符串表示。

```
replace($original, $search, $replacement)
```

将所有出现的 search 替换为 replacement。所有参数都必须是表达式。

```
substring($original, $begin, $subLength)
```

获取字符串的一部分。subLength 参数是可选的。

```
left($original, $subLength),
  right($original, $subLength)
```

字符串的第一部分。字符串的最后一部分。

```
trim($original), lTrim($original),
  rTrim($original)
```

去除所有空格，或去除左侧或右侧的空格。

```
toUpper($original), toLower($original)
```

大写和小写。

```
split($original, $delimiter)
```

将字符串拆分为字符串列表。

```
reverse($original)
```

反转字符串。

```
size($string)
```

计算字符串中的字符数。

### 关系函数

```
type(a_relationship)
```

关系类型的字符串表示。

```
startNode(a_relationship)
```

关系的起始节点。

```
endNode(a_relationship)
```

关系的结束节点。

```
id(a_relationship)
```

关系的内部 ID。

### 聚合函数

```
count(*)
```

匹配行的数量。

```
count(variable)
```

非 null 值的数量。

```
count(DISTINCT variable)
```

所有聚合函数也都接受 DISTINCT 运算符，该运算符从值中删除重复项。

```
collect(n.property)
```

从值创建列表，忽略 null。

```
sum(n.property)
```

对数值求和。类似的函数有 avg()、min()、max()。

```
percentileDisc(n.property, $percentile)
```

离散百分位数。连续百分位数是 percentileCont()。百分位数参数范围从 0.0 到 1.0。

```
stDev(n.property)
```

总体样本的标准差。对于整个总体，请使用 stDevP()。

## Neo4j 模式操作

### 索引 (INDEX)

```
CREATE INDEX FOR (p:Person) ON (p.name)
```

在具有 Person 标签和 name 属性的节点上创建索引。

```
CREATE INDEX index_name FOR ()-[k:KNOWS]-() ON (k.since)
```

在具有 KNOWS 类型和 since 属性的关系上创建名为 index_name 的索引。

```
CREATE INDEX FOR (p:Person) ON (p.surname)
OPTIONS {indexProvider: 'native-btree-1.0', indexConfig: {`spatial.cartesian.min`: [-100.0, -100.0], `spatial.cartesian.max`: [100.0, 100.0]}}
```

在具有 Person 标签和 surname 属性的节点上创建索引，索引提供程序为 native-btree-1.0，并使用给定的 spatial.cartesian 设置。其他索引设置将使用其默认值。

```
CREATE INDEX FOR (p:Person) ON (p.name, p.age)
```

在具有 Person 标签以及 name 和 age 属性的节点上创建复合索引，如果索引已存在则抛出错误。

```
CREATE INDEX IF NOT EXISTS FOR (p:Person) ON (p.name, p.age)
```

如果尚不存在，则在具有 Person 标签以及 name 和 age 属性的节点上创建复合索引；如果已存在，则不执行任何操作。

```
CREATE LOOKUP INDEX lookup_index_name FOR (n) ON EACH labels(n)
```

在具有任何标签的节点上创建名为 lookup_index_name 的令牌查找索引。

```
CREATE LOOKUP INDEX FOR ()-[r]-() ON EACH type(r)
```

在具有任何关系类型的关系上创建令牌查找索引。

```
CREATE FULLTEXT INDEX node_fulltext_index_name FOR (n:Friend) ON EACH [n.name]
OPTIONS {indexConfig: {`fulltext.analyzer`: 'swedish'}}
```

在节点上创建名为 node_fulltext_index_name 且分析器为 swedish 的全文索引。节点上的全文索引只能通过过程 db.index.fulltext.queryNodes 使用。其他索引设置将使用其默认值。

```
CREATE FULLTEXT INDEX rel_fulltext_index_name FOR ()-[r:HAS_PET|BROUGHT_PET]-() ON EACH [r.since, r.price]
```

在关系上创建名为 rel_fulltext_index_name 的全文索引。关系上的全文索引只能通过过程 db.index.fulltext.queryRelationships 使用。

```
SHOW INDEXES
```

列出所有索引。

```
MATCH (n:Person) WHERE n.name = $value
```

索引可以自动用于相等比较。请注意，例如 toLower(n.name) = $value 将不会使用索引。

```
MATCH (n:Person)
WHERE n.name IN [$value]
```

索引可以自动用于 IN 列表检查。

```
MATCH (n:Person)
WHERE n.name = $value and n.age = $value2
```

复合索引可以自动用于两个属性的相等比较。请注意，复合索引的所有属性上都需要有谓词才能使用它。

```
MATCH (n:Person)
USING INDEX n:Person(name)
WHERE n.name = $value
```

当 Cypher 使用次优索引或应使用多个索引时，可以强制使用索引。

```
DROP INDEX index_name
```

删除名为 index_name 的索引，如果索引不存在则抛出错误。

```
DROP INDEX index_name IF EXISTS
```

如果名为 index_name 的索引存在，则删除它；如果不存在，则不执行任何操作。

### 约束 (CONSTRAINT)

```
CREATE CONSTRAINT ON (p:Person)
       ASSERT p.name IS UNIQUE
```

在 Person 标签和 name 属性上创建唯一属性约束。如果任何其他具有该标签的节点在更新或创建时使用了已存在的名称，则写入操作将失败。此约束将创建一个附带的索引。

```
CREATE CONSTRAINT uniqueness ON (p:Person)
       ASSERT p.age IS UNIQUE
```

在 Person 标签和 age 属性上创建名为 uniqueness 的唯一属性约束。如果任何其他具有该标签的节点在更新或创建时使用了已存在的年龄，则写入操作将失败。此约束将创建一个附带的索引。

```
CREATE CONSTRAINT ON (p:Person)
       ASSERT p.surname IS UNIQUE
       OPTIONS {indexProvider: 'native-btree-1.0'}
```

在 Person 标签和 surname 属性上创建唯一属性约束，附带索引的索引提供程序为 native-btree-1.0。

```
CREATE CONSTRAINT ON (p:Person)
       ASSERT p.name IS NOT NULL
```

(★) 在 Person 标签和 name 属性上创建节点属性存在约束，如果约束已存在则抛出错误。如果创建具有该标签的节点时没有名称，或者从具有 Person 标签的现有节点中删除了 name 属性，则写入操作将失败。

```
CREATE CONSTRAINT node_exists IF NOT EXISTS ON (p:Person)
       ASSERT p.name IS NOT NULL
```

(★) 如果 Person 标签和 name 属性上的节点属性存在约束或任何名为 node_exists 的约束已存在，则不执行任何操作。如果不存在此类约束，则将创建它。

```
CREATE CONSTRAINT ON ()-[l:LIKED]-()
       ASSERT l.when IS NOT NULL
```

(★) 在 LIKED 类型和 when 属性上创建关系属性存在约束。如果创建具有该类型的关系时没有 when 属性，或者从具有 LIKED 类型的现有关系中删除了 when 属性，则写入操作将失败。

```
CREATE CONSTRAINT relationship_exists ON ()-[l:LIKED]-()
       ASSERT l.since IS NOT NULL
```

(★) 在 LIKED 类型和 since 属性上创建名为 relationship_exists 的关系属性存在约束。如果创建具有该类型的关系时没有 since 属性，或者从具有 LIKED 类型的现有关系中删除了 since 属性，则写入操作将失败。

```
SHOW UNIQUE CONSTRAINTS YIELD *
```

列出所有唯一约束。

```
CREATE CONSTRAINT ON (p:Person)
      ASSERT (p.firstname, p.surname) IS NODE KEY
```

(★) 在 Person 标签以及 firstname 和 surname 属性上创建节点键约束。如果创建具有该标签的节点时没有 firstname 和 surname，或者两者的组合不是唯一的，或者具有 Person 标签的现有节点上的 firstname 和/或 surname 标签被修改以违反这些约束，则写入操作将失败。

```
CREATE CONSTRAINT node_key ON (p:Person)
      ASSERT (p.name, p.surname) IS NODE KEY
```

(★) 在 Person 标签以及 name 和 surname 属性上创建名为 node_key 的节点键约束。如果创建具有该标签的节点时没有 name 和 surname，或者两者的组合不是唯一的，或者具有 Person 标签的现有节点上的 name 和/或 surname 标签被修改以违反这些约束，则写入操作将失败。

```
CREATE CONSTRAINT node_key_with_config ON (p:Person)
      ASSERT (p.name, p.age) IS NODE KEY
      OPTIONS {indexConfig: {`spatial.wgs-84.min`: [-100.0, -100.0], `spatial.wgs-84.max`: [100.0, 100.0]}}
```

(★) 在 Person 标签以及 name 和 age 属性上创建名为 node_key_with_config 的节点键约束，并为附带索引提供给定的 spatial.wgs-84 设置。其他索引设置将使用其默认值。

```
DROP CONSTRAINT uniqueness
```

删除名为 uniqueness 的约束，如果约束不存在则抛出错误。

```
DROP CONSTRAINT uniqueness IF EXISTS
```

如果名为 uniqueness 的约束存在，则删除它；如果不存在，则不执行任何操作。

### 性能

- 尽可能使用参数而不是字面量。这允许 Cypher 重用您的查询，而不必解析和构建新的执行计划。
- 始终为您的可变长度模式设置上限。查询可能会意外地失控并触及图中的所有节点。
- 仅返回您需要的数据。避免返回整个节点和关系——相反，选择您需要的数据并仅返回那些数据。
- 使用 `PROFILE` / `EXPLAIN` 来分析查询的性能。有关这些主题以及其他主题（例如计划器提示）的更多信息，请参见[查询调优](https://neo4j.com/docs/cypher-manual/4.3/query-tuning)。

## Neo4j 多数据库

### 数据库管理

```
CREATE OR REPLACE DATABASE myDatabase
```

(★) 创建一个名为 myDatabase 的数据库。如果已存在同名数据库，则删除现有数据库并创建一个新数据库。

```
STOP DATABASE myDatabase
```

(★) 停止数据库 myDatabase。

```
START DATABASE myDatabase
```

(★) 启动数据库 myDatabase。

```
SHOW DATABASES
```

列出系统中的所有数据库及其信息。

```
SHOW DATABASES
YIELD name, currentStatus
WHERE name CONTAINS 'my' AND currentStatus = 'online'
```

列出有关数据库的信息，按名称和在线状态筛选，并根据这些条件进一步细化。

```
SHOW DATABASE myDatabase
```

列出有关数据库 myDatabase 的信息。

```
SHOW DEFAULT DATABASE
```

列出有关默认数据库的信息。

```
SHOW HOME DATABASE
```

列出有关当前用户主数据库的信息。

```
DROP DATABASE myDatabase IF EXISTS
```

(★) 如果数据库 myDatabase 存在，则删除它。

## Neo4j 安全

### 用户管理

```
CREATE USER alice SET PASSWORD $password
```

创建一个新用户和密码。此密码必须在首次登录时更改。

```
ALTER USER alice SET PASSWORD $password CHANGE NOT REQUIRED
```

为用户设置新密码。该用户在下次登录时无需更改此密码。

```
ALTER USER alice IF EXISTS SET PASSWORD CHANGE REQUIRED
```

如果指定用户存在，则强制该用户在下次登录时更改密码。

```
ALTER USER alice SET STATUS SUSPENDED
```

(★) 将用户状态更改为已暂停。使用 SET STATUS ACTIVE 重新激活用户。

```
ALTER USER alice SET HOME DATABASE otherDb
```

(★) 将用户的主数据库更改为 otherDb。使用 REMOVE HOME DATABASE 取消设置用户的主数据库并回退到默认数据库。

```
ALTER CURRENT USER SET PASSWORD FROM $old TO $new
```

更改已登录用户的密码。该用户在下次登录时无需更改此密码。

```
SHOW CURRENT USER
```

列出当前登录的用户、其状态、角色以及是否需要更改密码。(★) 状态和角色仅限企业版。

```
SHOW USERS
```

列出系统中的所有用户、其状态、角色以及是否需要更改密码。(★) 状态和角色仅限企业版。

```
SHOW USERS
YIELD user, suspended
WHERE suspended = true
```

列出系统中的用户，按其名称和状态筛选，并根据是否已暂停进一步细化。(★) 状态仅限企业版。

```
RENAME USER alice TO alice_delete
```

将用户 alice 重命名为 alice_delete。

```
DROP USER alice_delete
```

删除用户。

### (★) 角色管理

```
CREATE ROLE my_role
```

创建一个角色。

```
CREATE ROLE my_second_role IF NOT EXISTS AS COPY OF my_role
```

创建一个名为 my_second_role 的角色（除非它已存在），作为现有 my_role 的副本。

```
RENAME ROLE my_second_role TO my_other_role
```

将名为 my_second_role 的角色重命名为 my_other_role。

```
GRANT ROLE my_role, my_other_role TO alice
```

向用户分配角色。

```
REVOKE ROLE my_other_role FROM alice
```

从用户中删除指定的角色。

```
SHOW ROLES
```

列出系统中的所有角色。

```
SHOW ROLES
YIELD role
WHERE role CONTAINS 'my'
```

列出角色，按角色名称筛选，并根据名称是否包含 'my' 进一步细化。

```
SHOW POPULATED ROLES WITH USERS
```

列出系统中至少分配给一个用户的所有角色，以及分配给这些角色的用户。

```
DROP ROLE my_role
```

删除一个角色。

### (★) 图读取权限

```
GRANT TRAVERSE ON GRAPH * NODES * TO my_role
```

向角色授予对所有图上所有节点的遍历权限。

```
DENY READ {prop} ON GRAPH foo RELATIONSHIP Type TO my_role
```

拒绝角色对指定图中指定类型的所有关系上的指定属性的读取权限。

```
GRANT MATCH {*} ON HOME GRAPH ELEMENTS Label TO my_role
```

向角色授予对主图中所有属性的读取权限和遍历权限。此处，这两种权限适用于图中具有指定标签/类型的所有节点和关系。

### (★) 图写入权限

```
GRANT CREATE ON GRAPH * NODES Label TO my_role
```

向角色授予在所有图中创建具有指定标签的所有节点的权限。

```
DENY DELETE ON GRAPH neo4j TO my_role
```

拒绝角色对指定图中所有节点和关系的删除权限。

```
REVOKE SET LABEL Label ON GRAPH * FROM my_role
```

从角色中撤销对所有图上指定标签的设置标签权限。

```
GRANT REMOVE LABEL * ON GRAPH foo TO my_role
```

向角色授予对指定图上所有标签的移除标签权限。

```
DENY SET PROPERTY {prop} ON GRAPH foo RELATIONSHIPS Type TO my_role
```

拒绝角色对指定图中指定类型的所有关系上的指定属性的设置属性权限。

```
GRANT MERGE {*} ON GRAPH * NODES Label TO my_role
```

向角色授予对所有图中具有指定标签的所有节点上的所有属性的合并权限。

```
REVOKE WRITE ON GRAPH * FROM my_role
```

从角色中撤销对所有图的写入权限。

```
DENY ALL GRAPH PRIVILEGES ON GRAPH foo TO my_role
```

拒绝角色对指定图的所有图权限。

### (★) SHOW 权限 (SHOW PRIVILEGES)

```
SHOW PRIVILEGES AS COMMANDS
```

以 Cypher 命令形式列出系统中的所有权限。

```
SHOW PRIVILEGES
```

列出系统中的所有权限及其分配到的角色。

```
SHOW PRIVILEGES
YIELD role, action, access
WHERE role = 'my_role'
```

列出有关权限的信息，按角色、操作和访问权限筛选，并根据角色名称进一步细化。

```
SHOW ROLE my_role PRIVILEGES AS COMMANDS
```

以 Cypher 命令形式列出分配给角色的所有权限。

```
SHOW ROLE my_role, my_second_role PRIVILEGES AS COMMANDS
```

以 Cypher 命令形式列出分配给多个角色中每个角色的所有权限。

```
SHOW USER alice PRIVILEGES AS COMMANDS
```

以 Cypher 命令形式列出用户的所有权限及其分配到的角色。

```
SHOW USER PRIVILEGES AS COMMANDS
```

以 Cypher 命令形式列出当前登录用户的所有权限及其分配到的角色。

### (★) 数据库权限

```
GRANT ACCESS ON DATABASE * TO my_role
```

向角色授予访问和对所有数据库运行查询的权限。

```
GRANT START ON DATABASE * TO my_role
```

向角色授予启动所有数据库的权限。

```
GRANT STOP ON DATABASE * TO my_role
```

向角色授予停止所有数据库的权限。

```
GRANT CREATE INDEX ON DATABASE foo TO my_role
```

向角色授予在指定数据库上创建索引的权限。

```
GRANT DROP INDEX ON DATABASE foo TO my_role
```

向角色授予在指定数据库上删除索引的权限。

```
GRANT SHOW INDEX ON DATABASE * TO my_role
```

向角色授予显示所有数据库上索引的权限。

```
DENY INDEX MANAGEMENT ON DATABASE bar TO my_role
```

拒绝角色在指定数据库上创建和删除索引的权限。

```
GRANT CREATE CONSTRAINT ON DATABASE * TO my_role
```

向角色授予在所有数据库上创建约束的权限。

```
DENY DROP CONSTRAINT ON DATABASE * TO my_role
```

拒绝角色在所有数据库上删除约束的权限。

```
DENY SHOW CONSTRAINT ON DATABASE foo TO my_role
```

拒绝角色显示指定数据库上约束的权限。

```
REVOKE CONSTRAINT ON DATABASE * FROM my_role
```

从角色中撤销在所有数据库上创建和删除约束的已授予和已拒绝的权限。

```
GRANT CREATE NEW LABELS ON DATABASE * TO my_role
```

向角色授予在所有数据库上创建新标签的权限。

```
DENY CREATE NEW TYPES ON DATABASE foo TO my_role
```

拒绝角色在指定数据库上创建新关系类型的权限。

```
REVOKE GRANT CREATE NEW PROPERTY NAMES ON DATABASE bar FROM my_role
```

从角色中撤销在指定数据库上创建新属性名称的授予权限。

```
GRANT NAME MANAGEMENT ON HOME DATABASE TO my_role
```

向角色授予在主数据库上创建标签、关系类型和属性名称的权限。

```
GRANT ALL ON DATABASE baz TO my_role
```

向角色授予在指定数据库上访问、创建和删除索引和约束，创建新标签、类型和属性名称的权限。

```
GRANT SHOW TRANSACTION (*) ON DATABASE foo TO my_role
```

向角色授予在指定数据库上列出所有用户的事务和查询的权限。

```
DENY TERMINATE TRANSACTION (user1, user2) ON DATABASES * TO my_role
```

拒绝角色终止所有数据库上来自 user1 和 user2 的事务和查询的权限。

```
REVOKE GRANT TRANSACTION MANAGEMENT ON HOME DATABASE FROM my_role
```

从角色中撤销在主数据库上列出和终止所有用户的事务和查询的已授予权限。

### (★) 角色管理权限

```
GRANT CREATE ROLE ON DBMS TO my_role
```

向角色授予创建角色的权限。

```
GRANT RENAME ROLE ON DBMS TO my_role
```

向角色授予重命名角色的权限。

```
GRANT DROP ROLE ON DBMS TO my_role
```

向角色授予删除角色的权限。

```
DENY ASSIGN ROLE ON DBMS TO my_role
```

拒绝角色向用户分配角色的权限。

```
DENY REMOVE ROLE ON DBMS TO my_role
```

拒绝角色从用户中移除角色的权限。

```
REVOKE DENY SHOW ROLE ON DBMS FROM my_role
```

从角色中撤销显示角色的已拒绝权限。

```
GRANT ROLE MANAGEMENT ON DBMS TO my_role
```

向角色授予管理角色的所有权限。

### (★) 用户管理权限

```
GRANT CREATE USER ON DBMS TO my_role
```

向角色授予创建用户的权限。

```
GRANT RENAME USER ON DBMS TO my_role
```

向角色授予重命名用户的权限。

```
DENY ALTER USER ON DBMS TO my_role
```

拒绝角色更改用户的权限。

```
REVOKE SET PASSWORDS ON DBMS FROM my_role
```

从角色中撤销更改用户密码的已授予和已拒绝的权限。

```
REVOKE GRANT SET USER STATUS ON DBMS FROM my_role
```

从角色中撤销更改用户帐户状态的已授予权限。

```
GRANT SET USER HOME DATABASE ON DBMS TO my_role
```

向角色授予更改用户主数据库的权限。

```
GRANT DROP USER ON DBMS TO my_role
```

向角色授予删除用户的权限。

```
REVOKE DENY SHOW USER ON DBMS FROM my_role
```

从角色中撤销显示用户的已拒绝权限。

```
GRANT USER MANAGEMENT ON DBMS TO my_role
```

向角色授予管理用户的所有权限。

### (★) 数据库管理权限

```
GRANT CREATE DATABASE ON DBMS TO my_role
```

向角色授予创建数据库的权限。

```
REVOKE DENY DROP DATABASE ON DBMS FROM my_role
```

从角色中撤销删除数据库的已拒绝权限。

```
DENY DATABASE MANAGEMENT ON DBMS TO my_role
```

拒绝角色管理数据库的所有权限。

### (★) 权限管理权限

```
GRANT SHOW PRIVILEGE ON DBMS TO my_role
```

向角色授予显示权限的权限。

```
DENY ASSIGN PRIVILEGE ON DBMS TO my_role
```

拒绝角色向角色分配权限的权限。

```
REVOKE GRANT REMOVE PRIVILEGE ON DBMS FROM my_role
```

从角色中撤销从角色移除权限的已授予权限。

```
REVOKE PRIVILEGE MANAGEMENT ON DBMS FROM my_role
```

从角色中撤销管理权限的所有已授予和已拒绝的权限。

### (★) DBMS 权限

```
GRANT ALL ON DBMS TO my_role
```

向角色授予执行所有角色管理、用户管理、数据库管理和权限管理的权限。

## ★ 注意

(★) 功能仅在 Neo4j 企业版中可用。

