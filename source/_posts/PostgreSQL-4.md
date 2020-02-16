---
title: PostgreSQL-4
date: 2020-02-16 15:07:38
tags: [ORDBMS,随笔]
categories: [软件,数据库]
---

### PostSQL-4

**PostgreSQL命令语句便捷参考(总览)**

* 中文手册详细资料[跳转](http://www.postgres.cn/docs/9.6/)
> `http://www.postgres.cn/docs/9.6/`

* 输出帮助内容
> `postgres-# \help <command_name>`

---

**CREATE**

* 定义一个新的聚集函数
> `CREATE AGGREGATE`

* 定义一个用户定义的转换
> `CREATE CAST`

* 定义一个新的约束触发器 
> `CREATE CONSTRAINT TRIGGER`

* 定义一个新的的编码转换
> `CREATE CONVERSION`

* 创建新数据库
> `CREATE DATABASE`

* 定义一个新域
> `CREATE DOMAIN`

* 定义一个新函数
> `CREATE FUNCTION`

* 定义一个新的用户组
> `CREATE GROUP`

* 定义一个新索引
> `CREATE INDEX`

* 定义一种新的过程语言
> `CREATE LANGUAGE`

* 定义一个新的操作符
> `CREATE OPERATOR`

* 定义一个新的操作符表
> `CREATE OPERATOR CLASS`

* 定义一个新的数据库角色
> `CREATE ROLE`

* 定义一个新重写规则
> `CREATE RULE`

* 定义一个新模式
> `CREATE SCHEMA`

* 定义一个新的外部服务器
> `CREATE SERVER`

* 定义一个新序列发生器
> `CREATE SEQUENCE`

* 定义一个新表
> `CREATE TABLE`

* 从一条查询的结果中定义一个新表
> `CREATE TABLE AS`

* 定义一个新的表空间
> `CREATE TABLESPACE`

* 定义一个新的触发器
> `CREATE TRIGGER`

* 定义一个新的数据类型
> `CREATE TYPE`

* 创建一个新的数据库用户帐户
> `CREATE USER`

* 定义一个视图
> `CREATE VIEW`


---

**ALTER**

* 修改一个聚集函数的定义
> `ALTER AGGREGATE`

* 修改一个排序规则定义
> `ALTER COLLATION`

* 修改一个编码转换的定义
> `ALTER CONVERSION`

* 修改一个数据库
> `ALTER DATABASE`

* 定义默认的访问权限
> `ALTER DEFAULT PRIVILEGES`

* 修改一个域的定义
> `ALTER DOMAIN`

* 修改一个函数的定义
> `ALTER FUNCTION`

* 修改一个用户组
> `ALTER GROUP`

* 修改一个索引的定义
> `ALTER INDEX`

* 改变一个操作符的定义
> `ALTER OPERATOR`

* 修改一个模式的定义
> `ALTER SCHEMA`

* 修改一个序列生成器的定义
> `ALTER SEQUENCE`

* 修改表的定义
> `ALTER TABLE`

* 修改一个表空间的定义
> `ALTER TABLESPACE`

* 修改改变一个触发器的定义
> `ALTER TRIGGER`

* 修改一个类型的定义
> `ALTER TYPE`

* 修改数据库用户帐号
> `ALTER USER`

* 更新一个表中的行
> `UPDATE`

---

**删除**

* 删除一个准备好的查询
> `DEALLOCATE`

* 删除一个表中的行
> `DELETE`

* 删除一个用户定义的聚集函数
> `DROP AGGREGATE`

* 删除一个用户定义的类型转换
> `DROP CAST`

* 删除一个用户定义的编码转换
> `DROP CONVERSION`

* 删除一个数据库
> `DROP DATABASE`

* 删除一个用户定义的域
> `DROP DOMAIN`

* 删除一个函数
> `DROP FUNCTION`

* 删除一个用户组
> `DROP GROUP`

* 删除一个索引
> `DROP INDEX`

* 删除一个过程语言
> `DROP LANGUAGE`

* 删除一个操作符
> `DROP OPERATOR`

* 删除一个操作符表
> `DROP OPERATOR CLASS`

* 删除一个数据库角色
> `DROP ROLE`

* 删除一个重写规则
> `DROP RULE`

* 删除一个模式
> `DROP SCHEMA`

* 删除一个序列
> `DROP SEQUENCE`

* 删除一个表
> `DROP TABLE`

* 删除一个表空间
> `DROP TABLESPACE`

* 删除一个触发器定义
> `DROP TRIGGER`

* 删除一个用户定义数据类型
> `DROP TYPE`

* 删除一个数据库用户帐号
> `DROP USER`

* 删除一个视图
> `DROP VIEW`

* 清空一个或一组表
> `TRUNCATE`

---

`SELECT`
> 从表或视图中取出若干行

`SELECT INTO`
> 从一个查询的结果中定义一个新表

---

`SET`
> 修改运行时参数

`SET CONSTRAINTS`
> 设置当前事务的约束检查模式

`SET SESSION AUTHORIZATION`
> 为当前会话设置会话用户标识符和当前用户标识符

`SET TRANSACTION`
> 开始一个事务块

---

**其它**


* 收集与数据库有关的统计
> `ANALYZE`

* 用于退出当前事务
> `ABORT`

* 开始一个事务块
> `BEGIN`

* 开始一个事务块
> `START TRANSACTION`

* 提交当前事务
> `COMMIT`

* 提交当前的事务
> `END`

* 在当前事务里定义一个新的保存点
> `SAVEPOINT`

* 回滚到一个保存点
> `ROLLBACK TO SAVEPOINT`

* 退出当前事务
> `ROLLBACK`

* 强制一个事务日志检查点
> `CHECKPOINT`

* 定义一个游标
> `DECLARE`

* 定位一个游标
> `MOVE`

* 用游标从查询中抓取行
> `FETCH`

* 关闭游标
> `CLOSE`

* 重建索引
> `REINDEX`

* 根据一个索引对某个表盘簇化排序
> `CLUSTER`

* 定义或者改变一个对象的注释
> `COMMENT`

* 删除一个前面定义的保存点
> `RELEASE SAVEPOINT`

* 在表和文件之间拷贝数据
> `COPY`

* 创建一个准备好的查询
> `PREPARE`

* 执行一个准备好的查询
> `EXECUTE`

* 显示一个语句的执行规划
> `EXPLAIN`

* 生成一个通知
> `NOTIFY`

* 定义访问权限
> `GRANT`

* 删除访问权限
> `REVOKE`

* 在表中创建新行，即插入数据
> `INSERT`

* 监听一个通知
> `LISTEN`

* 停止监听通知信息
> `UNLISTEN`

* 加载或重载一个共享库文件
> `LOAD`

* 锁定一个表
> `LOCK`

* 把一个运行时参数值恢复为默认值
> `RESET`

* 显示运行时参数的值
> `SHOW`

* 垃圾收集以及可选地分析一个数据库
> `VACUUM`

* 计算一个或一组行
> `VALUES`

---
