---
title: PostgreSQL-1
date: 2020-02-15 21:44:16
tags: [ORDBMS,随笔]
categories: [软件,数据库]
---

### PostgreSQL-1

**概述:**
* ORDBMS(关系数据库服务器)
* 基于BSD许可证发行

---

**基本特征:**
* 函数:通过函数，可以在数据库服务器端执行指令程序
* 索引:用户可以自定义索引方法，或使用内置的`B树`，`哈希表`与`GiST索引`
* 触发器:触发器是由SQL语句查询所触发的事件，如：一个INSERT语句可能触发一个检查数据完整性的触发器。触发器通常由`INSERT`或`UPDATE`语句触发
* 多版本并发控制:PostgreSQL使用多版本并发控制(MVCC，Multiversion concurrency control)系统进行并发控制，该系统向每个用户提供了一个数据库的"快照"，用户在事务内所作的每个修改，对于其他的用户都不可见，直到该事务成功提交
* 规则:规则(RULE)允许一个查询能被重写，通常用来实现对视图(VIEW)的操作，如插入(INSERT)、更新(UPDATE)、删除(DELETE)
* 数据类型:包括文本、任意精度的数值数组、`JSON数据`、`枚举类型`、`XML数据等`
* 全文检索:通过`Tsearch2`或`OpenFTS`，`8.3版本`中内嵌`Tsearch2`
* NoSQL:`JSON`，`JSONB`，`XML`，`HStore`原生支持，至`NoSQL`数据库的外部数据包装器
* 数据仓库:能平滑迁移至同属`PostgreSQL`生态的`GreenPlum`，`DeepGreen`，`HAWK`等，使用`FDW`进行`ETL`
* PostpreSQL与MySQL的语法与模式完全不同

---

**安装:**

* `apt-get`全自动安装
> `$ sudo apt-get install postgresql postgresql-client`
* 安装完毕后，系统会创建一个数据库超级用户postgres，密码为空
> `#  sudo -i -u postgres`
* 进入postgres命令行提示符
> `$ psql`
* 退出PostgreSQL命令行提示符
> `\q`

---

* 基本配置与帮助
* 可执行文件目录
> `/etc/init.d/postgresql`
> `/etc/postgresql`
* 配置文件目录
> `/usr/lib/postgresql`
* 帮助文档目录
> `/usr/share/postgresql`
* 帮助指令
> `postgres-# \help <command_name>`
* 例如
> `postgres=# \help SELECT`
* 查看所有帮助(指令用法)
> `postgres=# \?`

---

**其他:**
* `pgAdmin`工具(图形化管理与操作工具)
* `pgAdmin`工具提供了完整操作数据库的功能
* 类似于MySQL的`MySQLadmin`
* 封装命令
* 进入`PostpreSQL`的可执行目录内执行(/安装目录/bin)
* PostgreSQL特有性质，例如`CREATE DATABASE`语句等同于`createdb`命令
* 文案中将会避免使用封装命令，而尽可能多的使用SQL标准中所规定的标准语句
* 封装命令的执行不需要添加分号(`;`)
* 关于权限的使用与说明本篇不做阐述


---

* `createdb`命令语法格式如下:
* 进入`PostpreSQL`的可执行目录内执行
> `createdb [option...] [dbname [description]]`
* 参数说明:
> `dbname`:要创建的数据库名
> `description`:关于新创建的数据库相关的说明
> `options`:参数可选项，具体参考官方中文手册

* `psql`连接工具语法
* `psql`的命令都是以斜杠`\`开头的
* 关于`\`的具体使用，本篇将不会多做阐述
> `psql -h <hostname or ip> -p <端口> [数据库名称] [用户名称]`
* 执行存储在外部文件中的SQL命令
> `\i <文件名>`执行存储在外部文件中的sql语句
> 当然也可以在`psql命令行`加`-s <filename>`来执行SQL脚本文件中的命令
> 如`psql -s test.sql`

---

**快速参考**

* 相关概念简述:
* 数据类型
* 运算符
* 表达式
* 触发器
* NULL
* 子查询/嵌套查询/内部查询
* 事务
* 函数

---

* 模式 `SCHEMA`
* 别名 `AS`
* 序列  `smallserial/serial/bigserial(AUTO_INCREMENT)`
* 排序/分组 `order by(asc/desc)/group by`
* 连接 `UNION/JOIN LEFT/RIGHT/PULL/INNER/CROSS`
* 索引 `INDEX`
* 约束 `PRIMARY KEY/FOREIGN KEY/CHECK/EXCLUSION/UNIQUE/NOT NULL`
* 视图 `VIEW`
* 锁 `LOCK`
* 权限 `GRANT`
* 时间/日期 `DATE`

---

**参考资料:**

* 手册CN[跳转](http://www.postgres.cn/docs/9.6/)
> `http://www.postgres.cn/docs/9.6/`

* 10.1手册源码CN[跳转](https://github.com/postgres-cn/pgdoc-cn/wiki/pg10)
> `https://github.com/postgres-cn/pgdoc-cn/wiki/pg10`

* 最新版手册源码CN[跳转](https://github.com/postgres-cn/pgdoc-cn/releases)
> `https://github.com/postgres-cn/pgdoc-cn/releases`

* 手册翻译社区CN[跳转](https://github.com/postgres-cn/pgdoc-cn)
> `https://github.com/postgres-cn/pgdoc-cn`

* 官方网站[跳转](https://www.postgresql.org/)
> `https://www.postgresql.org/`

* 下载地址[跳转](https://www.postgresql.org/download/linux/debian/)
> `https://www.postgresql.org/download/linux/debian/`

* 软件源码[跳转](https://www.postgresql.org/ftp/source/)
> `https://www.postgresql.org/ftp/source/`

* `apt-get`获取
> `apt-get install postgresql postgresql-client`

---
