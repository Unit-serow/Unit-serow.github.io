---
title: Redis-2
date: 2020-02-16 18:14:47
tags: [Key-value,随笔]
categories: [软件,数据库]
---

## Redis-2

* 配置与数据类型简述

---

### Redis配置

* 启动Redis
> `$ redis-server`
* 打开终端(查看redis是否启动)
> `$ redis-cli`
> `redis 127.0.0.1:6379>`
> 本机IP:`127.0.0.1`，redis服务端口:`6379`

```
root@debian:~# redis-cli
127.0.0.1:6379> 
```

---

* 配置文件
> `/安装目录/redis.conf`

* CONFIG命令用于查看或设置配置项

* 命令格式
> `redis 127.0.0.1:6379> CONFIG GET CONFIG_SETTING_NAME`
> `*` 用于匹配所有配置项
> `redis 127.0.0.1:6379> CONFIG GET *`

* 可以通过修改redis.conf文件或使用 CONFIG set 命令来修改配置
* CONFIG SET 命令
* 基本语法：
> `redis 127.0.0.1:6379> CONFIG SET CONFIG_SETTING_NAME NEW_CONFIG_VALUE`

* 对于GONFIG的参数与redis.conf的配置项在本篇内不进行过多阐述

---

### 数据类型简述

* Redis支持五种数据类型:
* String(字符串)
* Hash(哈希)
* List(列表)
* Set(集合)
* Zset(sorted set:有序集合)

---

* 本篇中的应用实例简述只列举出最基本的用法，其他命令不会多做阐述
* 在命令提示符内输入命令时Redis会给出对应的相关提示
* 删除:`DEL KEY_name`

---

1. String(字符串)
* String是redis最基本的类型，方式是一个`Key`对应一个`Value`
* String类型是二进制安全的，即Redis的String可以包含任何数据，包括序列化的对象与任何形式的图片
* String类型的值最大能存储512MB
* 相关命令:`SET`与`GET`

* 应用实例:
* 使用Redis中的`SET`与`GET`命令，`Key`为`UNIT`，`Value`为`serow`
> `SET UNIT "serow"`
> `GET UNIT`

* 输出:
```
127.0.0.1:6379> SET UNIT "serow"
OK
127.0.0.1:6379> GET UNIT
"serow"
```

* 删除
> `DEL UNIT`

```
127.0.0.1:6379> DEL UNIT
(integer) 1
127.0.0.1:6379> DEL UNIT
(integer) 0
```

---

2. Hash(哈希)
* Redis hash是一个键值(key=>value)对集合
* Redis hash是一个String类型的`field`和`value`的映射表
* Hash适合用于存储对象
* 每个hash可以存储`2^32-1`键值对(40多亿)
* 相关命令:`HMSET`与`HGET`

* 应用实例:
* 使用Redis中的`HMSET`与`HGET`命令，`HMSET`设置了两个`field=>value`对，`HGET`获取对应`field`对应的`value`
> `HMSET UNIT field1 "serow" field2 "takin"`
> `HGET UNIT field1`
> `HGET UNIT field2`

* 输出:
```
127.0.0.1:6379> HMSET UNIT field1 "serow" field2 "takin"
OK
127.0.0.1:6379> HGET UNIT field1
"serow"
127.0.0.1:6379> HGET UNIT field2
"takin"
```

* 删除
> `DEL UNIT`

```
127.0.0.1:6379> DEL UNIT
(integer) 1
127.0.0.1:6379> DEL UNIT
(integer) 0
```

---

3. List(列表)
* Redis 列表是简单的字符串列表，按照插入顺序排序
* 可以添加一个元素到列表的头部(左侧)或者尾部(右侧)
* 列表最多可存储`2^32-1`元素 (4294967295, 每个列表可存储40多亿)
* 相关命令:`LPUSH`与`LRANGE`

* 应用实例:
* 使用Redis中的`LPUSH`与`LRANGE`命令
> `LPUSH UNIT redis`
> `LPUSH UNIT serow`
> `LPUSH UNIT takin`
> `LRANGE UNIT 0 10`

* 输出:
```
127.0.0.1:6379> LPUSH UNIT redis
(integer) 1
127.0.0.1:6379> LPUSH UNIT serow
(integer) 2
127.0.0.1:6379> LPUSH UNIT takin
(integer) 3
127.0.0.1:6379> LRANGE UNIT 0 10
1) "takin"
2) "serow"
3) "redis"
```

* 删除
> `DEL UNIT`

```
127.0.0.1:6379> DEL UNIT
(integer) 1
127.0.0.1:6379> DEL UNIT
(integer) 0
```

