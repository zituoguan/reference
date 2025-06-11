---
title: MongoDB
date: 2023-04-05
background:
  bg-gradient-to-r from-green-900 via-green-600 to-green-400 hover:from-green-900 hover:via-green-700 hover:to-green-500
tags:
  - NoSQL
  - DB
categories:
  - 数据库
intro:
  MongoDB 速查表为您提供了最常用的 MongoDB 命令和查询以供参考。该速查表来自 MongoDB 开发者网站。
plugins:
  - tooltip
  - copyCode
---

## 入门指南 {.cols-2}

### 连接 MongoDB Shell

```mongosh
mongo # 默认连接到 mongodb://127.0.0.1:27017
```

```mongosh
mongo --host <主机> --port <端口> -u <用户> -p <密码> # 如果希望提示输入密码，则省略密码
```

```mongosh
mongo "mongodb://192.168.1.1:27017"
```

```mongosh
mongo "mongodb+srv://集群名称.abcde.mongodb.net/<数据库名>" --username <用户名> # MongoDB Atlas
```

### 辅助命令

显示数据库 :

```mongosh
db // 打印当前数据库
```

切换数据库 :

```mongosh
use <数据库名>
```

显示集合 :

```mongosh
show collections
```

运行 JavaScript 文件 :

```mongosh
load("myScript.js")
```

---

## 增删改查 (CRUD)

### 创建 (Create)

```mongosh
db.coll.insertOne({name: "Max"})
db.coll.insertMany([{name: "Max"}, {name:"Alex"}]) // 有序批量插入
db.coll.insertMany([{name: "Max"}, {name:"Alex"}], {ordered: false}) // 无序批量插入
db.coll.insertOne({date: ISODate()})
db.coll.insertMany({name: "Max"}, {"writeConcern": {"w": "majority", "wtimeout": 5000}})
```

### 删除 (Delete)

```mongosh
db.coll.deleteOne({name: "Max"})
db.coll.deleteMany( $and: [{name: "Max"}, {justOne: true}]) // 删除包含这两个值的所有条目
db.coll.deleteMany( $or: [{name: "Max"}, {justOne: true}])  // 删除包含任一指定值的所有条目
db.coll.deleteMany({}) // 警告！删除所有文档，但不会删除集合本身及其索引定义
db.coll.deleteMany({name: "Max"}, {"writeConcern": {"w": "majority", "wtimeout": 5000}})
db.coll.findOneAndDelete({"name": "Max"})
```

### 更新 (Update)

```mongosh
db.coll.updateMany({"_id": 1}, {$set: {"year": 2016}}) // 警告！替换 "_id" = 1 的整个文档
db.coll.updateOne({"_id": 1}, {$set: {"year": 2016, name: "Max"}})   
db.coll.updateOne({"_id": 1}, {$unset: {"year": 1}})  
db.coll.updateOne({"_id": 1}, {$rename: {"year": "date"} }) 
db.coll.updateOne({"_id": 1}, {$inc: {"year": 5}}) 
db.coll.updateOne({"_id": 1}, {$mul: {price: 2}})  
db.coll.updateOne({"_id": 1}, {$min: {"imdb": 5}})
db.coll.updateOne({"_id": 1}, {$max: {"imdb": 8}}) 
db.coll.updateMany({"_id": {$lt: 10}}, {$set: {"lastModified": ISODate()}})  
```

### 数组 {.row-span-2}

```mongosh
db.coll.updateOne({"_id": 1}, {$push :{"array": 1}})
db.coll.updateOne({"_id": 1}, {$pull :{"array": 1}})
db.coll.updateOne({"_id": 1}, {$addToSet :{"array": 2}})
db.coll.updateOne({"_id": 1}, {$pop: {"array": 1}})  // 最后一个元素
db.coll.updateOne({"_id": 1}, {$pop: {"array": -1}}) // 第一个元素
db.coll.updateOne({"_id": 1}, {$pullAll: {"array" :[3, 4, 5]}})
db.coll.updateOne({"_id": 1}, {$push: {scores: {$each: [90, 92, 85]}}})
db.coll.updateOne({"_id": 1, "grades": 80}, {$set: {"grades.$": 82}})
db.coll.updateMany({}, {$inc: {"grades.$[]": 10}})
db.coll.updateMany({}, {$set: {"grades.$[element]": 100}}, {arrayFilters: [{"element": {$gte: 100}}]})
```

### 更新多个文档 {.row-span-1}

```mongosh
db.coll.updateMany({"year": 1999}, {$set: {"decade": "90's"}})
```

### 查找并更新一个文档 {.row-span-1}

```mongosh
db.coll.findOneAndUpdate({"name": "Max"}, {$inc: {"points": 5}}, {returnNewDocument: true})
```

### 更新或插入 (Upsert) {.row-span-1}

```mongosh
db.coll.updateOne({"_id": 1}, {$set: {item: "apple"}, $setOnInsert: {defaultQty: 100}}, {upsert: true})
```

### 替换 {.row-span-1}

