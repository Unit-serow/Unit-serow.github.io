---
title: Redis-3
date: 2020-02-16 21:01:07
tags: [随笔,NoSQL]
categories: [软件,数据库]
---

### Redis-简易参考

**便捷参考**

* 基本语法:
> `redis 127.0.0.1:6379> COMMAND KEY_NAME VALUE`
* 参数说明:
> `COMMAND为命令(映射于数据类型)`
> `KEY_NAME为键`
> `VALUE 为值`

---

**相关命令简述(不进行详细说明)**

* String/Hash/List/Set/Sorted set不进行说明
* Redis 在 2.8.9 版本添加了 HyperLogLog 结构
* Redis HyperLogLog 是用来做基数统计的算法

|相关说明|相关参数|
|:----|:----|
|HyperLogLog用于实现基数统计算法|PFADD\PFCOUNT\PFMERGE|
|订阅|SUBSCRIBE\PUBLISH|
|事务|MULTI\EXEC\DISCARD|
|脚本|EVAL|
|连接|PING\QUIT\SELECT index|
|服务|INFO|
|备份|Bgsave\SAVE| 
|恢复|SAVE| 
|安全|CONFIG\AUTH|
|性能测试|redis-benchmark [option] [option value]|
|连接客户端|redis-server --maxclients [最大连接数]|CLIENT KILL|

---

**相关概念**

* 订阅
* 事务
* 脚本
* 连接
* 服务器
* 数据备份
* 数据恢复
* 安全
* 管道技术
* 分区
* 测试(性能)
* Log

---

* 参考资料:[跳转](https://redis.io/commands)
> `https://redis.io/commands`

* 在线测试[跳转](http://try.redis.io/)
> `http://try.redis.io/`

---
