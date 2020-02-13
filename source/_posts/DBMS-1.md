---
title: DBMS-1
date: 2020-02-12 14:27:10
tags: 随笔
categories: [软件,数据库]
---

### DBMS-1

**概述:**
* 本篇注重对知识体系的规划与系别的整理
* 别称:数据库管理系统(Database Management System)
* 简称:DBMS
* 一个数据库由多个表空间(Tablespace)构成
* 用于将数据以一定方式存储到同一个数据库内，能同时予以多个用户共享
* 让应用程序的数据集合彼此独立，并且具有尽可能小的冗余度
* 数据库管理系统指的是为管理数据库而设计的电脑软件(程序)系统
* 大多数具有存储，截取，安全保证，备份等基础功能
* 几乎所有的数据库管理系统都配备了一个开放式数据库连接（ODBC）驱动程序，令各个数据库之间得以互相集成
* 不涉及结构化查询语言/数据查询语言(SQL)相关内容

---

* 数据库的类别一览

|类别|相关(与其相结合)|
|:----|:----|
|分布式数据库|分布处理技术|
|并行数据库 |并行处理技术|
|演绎数据库|人工智能|
|多媒体数据库|多媒体技术|
|特定领域数据库|统计/空间/工程/地理数据库等等|
|关系型数据库|MySQL,Oracle,postgreSQL等|
|非关系型数据库|NoSQL/Redis,MongoDB等|

---

* 关系型数据库简介
> MySQL
> MariaDB (MySQL的代替品)
> Percona Server (MySQL的代替品)
> PostgreSQL
> Microsoft Access
> Microsoft SQL Server
> Google Fusion Tables
> FileMaker
> Oracle数据库
> Sybase
> dBASE
> Clipper
> FoxPro
> foshub

---

* 非关系型数据库(NoSQL)简介
* NoSQL是对不同于传统的关系数据库的数据库管理系统的统称
> BigTable (Google)
> Cassandra
> MongoDB
> CouchDB
> Redis

---

* 键值数据库简介
> Apache Cassandra(为Facebook所使用)高度可扩展
> Dynamo
> LevelDB(Google)

---

**数据库关系模型简述(数据结构):**

1. 对象模型
* 层次-层次模型
>`Hierarchical database model`
> 轻量级数据访问协议
> 用树形结构描述实体及其之间关系的数据模型

2. 网状-网状模型
> `Network model`
> 用于大型数据储存
> 由美国的`查尔斯·巴赫曼(Charles William Bachman)`发明 

3. 平面-平面模型
* `Flat-file database`
* 表格模型，一般在形式上是一个二维数组
* 如表格模型数据Excel
* 不同于平面文件系统`Flat file system`

4. 关系-关系模型
> `Relational model`
> 基于谓词逻辑和集合论的一种数据模型

5. ER模型-增强实体关系模型
> `Entity-relationship model`
> 概念数据模型的高层描述所使用的数据模型或模式图

6. 图-图数据库
> `graph database,GDB` 
> 使用图结构进行语义查询的数据库，它使用节点、边和属性来表示和存储数据
> 该系统的关键概念是图，它直接将存储中的数据项，与数据节点和节点间表示关系的边的集合相关联

7. 面向对象-面向对象模型
> 面向对象数据库
> 对象数据库的数据库管理系统被称为`ODBMS`或`OODBMS`
> 以对象形式表示信息的数据库

8. 实体-属性-值
> `Entity–attribute–value model,EAV`
> EAV也称为对象属性值模型，垂直数据库模型和开放式架构
> 是一种数据模型，以节省空间的方式对实体进行编码，其中可以用来描述实体的属性(属性，参数)的数量可能很大，但是实际适用于给定的实体是相对适度的
> 这样的实体对应于稀疏矩阵的数学概念

9. 空间/纬度建模
> `Dimensional modeling,DM`

10. 半结构化模型

---

**其他模型:**

11. 关联-数据关联模型
> `Associative model of data`
> 数据的关联模型是一个数据模型的数据库系统

12. 多维-联机分析处理
> `Online analytical processing,OLAP`
> 是计算机技术中快速解决多维分析问题(MDA)的一种方法

13. 数组-矩阵数据库管理系统
> `Array DBMS`
> `Array database management systems`(array DBMSs) 
> 矩阵数据库管理系统(Array DBMS)专门为矩阵(也称为栅格数据)提供数据库服务

14. 语义数据模型
> `Semantic data model,SDM`
> 基于高级语义的数据库描述和数据库的结构形式化(数据库模型)

15. 星模式
> `Star schema`
> 在计算中，星形模式是数据集市模式的最简单样式，并且是最广泛用于开发数据仓库和维度数据集市的方法

16. XML数据库
> `XML database`
> 数据持久性软件系统，该系统允许数据被指定，有时存储在XML格式

**关于实现方法这里不做阐述**

---

**架构:**
* 数据库的架构可以大致区分为三个概括层次:内层,概念层和外层
> 内层:最接近实际存储体，亦即有关数据的实际存储方式
> 外层:最接近用户，即有关个别用户观看数据的方式
> 概念层:介于两者之间的间接层

---

**数据库事务**
* 事务(transaction)包含一组数据库操作的逻辑工作单元，在事务中包含的数据库操作是不可分割的整体
* 这些操作要么一起做，要么一起回滚(Roll Back)到执行前的状态
* 事务的ACID特性：
> 基元性 (atomicity)
> 一致性 (consistency)
> 隔离性 (isolation)
> 持续性 (durability)
* 事务的并发性是指多个事务的并行操作轮流交叉运行，事务的并发可能会访问和存储不正确的数据，破坏交易的隔离性和数据库的一致性

---

* 网状模型-网状数据模型的数据结构
* 满足下面两个条件的基本层次联系的集合为网状模型
1. 允许一个以上的结点无双亲
2. 一个结点可以有多于一个的双亲

---

**其他:**

* 数据库管理系统是指管理数据库的程序

* 相关概念简述:
> 数据库存储结构(Database storage structures)
> 数据模型(data model)
> 数据库模型(database model)
> 关系模型(Relational model)
> 数据结构(data structure)
> 数据类型
