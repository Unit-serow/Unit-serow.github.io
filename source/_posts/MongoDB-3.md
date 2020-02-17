---
title: MongoDB-3
date: 2020-02-17 21:43:03
tags: [NoSQL,随笔]
categories: [软件,数据库]
---

### MongoDB-3

**使用数据模型:**

* 集合SET1
> `db.createCollection("SET1", { capped : true, autoIndexId : true, size : 6142800, max : 10000} )`

```
db.SET1.insert({ A: "A1", B: "A2", likes: 100});
db.SET1.insert({ A: "A1", B: "A2", likes: 110});
db.SET1.insert({ A: "B1", B: "B2", likes: 120});
db.SET1.insert({ A: "B1", B: "B2", likes: 130});
db.SET1.insert({ A: "D1", B: "D2", likes: 140});
db.SET1.insert({ A: "D1", B: "D2", likes: 150});
db.SET1.insert({ A: "E1", B: "E2", likes: 160});
db.SET1.insert({ A: "E1", B: "E2", likes: 170});
db.SET1.insert({ A: "F1", B: "F2", likes: 180});
db.SET1.insert({ A: "F1", B: "F2", likes: 190});
```

```
> db.createCollection("SET1", { capped : true, autoIndexId : true, size : 6142800, max : 10000} )
{
	"note" : "the autoIndexId option is deprecated and will be removed in a future release",
	"ok" : 1
}
```

```
> db.SET1.insert({ A: "A1", B: "A2", likes: 100});
WriteResult({ "nInserted" : 1 })
```
```
> db.SET1.insert({ A: "A1", B: "A2", likes: 110});
WriteResult({ "nInserted" : 1 })
```
```
> db.SET1.insert({ A: "B1", B: "B2", likes: 120});
WriteResult({ "nInserted" : 1 })
```
```
> db.SET1.insert({ A: "B1", B: "B2", likes: 130});
WriteResult({ "nInserted" : 1 })
```
```
> db.SET1.insert({ A: "D1", B: "D2", likes: 140});
WriteResult({ "nInserted" : 1 })
```
```
> db.SET1.insert({ A: "D1", B: "D2", likes: 150});
WriteResult({ "nInserted" : 1 })
```
```
> db.SET1.insert({ A: "E1", B: "E2", likes: 160});
WriteResult({ "nInserted" : 1 })
```
```
> db.SET1.insert({ A: "E1", B: "E2", likes: 170});
WriteResult({ "nInserted" : 1 })
```
```
> db.SET1.insert({ A: "F1", B: "F2", likes: 180});
WriteResult({ "nInserted" : 1 })
```
```
> db.SET1.insert({ A: "F1", B: "F2", likes: 190});
WriteResult({ "nInserted" : 1 })
```

```
> db.SET1.find()
{ "_id" : ObjectId("5e4a854d97967282a0f02973"), "A" : "A1", "B" : "A2", "likes" : 100 }
{ "_id" : ObjectId("5e4a854d97967282a0f02974"), "A" : "A1", "B" : "A2", "likes" : 110 }
{ "_id" : ObjectId("5e4a854d97967282a0f02975"), "A" : "B1", "B" : "B2", "likes" : 120 }
{ "_id" : ObjectId("5e4a854d97967282a0f02976"), "A" : "B1", "B" : "B2", "likes" : 130 }
{ "_id" : ObjectId("5e4a854d97967282a0f02977"), "A" : "D1", "B" : "D2", "likes" : 140 }
{ "_id" : ObjectId("5e4a854d97967282a0f02978"), "A" : "D1", "B" : "D2", "likes" : 150 }
{ "_id" : ObjectId("5e4a854d97967282a0f02979"), "A" : "E1", "B" : "E2", "likes" : 160 }
{ "_id" : ObjectId("5e4a854d97967282a0f0297a"), "A" : "E1", "B" : "E2", "likes" : 170 }
{ "_id" : ObjectId("5e4a854d97967282a0f0297b"), "A" : "F1", "B" : "F2", "likes" : 180 }
{ "_id" : ObjectId("5e4a854e97967282a0f0297c"), "A" : "F1", "B" : "F2", "likes" : 190 }
```

---

**开始查询:**

* 查询并输出A=A1和B=A2的键值
> `db.SET1.find({"A" : "A1", "B" : "A2"})`

```
> db.SET1.find({"A" : "A1", "B" : "A2"})
{ "_id" : ObjectId("5e4a854d97967282a0f02973"), "A" : "A1", "B" : "A2", "likes" : 100 }
{ "_id" : ObjectId("5e4a854d97967282a0f02974"), "A" : "A1", "B" : "A2", "likes" : 110 }
```

---

* 查询并输出集合SET1内likes大于100且小于200的键值，跳过前两条并且只输出四条
> `db.SET1.find({likes : {$lt :200, $gt : 100}}).limit(4).skip(2)`

```
> db.SET1.find({likes : {$lt :200, $gt : 100}}).limit(4).skip(2)
{ "_id" : ObjectId("5e4a854d97967282a0f02976"), "A" : "B1", "B" : "B2", "likes" : 130 }
{ "_id" : ObjectId("5e4a854d97967282a0f02977"), "A" : "D1", "B" : "D2", "likes" : 140 }
{ "_id" : ObjectId("5e4a854d97967282a0f02978"), "A" : "D1", "B" : "D2", "likes" : 150 }
{ "_id" : ObjectId("5e4a854d97967282a0f02979"), "A" : "E1", "B" : "E2", "likes" : 160 }
```

---

* 查询并降序输出集合SET1内A等于A1或等于B1或等于D1的数据
> `db.SET1.find({$or:[{"A": "A1"},{"A": "B1"},{"A": "D1"}]}).sort({"likes":-1})`