```mongosh
db.coll.replaceOne({"name": "Max"}, {"firstname": "Maxime", "surname": "Beugnet"})
```

### 写关注 (Write Concern) {.row-span-1}

```mongosh
db.coll.updateMany({}, {$set: {"x": 1}}, {"writeConcern": {"w": "majority", "wtimeout": 5000}})
```

### 查找 (Find) {.row-span-2}

```mongosh
db.coll.findOne() // 返回单个文档
db.coll.find()    // 返回一个游标 - 显示20个结果 - 输入 "it" 显示更多
db.coll.find().pretty()
db.coll.find({name: "Max", age: 32}) // 隐式的逻辑 "AND"
db.coll.find({date: ISODate("2020-09-25T13:57:17.180Z")})
db.coll.find({name: "Max", age: 32}).explain("executionStats") // 或 "queryPlanner" 或 "allPlansExecution"
db.coll.distinct("name")
```

### 计数 (Count)

```mongosh
db.coll.estimatedDocumentCount()  // 基于集合元数据的估算
db.coll.countDocuments({age: 32}) // 聚合管道的别名 - 精确计数
```

### 比较运算符

```mongosh
db.coll.find({"year": {$gt: 1970}})
db.coll.find({"year": {$gte: 1970}})
db.coll.find({"year": {$lt: 1970}})
db.coll.find({"year": {$lte: 1970}})
db.coll.find({"year": {$ne: 1970}})
db.coll.find({"year": {$in: [1958, 1959]}})
db.coll.find({"year": {$nin: [1958, 1959]}})
```

### 逻辑运算符

```mongosh
db.coll.find({name:{$not: {$eq: "Max"}}})
db.coll.find({$or: [{"year" : 1958}, {"year" : 1959}]})
db.coll.find({$nor: [{price: 1.99}, {sale: true}]})
db.coll.find({
$and: [
    {$or: [{qty: {$lt :10}}, {qty :{$gt: 50}}]},
{$or: [{sale: true}, {price: {$lt: 5 }}]}
]
})
```

### 元素运算符

```mongosh
db.coll.find({name: {$exists: true}})
db.coll.find({"zipCode": {$type: 2 }})
db.coll.find({"zipCode": {$type: "string"}})
```

### 聚合管道

```mongosh
db.coll.aggregate([
{$match: {status: "A"}},
{$group: {_id: "$cust_id", total: {$sum: "$amount"}}},
{$sort: {total: -1}}
])
```

### 使用 "text" 索引进行文本搜索

```mongosh
db.coll.find({$text: {$search: "cake"}}, {score: {$meta: "textScore"}}).sort({score: {$meta: "textScore"}})
```

### 正则表达式

```mongosh
db.coll.find({name: /^Max/}) // 正则表达式：以字母 "M" 开头
db.coll.find({name: /^Max$/i}) // 正则表达式不区分大小写
```

### 数组查询

```mongosh
db.coll.find({tags: {$all: ["Realm", "Charts"]}})
db.coll.find({field: {$size: 2}}) // 无法索引 - 最好存储数组大小并更新它
db.coll.find({results: {$elemMatch: {product: "xyz", score: {$gte: 8}}}})
```

### 投影 (Projections)

```mongosh
db.coll.find({"x": 1}, {"actors": 1}) // actors + _id
db.coll.find({"x": 1}, {"actors": 1, "_id": 0}) // actors
db.coll.find({"x": 1}, {"actors": 0, "summary": 0}) // 除 "actors" 和 "summary" 外的所有字段
```

### 排序、跳过、限制

```mongosh
db.coll.find({}).sort({"year": 1, "rating": -1}).skip(10).limit(3)
```

### 读关注 (Read Concern)

```mongosh
db.coll.find().readConcern("majority")
```

## 数据库和集合 {.cols-2}

### 删除 {.row-span-1}

```mongosh
db.coll.drop()    // 删除集合及其索引定义
db.dropDatabase() // 仔细检查您当前是否*不在*生产集群上... :-) 
```

### 创建集合 {.row-span-2}

```mongosh
db.createCollection("contacts", {
   validator: {$jsonSchema: {
      bsonType: "object",
      required: ["phone"],
      properties: {
         phone: {
            bsonType: "string",
            description: "必须是字符串且为必填项"
         },
         email: {
            bsonType: "string",
            pattern: "@mongodb\.com$",
            description: "必须是字符串并匹配正则表达式模式"
         },
         status: {
            enum: [ "Unknown", "Incomplete" ],
            description: "只能是枚举值之一"
         }
      }
   }}
})
```

### 其他集合函数 {.row-span-1}

```mongosh
db.coll.stats()
db.coll.storageSize()
db.coll.totalIndexSize()
db.coll.totalSize()
db.coll.validate({full: true})
db.coll.renameCollection("new_coll", true) // 第二个参数表示如果目标集合存在则删除它
```

## 索引 {.cols-2}

### 基础操作

#### 列出索引

```mongosh
db.coll.getIndexes()
db.coll.getIndexKeys()
```

