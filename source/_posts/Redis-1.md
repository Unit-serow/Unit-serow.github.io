---
title: Redis-1
date: 2020-02-16 15:55:15
tags: [随笔,NoSQL]
categories: [软件,数据库]
---

### REmote DIctionary Server(Redis)

**概述:**

* 是一种Key-Value数据库
* 还可称为key-value存储系统，即数据结构服务器
* 由ANSI C语言编写
* 是基于BSD协议的`Free software`
* 支持多种语言的API
* 支持网络
* 可基于内存亦可持久化的日志型

---

* Redis具有极为先进的数据管理方式与处理算法
* Redis与其它`key-value`缓存产品相比的特有性质:
> Redis支持数据的持久化，可以将内存中的数据保存在磁盘中，重启的时候可以再次加载进行使用
> Redis不仅仅支持简单的`key-value`类型的数据，同时还提供`list`,`set`,`zset`,`hash`等数据结构的存储
> Redis支持数据的备份，即`master-slave`模式的数据备份
> Redis有着更为复杂的数据结构并且提供对他们的原子性操作，这是一个不同于其他数据库的进化路径
> Redis的数据类型都是基于基本数据结构的同时对程序员透明，无需进行额外的抽象
> Redis运行在内存中但是可以持久化到磁盘，所以在对不同数据集进行高速读写时需要权衡内存，因为数据量不能大于硬件内存
> 在内存数据库方面的另一个优点是，相比在磁盘上相同的复杂的数据结构，在内存中操作起来非常简单，这样Redis可以做很多内部复杂性很强的事情
> 同时，在磁盘格式方面他们是紧凑的以追加的方式产生的，因为他们并不需要进行随机访问

---

* Redis特点
> 性能特点: Redis能读的速度是`110000次/s`，写的速度是`81000次/s`
> 数据类型特点: Redis支持二进制案例的`Strings`,`Lists`,`Hashes`,`Sets`及`Ordered Sets`数据类型操作
* 原子性质:
> Redis的所有操作都是原子性的(只有成功且完全执行与失败且完全不执行)，单个操作是原子性的
> 多个操作也支持事务，即原子性，通过`MULTI`和`EXEC`指令对其进行封装

---

* 原子性操作:
> 将任何一套完整数据处理操作定义为一个事务
> 该事务要么完全执行，要么完全不执行，不会出现执行到一半因为错误而中止
> 以此绝对的保证了数据的完整性
> 如果把事务比作一个程序，它要么完整的被执行,要么完全不执行

* key value 存储
> 键值存储，即为key=>value
> 键=>值(key=>value)对，键唯一，对应一个值，值的形式随意
> 以此绝对的保证了数据结构的完备性

---

**相关基本概念(基本数据结构概念)**
* String: 字符串
* Hash: 散列
* List: 列表
* Set: 集合
* Sorted Set: 有序集合

---

**参考资料:**

* 文档[跳转](https://redis.io/documentation)
> `https://redis.io/documentation`

* 官网[跳转]( https://redis.io/)
> `https://redis.io/`

* 获取[跳转](https://redis.io/download)
> `https://redis.io/download`

* 配置说明[跳转](https://redis.io/topics/config)
> `https://redis.io/topics/config`

* apt-get自动化获取
> `apt-get install redis-server`

---
