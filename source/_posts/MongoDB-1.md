---
title: MongoDB-1
date: 2020-02-17 17:08:31
tags: [NoSQL,随笔]
categories: [软件,数据库]
---

### MongoDB-1

**概述:**

* NoSQL
* 是一个基于分布式文件存储的数据库
* 由C++撰写
* 目的是为WEB应用提供可扩展的高性能数据存储解决方案
* 虽然是非关系型，但它的功能超越了所有其他的NoSQL，是最接近关系型数据库的NoSQL
* MongoDB 将数据存储为一个文档，数据结构由键值`(key=>value)`对组成
* MongoDB 文档类似于JSON对象
* 字段值可以包含其他文档，数组及文档数组
* 2007年10月，MongoDB由10gen团队所开发，发布于2009年2月

---

**(Key=>Value)简述:**

```
{
   name: "serow"	<-field: value
   time: "2020-01-17"	<-field: value
   xxx: "xxx"		<-field: value
}
```

---

**存储结构示例**

**向数据库内UNIT1集合插入两条文档数据**

`db.UNIT1.insert({[A: '1', '2', '3'], [B: '1', '2', '3'] likes: 100)});`

```
> db.UNIT1.insert({
... A: ['1', '2', '3'],
... B: ['1', '2', '3'],
... likes: 100});
WriteResult({ "nInserted" : 1 })
```

```
> db.UNIT1.insert({ A: ['1', '2', '3'], B: ['1', '2', '3'], likes: 100});
WriteResult({ "nInserted" : 1 })
```

---

**输出示例(结构示例):**

`db.UNIT1.find()`

```
> db.UNIT1.find()
{ "_id" : ObjectId("5e4a564937144332c7b7814a"), "A" : [ "1", "2", "3" ], "B" : [ "1", "2", "3" ], "likes" : 100 }
{ "_id" : ObjectId("5e4a569837144332c7b7814b"), "A" : [ "1", "2", "3" ], "B" : [ "1", "2", "3" ], "likes" : 100 }
```

---

**特点:**

1. MongoDB是一个面向文档存储的数据库，因此降低了管理与操作的难度
2. Mongo支持丰富的查询表达式，而查询指令使用JSON形式的标记，可轻易查询文档中内嵌的对象及数组
3. 允许在MongoDB记录中设置任何属性的索引来实现更快的排序
4. 允许通过本地或者网络创建数据镜像，以此大幅增加了MongoDB的扩展性
---
5. MongoDB使用update()命令可以实现替换完成的文档(数据)或者一些指定的数据字段
6. MongoDB中的Map/reduce主要是用来对数据进行批量处理和聚合操作
7. Map和Reduce:Map函数调用emit(key,value)遍历集合中所有的记录，将key与value传给Reduce函数进行处理
8. Map函数和Reduce函数是使用Javascript编写的，并可以通过db.runCommand或mapreduce命令来执行MapReduce操作
9. MongoDB允许在服务端执行脚本用Javascript编写某个函数，然后直接在服务端执行，函数的定义可以存储在服务端，以方便下次调用
---
10. MongoDB拥有各种API用以支持各类编程语言:PHP,Lisp,Puby,C++,Scala,Python等
11. 在负载增加时(需要更多的存储空间和更强的处理能力)，它可以分布在计算机网络中的其他节点上，即为分片

---

**内置工具**

* MongoDB中的内置功能(插件)
> MongoDB提供了网络和系统监控工具Munin，作为插件应用于MongoDB中
> Gangila是MongoDB高性能的系统监视的工具，还可以可以用于存放大量小文件，作为插件应用于MongoDB中
> 基于图形界面的开源工具之一:Cacti，用于查看CPU负载，网络带宽利用率，同时提供了一个应用于监控MongoDB的插件

---

**GUI工具一览**

|名称|说明|
|:----|:----|
|Fang of Mongo|网页式，由Django和jQuery撰写|
|Futon4Mongo|一个CouchDB Futon web的MongoDB山寨版|
|Mongo3|由Ruby撰写|
|Opricot|一个基于浏览器的MongoDB控制台, 由PHP撰写|
|RockMongo|MongoDB管理工具，轻量级且支持多国语言，由PHP撰写|
|MongoHub|适用于OSX的应用程序|
|Database Master|Windows的mongodb管理工具|

---

**基本概念简述:**

* 在mongodb中基本的概念:
* 数据库
* 文档
* 集合
* 键
* 值(域)

|MongoDB术语与概念|SQL术语与通用概念|解释与说明|
|:----|:----|:----|
|database|database|数据库|
|collection|table|集合/数据库表|
|document|row|文档/数据行|
|field|column|域/数据字段|
|index|index|索引|
|primary key|primary key|主键,MongoDB自动将`_id`字段设置为主键|
|table joins|---|MongoDB不支持表连接|

---

**概念解析**

1. 数据库(Database)
* MongoDB的默认数据库为'db'，该数据库被存储于data目录内
* MongoDB的单个实例可以容纳多个独立的数据库，每个实例都有独立的集合与权限
* 不同的数据库被放置于data目录内不同的文件中

**基本命令:**

* 以列表方式输出已存在数据库信息
> `show dbs`
* 显示当前数据库对象或集合
> `db`
* 连接所选数据库，命名的具体规则不进行过多说明
> `use database_name`

**MongoDB内拥有特定作用的保留数据库，可直接访问**

**具体说明:**

> `admin`:操作权限管理数据库，添加于此数据库的用户会自动继承数据库的所有操作权限，即为root权限
> 一些特定的服务器端命令也只能从这个数据库运行，例如列出所有的数据库或者关闭服务器
> `local`:此数据库内的数据不可复制，可以用来存储限于本地单台服务器的任意集合
> `config`:当Mongo用于分片设置时，config数据库在内部使用，用于保存分片的相关信息

