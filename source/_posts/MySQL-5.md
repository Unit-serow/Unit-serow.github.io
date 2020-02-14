---
title: MySQL-5
date: 2020-02-15 02:19:25
tags: [随笔,RDBMS]
categories: [软件,数据库]
---

### MySQL-5

* MySQL补充内容
* MySQL可执行目录/usr/bin/mysql
* MySQL配置文件目录/etc/my.cnf

---

**添加用户**

```
mysql> use mysql;
Database changed

mysql> INSERT INTO user 
          (host, user, password, 
           select_priv, insert_priv, update_priv) 
           VALUES ('localhost', 'guest', 
           PASSWORD('guest123'), 'Y', 'Y', 'Y');
Query OK, 1 row affected (0.20 sec)
```

---

**泛用指令**
* 设置权限
> `chown mysql:mysql -R /var/lib/mysql`

* 初始化
> `mysqld --initialize`

* 查看所有数据库
> `SHOW DATABASES;`

* 查看当前数据库内所有表
> `SHOW TABLES;`

* 显示数据表的属性，属性类型，主键信息 ，是否为NULL，默认值等其他信息
> `SHOW COLUMNS FROM 数据表;`

* 显示数据表的详细索引信息，包括`PRIMARY KEY`(主键)
> `SHOW INDEX FROM 数据表;`

* 输出Mysql数据库管理系统的性能及统计信息
> `SHOW TABLE STATUS LIKE [FROM db_name] [LIKE 'pattern'] \G;` 

---

**RDBMS-MySQL参考资料**

* mysql官网[跳转](https://www.mysql.com/)
> `https://www.mysql.com/`

* mysql下载地址[跳转](https://dev.mysql.com/downloads/)
> `https://dev.mysql.com/downloads/`

* 文档(EN)[跳转](https://dev.mysql.com/doc/)
> `https://dev.mysql.com/doc/`

---

* MariaDB官网[跳转](https://mariadb.org)
> `https://mariadb.org`

* MariaDB下载地址[跳转](https://mariadb.org/download/)
> `https://mariadb.org/download/`

* 文档(CN)[跳转](https://mariadb.com/kb/zh-cn/mariadb/)
> `https://mariadb.com/kb/zh-cn/mariadb/`

---