```
> db.SET1.find({$or:[{"A": "A1"},{"A": "B1"},{"A": "D1"}]}).sort({"likes":-1})
{ "_id" : ObjectId("5e4a854d97967282a0f02978"), "A" : "D1", "B" : "D2", "likes" : 150 }
{ "_id" : ObjectId("5e4a854d97967282a0f02977"), "A" : "D1", "B" : "D2", "likes" : 140 }
{ "_id" : ObjectId("5e4a854d97967282a0f02976"), "A" : "B1", "B" : "B2", "likes" : 130 }
{ "_id" : ObjectId("5e4a854d97967282a0f02975"), "A" : "B1", "B" : "B2", "likes" : 120 }
{ "_id" : ObjectId("5e4a854d97967282a0f02974"), "A" : "A1", "B" : "A2", "likes" : 110 }
{ "_id" : ObjectId("5e4a854d97967282a0f02973"), "A" : "A1", "B" : "A2", "likes" : 100 }
```

---

* 查询并输出集合SET1内A等于A1或等于B1，且likes值小于并等于50的值
>`db.SET1.find({"likes": {$gt:50}, $or: [{"A" : "A1"},{"A" : "B1"}]})`

```
> db.SET1.find({"likes": {$gt:50}, $or: [{"A" : "A1"},{"A" : "B1"}]})
{ `"_id"` : ObjectId("5e4a854d97967282a0f02973"), "A" : "A1", "B" : "A2", "likes" : 100 }
{ `"_id"` : ObjectId("5e4a854d97967282a0f02974"), "A" : "A1", "B" : "A2", "likes" : 110 }
{ `"_id"` : ObjectId("5e4a854d97967282a0f02975"), "A" : "B1", "B" : "B2", "likes" : 120 }
{ `"_id"` : ObjectId("5e4a854d97967282a0f02976"), "A" : "B1", "B" : "B2", "likes" : 130 }
```

* 执行逻辑(顺序)
> 先执行sort(), 然后执行skip()，最后执行limit()
> 相当于`like >=50 AND (where A='A1' OR A='B1')`
> `where likes [条件运算符] [条件] AND (key=>value OR key=>value)`

---

* 以降序查询并输出集合SET1内文本A的内容
> `db.SET1.find({},{"A":1, _id:0}).sort({"likes":-1})`

```
> `db.SET1.find({},{"A":1, _id:0}).sort({"likes":-1})`
{ "A" : "F1" }
{ "A" : "F1" }
{ "A" : "E1" }
{ "A" : "E1" }
{ "A" : "D1" }
{ "A" : "D1" }
{ "A" : "B1" }
{ "A" : "B1" }
{ "A" : "A1" }
{ "A" : "A1" }
```

---

* 输出SET1内G列内的所有文本数据，输出量为三，偏移量为一
> `db.SET1.find({"A" : {$type : 'string'}}).limit(3).skip(1)`

```
> db.SET1.find({"A" : {$type : 'string'}}).limit(3).skip(1)
{ `"_id"` : ObjectId("5e4a854d97967282a0f02974"), "A" : "A1", "B" : "A2", "likes" : 110 }
{ `"_id"` : ObjectId("5e4a854d97967282a0f02975"), "A" : "B1", "B" : "B2", "likes" : 120 }
{ `"_id"` : ObjectId("5e4a854d97967282a0f02976"), "A" : "B1", "B" : "B2", "likes" : 130 }
```

> string可以用2表示，Array用4

---

* 在SET2内基于ID求出的文档A1的数据总和，并进行分组
> `db.SET1.aggregate([{$group : {`_id` : "A1", amount : {$sum : 1}}}])`

```
> db.SET1.aggregate([{$group : {`_id` : "A1", amount : {$sum : 1}}}])
{ `"_id"` : "A1", "amount" : 10 }
```

> 类似于RDBMS中的SQL语句:`Sselect A1, count(*) from SET2 group by _id`

---

* 类似概念
> 逗号'","`即为`AND`
> `$or`即为`OR`

---

* 操作符
> 用于比较两个表达式并从mongoDB集合中获取数据

**操作符总览**

|全称|符号说明|操作符|
|:----|:----|:----|
|greater than|">"(大于)|$gt|
|less than|"<"(小于)|$lt|
|gt equal|">="(大于等于)|$gte|
|lt equal|"<="(小于等于)|$lte|
|not equal|"!="(不等于)|$ne|
|equal|"="(等于)|$eq|

---

**相关概念**
* 条件操作符
* `projection`
* `$type`
* `limit`
* `skip`
* 排序(`sort({KEY:1/-1})`)
* 聚合(aggregate)
* 复制(副本集)
* 分片(集群)
* 序列(自增)

* 查询语法基本结构
> `db.collection.find((query, projection)`
> `db.collection.find({key1:value1, key2:value2}).pretty()`

---

**MongoDB与RDBMS Where语句比较**

**查询语句:**

|操作|格式|范例|RDBMS中的类似语句|
|:----|:----|:----|:----|
|等于|{<key>:<value>}|db.col.find({"A":"xxx"}).pretty()|where A = 'xxx'|
|小于|{<key>:{$lt:<value>}}|db.col.find({"likes":{$lt:50}}).pretty()|where likes < 50|
|小于或等于|{<key>:{$lte:<value>}}|db.col.find({"likes":{$lte:50}}).pretty()|where likes <= 50|
|大于|{<key>:{$gt:<value>}}|db.col.find({"likes":{$gt:50}}).pretty()|where likes > 50|
|大于或等于|{<key>:{$gte:<value>}}|db.col.find({"likes":{$gte:50}}).pretty()|where likes >= 50|
|不等于|{<key>:{$ne:<value>}}|db.col.find({"likes":{$ne:50}}).pretty()|where likes != 50|

---
