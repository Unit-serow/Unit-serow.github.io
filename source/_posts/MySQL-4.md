---
title: MySQL-4
date: 2020-02-15 01:49:54
tags: [RDBMS,随笔]
categories: [软件,数据库]
---

### MySQL数据导出与导入

**导出**

* 所导出目标文件必须为有可读写权限
* 使用`SELECT ... INTO OUTFILE`语句

* 基本语法:
```
mysql> SELECT * FROM table_name
    -> INTO OUTFILE '目标路径';
```

* 使用mysqldump导出原始数据
```
$ mysqldump -u root -p --no-create-info \
            --tab=/目标文件路径 database_name table_name
password:
```

* 导出SQL格式的文件
* 不添加`table_name`导出整个数据库
```
$ mysqldump -u root -p database_name table_name > 目标文件路径
password:
```
* 导出所有数据库
```
$ mysqldump -u root -p --all-databases > 目标文件路径
password:
```

---

**导入**

* mysql 命令导入
> `mysql -u username -p passwrod < 要导入的数据库数据文件路径(xxx.sql)`

* source 命令导入
* 登录到数库终端执行以下命令
```
mysql> USE DATABASE_NAME;
mysql> SET NAMES utf8;
mysql> SOURCE /目标文件路径(.sql)
```

```
mysqlimport导入
$ mysqlimport -u root -p --local tables_name /被导入文件路径
password *****
```

---

**PHP语法简介**

* PHP Mysqli
* mysqli()函数

**格式**
>`mysqli_function(value,value,...);` 

* 以上格式中function部分描述了mysqli()函数的功能，例如:
> `mysqli_connect($connect);`
> `mysqli_query($connect,"SQL 语句");`
> `mysqli_fetch_array()`
> `mysqli_close()`

---

**mysqladmin用法简述**

* 管理性操作语法
> `mysqladmin [OPTIONS] command [command-option] command ...`

* 帮助指令
> `mysqladmin --help`

* 连接
> `mysqladmin -u[username] -p[password] status`

---

**简要参数:**

|参数|作用|
|:----|:----|
|create databasename|创建一个新数据库|
|drop databasename|删除一个数据库及其所有表|
|shutdown|关掉服务器| 
|kill id,id,...|杀死mysql线程|
|flush-logs|清理掉所有日志| 
|flush-tables|清理掉所有表|
|ping|检查mysqld是否存在|

---
