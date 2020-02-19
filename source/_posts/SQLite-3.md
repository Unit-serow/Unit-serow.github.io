---
title: SQLite-3
date: 2020-02-19 20:44:10
tags: [RDBMS,随笔]
categories: [软件,数据库]
---

### SQLite-3

**概述:**

* 是遵守ACID的RDBMS(关系数据库管理系统)
> 因为SQLite遵守了ACID，所以实现了大多数SQL标准
> ACID(原子性,一致性,隔离性和持久性)
* 它使用动态的、弱类型的SQL语法
* 它作为嵌入式数据库，是应用程序，如网页浏览器，在本地/客户端存储数据的常见选择
* 与其它DBMS(数据库管理系统)不同的特点
> SQLite不是一个C/S(客户端/服务器结构)的数据库引擎，而是被集成在用户程序中
> 它有许多程序设计语言的语言绑定
* 虽然遵守了ACID，但还有以下未解决的问题
> 仅部分支持触发器
> ALTER TABLE功能有所限制，不能修改或删除列，只能通过重新创建表的方式迂回进行
> 参考局限性内容
---
* sqlite3的独立程序用来查询和管理SQLite数据库文件
> SQLite的用户可以把这个程序当作如何写SQLite应用程序的示例
* 支持且拥有多种语言接口(C/C++,Tcl,PHP,Java等等)
* SQLite通常小于600KB

---

### SQLite特点

* 完全不需要一个单独的服务器进程或操作的系统(无服务器的)
* SQLite 不需要配置，即不需要安装或管理
* 一套完整的SQLite数据库是存储在一个单一的跨平台的磁盘文件
* SQLite非常小的，是轻量级的，完全配置时小于400KiB，省略可选功能配置时小于250KiB
* SQLite能够自给自足的，即不需要任何外部的依赖
* SQLite事务完全兼容 ACID，允许从多个进程或线程安全访问
* SQLite支持SQL92(SQL2)标准的大多数查询语言的功能
* SQLite使用ANSI-C 编写，并提供了大量简单和易于使用的 API
* SQLite兼容于UNIX，UNIX-Like(Linux, Mac OS-X, Android, iOS)和Windows(Win32, WinCE, WinRT)
* SQLite拥有一套完整的与Shell交互的指令集

---

### SQLite安装

```
$ wget https://www.sqlite.org/download.html/sqlite-autoconf-3310100.tar.gz
$ tar xvzf sqlite-autoconf-3310100.tar.gz
$ cd sqlite-autoconf-3310100
$ ./configure --prefix=/usr/local(安装目录所在路径，/usr/local为用户环境变量)
$ make
$ make install
```

---

### 第三方GUI类插件

* SQLite拥有多种管理客户端，用以为SQLite提供GUI
* Navicat for SQLite是一套专为SQLite设计的强大数据库管理及开发工具
> 它可以用于任何版本2或3的SQLite数据库，并支持大部分SQLite的功能，包括触发器，索引，查看等
* SQLiteMan，使用Qt开发的一个SQLite客户端，支持多语言、跨平台
* Firefox，可以通过添加部分扩展获得SQLite客户端，包括`SQLite Manager`,`SQLite Reader`.`SQLite Manager`(另一个同名的WebExtensions扩展)
* SQLite Database Browser，一款连接SQLite数据库的图形客户端
* SQLite Expert Personal，Windows上的一款连接SQLite数据库的免费客户端

---

### SQLite 局限性

**在SQLite中，SQL92不支持的特性:**

|特性|描述|
|:----|:----|
|RIGHT OUTER JOIN|只实现了 LEFT OUTER JOIN|
|FULL OUTER JOIN|只实现了 LEFT OUTER JOIN|
|ALTER TABLE|支持 RENAME TABLE 和 ALTER TABLE 的 ADD COLUMN variants 命令，不支持 DROP COLUMN，ALTER COLUMN，ADD CONSTRAINT|
|Trigger支持|支持 FOR EACH ROW 触发器，但不支持 FOR EACH STATEMENT 触发器|
|VIEWS|在SQLite中，视图是只读的，即不可以在视图上执行 DELETE，INSERT 或 UPDATE 语句|
|GRANT 和 REVOKE|可以应用的唯一的访问权限是底层操作系统的正常文件访问权限|

---

### 其它概念

* DDL-数据定义语言

|命令|描述|
|:----|:----|
|CREATE|创建表，视图，数据库与其它对象|
|ALTER|修改数据库中的某个已有的数据库对象|
|DROP|用于删除表，视图，数据库与其它对象|

---

* DML-数据操作语言

|命令|描述|
|:----|:----|
|INSERT|插入记录|
|UPDATE|修改记录|
|DELETE|删除记录|

---

* DQL-数据查询语言

|命令|描述|
|:----|:----|
|SELECT|检索/查询|

---

### 常用函数(聚合函数)参考:

|函数|作用|
|:----|:----|
|MAX|返回最大值|
|MIN|返回最小值|
|COUNT|计算并返回行数|
|AVG|返回平均值|
|SUM|返回数值总和|
|RANDOM|用于伪随机数生成|
|ABS|返回参数绝对值|
|UPPER|将字符串转换为大写字母|
|LOWER|将字符串转化为小写字母|
|LENGTH|返回字符串长度|
|`sqlite_version`|返回SQLite库的版本|

---

### 参考资料:

* 官方网站:[跳转](http://www.sqlite.org/)
> `http://www.sqlite.org/`

* 源码地址:[跳转](https://www.sqlite.org/download.html)
> `https://www.sqlite.org/download.html`

* SQLite(PHP-API)文档:[跳转](http://www.php.net/manual/en/book.sqlite3.php)
> `http://www.php.net/manual/en/book.sqlite3.php`

* 获取方式:
> `wget https://www.sqlite.org/download.html/sqlite-autoconf-3310100.tar.gz`