* 关于数据库的具体命令本章不做阐述

---

2. 文档(Document)

1. 文档是一组键值(key-value)对(即BSON)
2. MongoDB的文档不需要设置相同的字段，并且相同的字段不需要相同的数据类型，这是MongoDB完全不同于关系型数据库的一个特点
3. 文档中的键/值对是有序的
4. 文档中的值不仅可以是在双引号里面的字符串，还可以是其他几种数据类型(并且允许嵌入整个文档)
5. MongoDB区分类型和大小写
6. MongoDB的文档不能有重复的键
7. 文档的键是字符串，除了少数例外情况，键可以使用任意UTF-8字符

**文档键命名规范:**

1. 键不能含有\0 (空字符)。这个字符用来表示键的结尾
2. `.`和`$`有特别的意义，只有在特定环境下才能使用
3. 以下划线`"_"`开头的键是保留的(不是严格要求的)

* 文档示例:
> `{"set":"unit","serow":"takin"}`

**RDBMS与MongoDB对应的术语:**


|RDBMS|MongoDB|
|:----|:----|
|数据库|数据库|
|表格|集合|
|行|文档|
|列|字段|
|表联合|嵌入文档|
|主键|主键(MongoDB提供了key为`_id`)|


**数据库和客户端:**

|数据库|客户端|
|:----|:----|
|mongo|mongod|
|Mysqld|mysql|
|Oracle|sqlplus|

---

3. 集合(collections)
* 集合是MongoDB文档组，类似于RDBMS[^1]中的表格
* 集合存在于数据库中，集合没有固定的结构
* 所以集合中可以插入不同格式和类型的数据，但通常情况下插入集合中的数据都会有一定的关联性
* 当第一个文档插入时，集合就会被创建

* 集合示例:
```
{"set":"group"}
{"unit":"communism","free":"rule"}
{"takin":"serow","elk":"crocodile","elephant"}
```

**集合的命名规则:**
* 集合名不能是空字符串`""`
* 集合名不能含有\0字符(空字符)，此字符表示集合名的结尾
* 集合名不能以"system."开头，这是为系统集合保留的前缀
* 集合名字不能含有保留字符
> 但某些驱动程序可以支持在集合名内包含保留字符，因为某些系统生成的集合中包含该字符
> 除非要访问这种系统创建的集合，否则不可以在名字里出现`$`

* 命名实例:
> `db.col.fineOne()`

---

4. 封装集合(Capped collections)

* Capped collections就是固定大小的collection
* 有很高的性能以及队列过期的特性(过期按照插入的顺序)，有点类似于`RRD`的概念
* Capped collections是高性能自动的维护对象的插入顺序
> 适合类似记录日志的功能
> 与标准的collection不同，其需要显式的创建一个capped collection，指定一个collection的大小(单位是字节)
> collection 的数据存储空间值提前分配的
* Capped collections 可以按照文档的插入顺序保存到集合中，而且这些文档在磁盘上存放位置也是按照插入顺序来保存的
> 所以更新Capped collections中文档的时候，更新后的文档不可以超过之前文档的大小，以确保所有文档在磁盘上的位置一直保持不变
* Capped collection是按照文档的插入顺序而不是使用索引确定插入位置，此种方法可以提高增添数据的效率
> MongoDB的操作日志文件`oplog.rs`就是利用Capped Collection来实现的
* 指定的存储大小包含了数据库的头信息，这一点需要特别注意
---
* 在Capped Collection中可以能添加新的对象
* 可以进行更新，并且对象不会增加存储空间，如果增加，更新就会失败
* 使用Capped Collection不能删除一个文档，可以使用drop()方法删除collection所有的行
* 删除之后必须显式的重新创建此collection
* 在32bit机器中，capped collection最大存储为`1e9( 1X10^9)`个字节
---
* Capped Collections示例:
> `db.createCollection("mycoll", {capped:true, size:100000})`

---

5. 元数据
* 数据库的信息存储在集合中，它们使用了系统的命名空间:
> `dbname.system.*`
* 在MongoDB数据库中名字空间`<dbname>.system.*`是包含多种系统信息的特殊集合(Collection)

**集合命名空间说明:**

|集合命名空间|描述|
|:----|:----|
|dbname.system.namespaces|列出所有名字空间|
|dbname.system.indexes|列出所有索引|
|dbname.system.profile|包含数据库概要(profile)信息|
|dbname.system.users|列出所有可访问数据库的用户|
|dbname.local.sources|包含复制对端(slave)的服务器信息和状态|

**对于修改系统集合中的对象有的规则:**

1. 在`"[{system.indexes]}"`插入数据，可以创建索引
>  但除此之外该表信息是不可变的(特殊的drop index命令将自动更新相关信息)
2. `"[{system.users}]"`是可修改的
3. `"[{system.profile}]"`是可删除的

---

**其它概念:**
MongoDB 数据类型
ObjectId
字符串(BSON字符串都是UTF-8编码)
时间戳
日期(`DATE/DATE()`)

---

**参考资料:**

官方网站[跳转](https://www.mongodb.com/)
`https://www.mongodb.com/`

官方文档EN[跳转](https://docs.mongodb.com/manual/)
`https://docs.mongodb.com/manual/`

下载地址[跳转](https://www.mongodb.com/download-center/community)
`https://www.mongodb.com/download-center/community`

---

[^1]:(关系数据库管理系统：Relational Database Management System，RDBMS)