* 还可以写为
> `LPUSH A A B C D E F G`
> `LRANGE A 0 10`

* 输出:
```
127.0.0.1:6379> LPUSH A A B C D E F G
(integer) 7
127.0.0.1:6379> LRANGE A 0 10
1) "G"
2) "F"
3) "E"
4) "D"
5) "C"
6) "B"
7) "A"
```

* 删除
> `DEL A`

```
127.0.0.1:6379> DEL A
(integer) 1
127.0.0.1:6379> DEL A
(integer) 0
```

---

4. SET(集合)
* Redis的Set是String类型的无序集合
* 集合是通过哈希表实现的，即添加，删除，查找的复杂度都是O(1)
* 集合中最大的成员数为`2^32-1`(4294967295, 每个集合可存储40多亿个成员)
* 相关命令:`SADD`与`SMEMBERS`

* 应用实例:
* 使用Redis中的`SADD`与`SMEMBERS`命令
> `SADD UNIT redis`
> `SADD UNIT serow`
> `SADD UNIT takin`
> `SADD UNIT takin`
> `SMEMBERS UNIT`

* 输出:
```
127.0.0.1:6379> SADD UNIT redis
(integer) 1
127.0.0.1:6379> SADD UNIT serow
(integer) 1
127.0.0.1:6379> SADD UNIT takin
(integer) 1
127.0.0.1:6379> SADD UNIT takin
(integer) 0
127.0.0.1:6379> SMEMBERS UNIT
1) "redis"
2) "takin"
3) "serow"
```

* 实例中takin添加了两次，但根据集合内元素的唯一性，第二次插入的元素将被忽略

* 删除
> `DEL UNIT`

```
127.0.0.1:6379> DEL UNIT
(integer) 1
127.0.0.1:6379> DEL UNIT
(integer) 0
```

---

5. ZSET(sorted set：有序集合)
* Redis zset和Set一样也是String类型元素的集合,且不允许重复的成员
* 不同的是每个元素都会关联一个`double类型`的分数
* Redis正是通过分数来为集合中的成员进行从小到大的排序
* Zset的成员是唯一的,但分数(score)却可以重复
* 相关命令:`ZADD`与`ZRANGEBYSCORE`

* 基本语法:
* 添加元素到集合，元素在集合中存在则更新对应`score`
> `zadd key score member`

* 应用实例:
* 使用Redis中的ZADD与ZRANGEBYSCORE命令
> `ZADD UNIT 0 redis`
> `ZADD UNIT 0 serow`
> `ZADD UNIT 0 takin`
> `ZADD UNIT 0 takin`
> `ZRANGEBYSCORE UNIT 0 1000`

* 输出:
```
127.0.0.1:6379> ZADD UNIT 0 redis
(integer) 1
127.0.0.1:6379> ZADD UNIT 0 serow
(integer) 1
127.0.0.1:6379> ZADD UNIT 0 takin
(integer) 1
127.0.0.1:6379> ZADD UNIT 0 takin
(integer) 0
127.0.0.1:6379> ZRANGEBYSCORE UNIT 0 1000
1) "redis"
2) "serow"
3) "takin"
```

* 删除
> `DEL UNIT`

```
127.0.0.1:6379> DEL UNIT
(integer) 1
127.0.0.1:6379> DEL UNIT
(integer) 0
```

---

**各个数据类型应用场景:**

|类型|简介|特性|场景|
|:----|:----|:----|:----|
|String(字符串)|二进制安全|可以包含任何数据,比如jpg图片或者序列化的对象,一个键最大能存储512M|---|
|Hash(字典)|键值对集合,即编程语言中的Map类型|适合存储对象,并且可以像数据库中update一个属性一样只修改某一项属性值(Memcached中需要取出整个字符串反序列化成对象修改完再序列化存回去)|存储,读取,修改用户属性|
|List(列表)|链表(双向链表)|增删快,提供了操作某一段元素的API|1. 最新消息排行等功能(比如朋友圈的时间线) 2.消息队列|
|Set(集合)|哈希表实现,元素不重复|1. 添加、删除,查找的复杂度都是O(1) 2. 为集合提供了求交集、并集、差集等操作|1.共同好友 2. 利用唯一性,统计访问网站的所有独立ip 3、好友推荐时,根据tag求交集,大于某个阈值就可以推荐|
|Sorted Set(有序集合)|将Set中的元素增加一个权重参数score,元素按score有序排列|数据插入集合时,已经进行天然排序|1. 排行榜 2. 带权重的消息队列|

---

