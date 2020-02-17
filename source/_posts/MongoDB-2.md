---
title: MongoDB-2
date: 2020-02-17 18:08:48
tags: [NoSQL,随笔]
categories: [软件,数据库]
---

### MongoSQL-2

**创建并连接**

* 创建并选择数据库
> `use TEST1`

```
> use TEST1
switched to db TEST1
```

* 创建集合
> `db.createCollection("SET1", { capped : true, autoIndexId : true, size : 6142800, max : 10000} )`

```
> db.createCollection("SET1", { capped : true, autoIndexId : true, size : 6142800, max : 10000} )
{
	"note" : "the autoIndexId option is deprecated and will be removed in a future release",
	"ok" : 1
}
```

---

**向集合内插入两个文档**

* 定义变量:
```
A1=({
A: ['1', '2', '3'],
B: ['1', '2', '3'],
C: ['1', '2', '3'],
D: ['1', '2', '3'],
E: ['1', '2', '4'],
likes: 100});
```

`A1=({ A: ['1', '2', '3'], B: ['1', '2', '3'], C: ['1', '2', '3'], D: ['1', '2', '3'], E: ['1', '2', '4'], likes: 100});`

```
> A1=({
... A: ['1', '2', '3'],
... B: ['1', '2', '3'],
... C: ['1', '2', '3'],
... D: ['1', '2', '3'],
... E: ['1', '2', '4'],
... likes: 100});
{
	"A" : [
		"1",
		"2",
		"3"
	],
	"B" : [
		"1",
		"2",
		"3"
	],
	"C" : [
		"1",
		"2",
		"3"
	],
	"D" : [
		"1",
		"2",
		"3"
	],
	"E" : [
		"1",
		"2",
		"4"
	],
	"likes" : 100
}
```

* 插入文档
```
db.SET1.insert(A1)
db.SET1.insert(A1)
```

```
> db.SET1.insert(A1)
WriteResult({ "nInserted" : 1 })
> db.SET1.insert(A1)
WriteResult({ "nInserted" : 1 })
```

`db.SET1.find()`

```
> db.SET1.find()
{ "_id" : ObjectId("5e4a614f39d6dc440c77623b"), "A" : [ "1", "2", "3" ], "B" : [ "1", "2", "3" ], "C" : [ "1", "2", "3" ], "D" : [ "1", "2", "3" ], "E" : [ "1", "2", "4" ], "likes" : 100 }
{ "_id" : ObjectId("5e4a615439d6dc440c77623c"), "A" : [ "1", "2", "3" ], "B" : [ "1", "2", "3" ], "C" : [ "1", "2", "3" ], "D" : [ "1", "2", "3" ], "E" : [ "1", "2", "4" ], "likes" : 100 }
```

---

* 更新数据
> `db.SET1.updateMany({'E': ['1' , '2', '4']}, {$set:{'E': ['1', '2', '3']}},{multi:true})`

```
> db.SET1.updateMany({'E': ['1' , '2', '4']}, {$set:{'E': ['1', '2', '3']}},{multi:true})
{ "acknowledged" : true, "matchedCount" : 2, "modifiedCount" : 2 }
```

* 查看集合内容
> `db.SET1.find().pretty()`

```
> db.SET1.find()
{ "_id" : ObjectId("5e4a614f39d6dc440c77623b"), "A" : [ "1", "2", "3" ], "B" : [ "1", "2", "3" ], "C" : [ "1", "2", "3" ], "D" : [ "1", "2", "3" ], "E" : [ "1", "2", "3" ], "likes" : 100 }
{ "_id" : ObjectId("5e4a615439d6dc440c77623c"), "A" : [ "1", "2", "3" ], "B" : [ "1", "2", "3" ], "C" : [ "1", "2", "3" ], "D" : [ "1", "2", "3" ], "E" : [ "1", "2", "3" ], "likes" : 100 }
```

* 查看数据库
> `db`

```
> db
TEST1
```

* 查看所有数据库
> `show dbs`

```
> show dbs
TEST1   0.000GB
admin   0.000GB
config  0.000GB
local   0.000GB
```

---

**创建索引**

* 因为索引不能用于并行数组
* 所以这里新建了一个文档并进行字符串插入

```
db.createCollection("SET2", { capped : true, autoIndexId : true, size : 6142800, max : 10000} )
db.SET2.insert({ A: "A1", B: "A2", likes: 100});
db.SET2.insert({ A: "A1", B: "A2", likes: 100});
```

```
> db.createCollection("SET2", { capped : true, autoIndexId : true, size : 6142800, max : 10000} )
{
	"note" : "the autoIndexId option is deprecated and will be removed in a future release",
	"ok" : 1
}
```

```
> db.SET2.insert({ A: "A1", B: "A2", likes: 100});
WriteResult({ "nInserted" : 1 })
```

```
> db.SET2.insert({ A: "A1", B: "A2", likes: 100});
WriteResult({ "nInserted" : 1 })
```

* 将文档SET2内的键A和键分别设置为升序索引与降序索引(DRBMS内称之为复合索引)
> `db.SET2.createIndex({"A":1,"B":-1})`

```
> db.SET2.createIndex({"A":1,"B":-1})
{
	"createdCollectionAutomatically" : false,
	"numIndexesBefore" : 1,
	"numIndexesAfter" : 2,
	"ok" : 1
```

---

* 查看所有索引
> `db.SET2.getIndexes()`

```
> db.SET2.getIndexes()
[
	{
		"v" : 2,
		"key" : {
			"_id" : 1
		},
		"name" : "_id_",
		"ns" : "A.SET2"
	},
	{
		"v" : 2,
		"key" : {
			"A" : 1,
			"B" : -1
		},
		"name" : "A_1_B_-1",
		"ns" : "A.SET2"
	}
]
```

---

* 删除所有索引
> `db.SET2.dropIndexes()`

```
> db.SET2.dropIndexes()
{
	"nIndexesWas" : 2,
	"msg" : "non-_id indexes dropped for collection",
	"ok" : 1
}
```

---

* 删除集合SET1内所有符合条件的文档
> `db.SET1.deleteMany({A: ['1', '2', '3']})`
> `db.SET1.remove({'A':['1', '2', '3']})`

* 查看集合内容
> `db.SET1.find().pretty()`

* 删除集合
> `db.SET1.drop()`

```
> db.SET1.drop()
true
```

* 删除所在数据库
> `db.dropDatabase()`

```
> db.dropDatabase()
{ "dropped" : "TEST1", "ok" : 1 }
```

* 查看已有数据库列表
> `show dbs`

```
> show dbs
admin   0.000GB
config  0.000GB
local   0.000GB
```

---

**补充内容:**

* 文档的数据结构和JOSN基本相同
* 所有存储在集合中的数据都是BSON格式
* BSON 是一种类似 JSON 的二进制形式的存储格式，是 Binary JSON 的简称
* 增删改查中只有查和改有实际用途，而精髓就在于查

---

**其它概念:**

* 数组
* 变量
* 数据库
* 集合
* 文档
* 键
* 值
* 索引(1/-1)
> `createIndex()` version>3.0.0
> `ensureIndex()` version<3.0.0

---