#### 删除索引

```mongosh
db.coll.dropIndex("name_1")
```

#### 隐藏/取消隐藏索引

```mongosh
db.coll.hideIndex("name_1")
db.coll.unhideIndex("name_1")
```

### 创建索引

```mongosh
// 索引类型
db.coll.createIndex({"name": 1})                // 单字段索引
db.coll.createIndex({"name": 1, "date": 1})     // 复合索引
db.coll.createIndex({foo: "text", bar: "text"}) // 文本索引
db.coll.createIndex({"$**": "text"})            // 通配符文本索引
db.coll.createIndex({"userMetadata.$**": 1})    // 通配符索引
db.coll.createIndex({"loc": "2d"})              // 2D 索引
db.coll.createIndex({"loc": "2dsphere"})        // 2dsphere 索引
db.coll.createIndex({"_id": "hashed"})          // 哈希索引

// 索引选项
db.coll.createIndex({"lastModifiedDate": 1}, {expireAfterSeconds: 3600})      // TTL 索引
db.coll.createIndex({"name": 1}, {unique: true})
db.coll.createIndex({"name": 1}, {partialFilterExpression: {age: {$gt: 18}}}) // 部分索引
db.coll.createIndex({"name": 1}, {collation: {locale: 'en', strength: 1}})    // 不区分大小写的索引，strength = 1 或 2
db.coll.createIndex({"name": 1 }, {sparse: true})
```

## 其他命令 {.cols-2}

### 常用命令 {.row-span-3}

```mongosh
use admin
db.createUser({"user": "root", "pwd": passwordPrompt(), "roles": ["root"]})
db.dropUser("root")
db.auth( "user", passwordPrompt() )

use test
db.getSiblingDB("dbname")
db.currentOp()
db.killOp(123) // 操作ID (opid)

db.fsyncLock()
db.fsyncUnlock()

db.getCollectionNames()
db.getCollectionInfos()
db.printCollectionStats()
db.stats()

db.getReplicationInfo()
db.printReplicationInfo()
db.isMaster()
db.hostInfo()
db.printShardingStatus()
db.shutdownServer()
db.serverStatus()

db.setSlaveOk()
db.getSlaveOk()

db.getProfilingLevel()
db.getProfilingStatus()
db.setProfilingLevel(1, 200) // 0 == 关闭, 1 == 开启 (记录慢查询), 2 == 开启 (记录所有操作)

db.enableFreeMonitoring()
db.disableFreeMonitoring()
db.getFreeMonitoringStatus()

db.createView("viewName", "sourceColl", [{$project:{department: 1}}])
```

### 副本集 {.row-span-2}

```mongosh
rs.status()
rs.initiate({"_id": "replicaTest",
  members: [
    { _id: 0, host: "127.0.0.1:27017" },
    { _id: 1, host: "127.0.0.1:27018" },
    { _id: 2, host: "127.0.0.1:27019", arbiterOnly:true }]
})
rs.add("mongodbd1.example.net:27017")
rs.addArb("mongodbd2.example.net:27017")
rs.remove("mongodbd1.example.net:27017")
rs.conf()
rs.isMaster()
rs.printReplicationInfo()
rs.printSlaveReplicationInfo()
rs.reconfig(<valid_conf>)
rs.slaveOk()
rs.stepDown(20, 5) // (降级等待秒数, 从节点追赶数据周期秒数)
```

### 分片集群 {.row-span-2}

```mongosh
sh.status()
sh.addShard("rs1/mongodbd1.example.net:27017")
sh.shardCollection("mydb.coll", {zipcode: 1})

sh.moveChunk("mydb.coll", { zipcode: "53187" }, "shard0019")
sh.splitAt("mydb.coll", {x: 70})
sh.splitFind("mydb.coll", {x: 70})
sh.disableAutoSplit()
sh.enableAutoSplit()

sh.startBalancer()
sh.stopBalancer()
sh.disableBalancing("mydb.coll")
sh.enableBalancing("mydb.coll")
sh.getBalancerState()
sh.setBalancerState(true/false)
sh.isBalancerRunning()

sh.addTagRange("mydb.coll", {state: "NY", zip: MinKey }, { state: "NY", zip: MaxKey }, "NY")
sh.removeTagRange("mydb.coll", {state: "NY", zip: MinKey }, { state: "NY", zip: MaxKey }, "NY")
sh.addShardTag("shard0000", "NYC")
sh.removeShardTag("shard0000", "NYC")

sh.addShardToZone("shard0000", "JFK")
sh.removeShardFromZone("shard0000", "NYC")
sh.removeRangeFromZone("mydb.coll", {a: 1, b: 1}, {a: 10, b: 10})
```

### 变更流 (Change Streams) {.row-span-1}

```mongosh
watchCursor = db.coll.watch( [ { $match : {"operationType" : "insert" } } ] )

while (!watchCursor.isExhausted()){
   if (watchCursor.hasNext()){
      print(tojson(watchCursor.next()));
   }
}
```
