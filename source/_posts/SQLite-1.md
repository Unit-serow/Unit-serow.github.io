---
title: SQLite-1
date: 2020-02-19 17:22:30
tags: [RDBMS,随笔]
categories: [软件,数据库]
---

### SQLite-1

---

* 创建数据库同时返回命令提示符
> `$sqlite3 TESTDB.db`

```
root@debian:/home/sqlite/file# sqlite3 TESTDB.db
SQLite version 3.31.1 2020-01-27 19:55:54
Enter ".help" for usage hints.
sqlite> 
```

查看所有数据库
> `.databases`

```
sqlite> .databases
main: /home/sqlite/file/TESTDB.db
```

* 创建TABLES2
```
CREATE TABLE TABLES2(
ID INTEGER PRIMARY KEY AUTOINCREMENT NOT NULL,
A TEXT NOT NULL,
B INT NOT NULL,
C CHAR(3),
D REAL);
```

```
sqlite> CREATE TABLE TABLES2(
ID INTEGER PRIMARY KEY AUTOINCREMENT NOT NULL,
A TEXT NOT NULL,
B INT NOT NULL,
C CHAR(3),
D REAL); 
```

* 设置表查询输出的格式
```
.width 3, 3, 3
SELECT * FROM TABLES2;
```

```
sqlite> .width 3, 3, 3
sqlite> SELECT * FROM TABLES2;
```

* 查看表信息
> `.table`

```
sqlite> .table
TABLES2
```

* 查看表配置
> `.schema`

```
sqlite> .schema
CREATE TABLE TABLES2(
ID INTEGER PRIMARY KEY AUTOINCREMENT NOT NULL,
A TEXT NOT NULL,
B INT NOT NULL,
C CHAR(3),
D REAL);
CREATE TABLE sqlite_sequence(name,seq);
```

---

* TABLES2修改为TABLES1
> `ALTER TABLE TABLES2 RENAME TO TABLES1;`

> `sqlite> ALTER TABLE TABLES2 RENAME TO TABLES1;`

* 添加新列TIME
> `ALTER TABLE TABLES1 ADD COLUMN TIME DATE;`

> `sqlite> ALTER TABLE TABLES1 ADD COLUMN TIME DATE;`

* 查看表信息
> `.table`

```
sqlite> .table
TABLES1
```

* 查看表配置
> `.schema`

```
sqlite> .schema
CREATE TABLE IF NOT EXISTS "TABLES1"(
ID INTEGER PRIMARY KEY AUTOINCREMENT NOT NULL,
A TEXT NOT NULL,
B INT NOT NULL,
C CHAR(3),
D REAL, TIME DATE);
CREATE TABLE sqlite_sequence(name,seq);
```

---

* `BEGIN;`
> `sqlite> BEGIN;`

* 插入数据
```
[3条] INSERT INTO TABLES1 (A,B,C,D,TIME) VALUES (1, 2, 3, 4, NOW())/(2020-2-19);
[1条] INSERT INTO TABLES1 VALUES (4, 1, 2, 6, 7, NOW())/(2020-2-19);
[1条] INSERT INTO TABLES1  VALUES (5, 1, 2, 3, 4, 2020-2-18);
[1条] INSERT INTO TABLES1  VALUES (6, 1, 2, 3, 4, 2020-2-18);
```

```
`INSERT INTO TABLES1 (A,B,C,D,TIME) VALUES (1, 2, 3, 4, 2020-2-19);`
`INSERT INTO TABLES1  VALUES (4, 1, 2, 6, 7, 2020-2-19);`
```

```
sqlite> INSERT INTO TABLES1 (A,B,C,D,TIME) VALUES (1, 2, 3, 4, 2020-2-19);
sqlite> INSERT INTO TABLES1 (A,B,C,D,TIME) VALUES (1, 2, 3, 4, 2020-2-19);
sqlite> INSERT INTO TABLES1 (A,B,C,D,TIME) VALUES (1, 2, 3, 4, 2020-2-19);
sqlite> INSERT INTO TABLES1  VALUES (4, 1, 2, 6, 7, 2020-2-19);
sqlite> INSERT INTO TABLES1  VALUES (5, 1, 2, 3, 4, 2020-2-18);
sqlite> INSERT INTO TABLES1  VALUES (6, 1, 2, 3, 4, 2020-2-18);
```

* 快照一
> `COMMIT;`
> `sqlite> COMMIT;`

* `BEGIN;`
> `sqlite> BEGIN;`

* 删除ID等于6的行
> `DELETE FROM TABLES1 WHERE ID = 6;`
> `sqlite> DELETE FROM TABLES1 WHERE ID = 6;`

* 更新TABLES1内C,D列的数据
```
UPDATE TABLES1
SET C = 3, D = 4
WHERE ID = 4;
```

```
sqlite> UPDATE TABLES1
   ...> SET C = 3, D = 4
   ...> WHERE ID = 4;   
```

> `SELECT * FROM TABLES1;`

```
sqlite> SELECT * FROM TABLES1;
1|1|2|3|4.0|1999
2|1|2|3|4.0|1999
3|1|2|3|4.0|1999
4|1|2|3|4.0|1999
5|1|2|3|4.0|2000
```

* 结束
> `COMMIT`
> `sqlite> COMMIT;`

---

* 创建表TABLES2并将TABLES1内数据复制到其中

* 查看表配置
> `.schema`

```
sqlite> .schema
CREATE TABLE IF NOT EXISTS "TABLES1"(
ID INTEGER PRIMARY KEY AUTOINCREMENT NOT NULL,
A TEXT NOT NULL,
B INT NOT NULL,
C CHAR(3),
D REAL, TIME DATE);
CREATE TABLE sqlite_sequence(name,seq);
```

* 复制配置信息，将TABLES1改为TABLES2
```
CREATE TABLE TABLES2(
ID INTEGER PRIMARY KEY AUTOINCREMENT NOT NULL,
A TEXT NOT NULL,
B INT NOT NULL,
C CHAR(3),
D REAL, TIME DATE);
```

```
sqlite> CREATE TABLE TABLES2(
   ...> ID INTEGER PRIMARY KEY AUTOINCREMENT NOT NULL,
   ...> A TEXT NOT NULL,
   ...> B INT NOT NULL,
   ...> C CHAR(3),
   ...> D REAL, TIME DATE);
```

* 复制TABLES1信息到TABLES2
```
INSERT INTO TABLES2 (A,B,C,D,TIME)
SELECT A,B,C,D,TIME
FROM TABLES1;
```

```
sqlite> INSERT INTO TABLES2 (A,B,C,D,TIME)
   ...> SELECT A,B,C,D,TIME
   ...> FROM TABLES1;
```

`SELECT * FROM TABLES2;`

```
sqlite> SELECT * FROM TABLES2;
1|1|2|3|4.0|1999
2|1|2|3|4.0|1999
3|1|2|3|4.0|1999
4|1|2|3|4.0|1999
5|1|2|3|4.0|2000
```

---

* 为TABLES1的A列与B列添加组合索引
> `CREATE INDEX INDEX1 ON TABLES1 (A,B);`

> `sqlite> CREATE INDEX INDEX1 ON TABLES1 (A,B);`

* 列出表TABLES1内所有可用索引
> `.indices/.indexes TABLES1`

```
sqlite> .indexes TABLES1
INDEX1
```

---

* 删除索引(索引最好不要使用在较小或频繁且大批量更新的表与列上，且最好不要有太多的NULL值)
> `DROP INDEX INDEX1;`
> `sqlite> DROP INDEX INDEX1;`

> `.exit`

* 将TESTDB数据库导以`.sql`后缀导出到当前文件夹
> $sqlite3 TESTDB.db .dump > testDB.sql;

```
root@debian:/home/sqlite/file# ls -l
总用量 20
-rw-r--r-- 1 root root 20480 2月  19 17:15 TESTDB.db
-rw-r--r-- 1 root root     0 2月  19 17:02 testDB.sql
```

> `$sqlite3 TEST1`

* 删除表TABLES1与TABLES2内所有内容
> `DELETE FROM TABLES1;`
> `DELETE FROM TABLES2;`

```
sqlite> DELETE FROM TABLES1;
sqlite> DELETE FROM TABLES2;
```

```
sqlite> SELECT * FROM TABLES1;
sqlite> SELECT * FROM TABLES2;
```

* 删除表TABLES1与TABLES2
> `DROP TABLE TESTDB.TABLES1;`或`DROP TABLE TABLES1;`
> `DROP TABLE TESTDB.TABLES2;`或`DROP TABLE TABLES2;`

```
sqlite> DROP TABLE TABLES1;
sqlite> DROP TABLE TABLES2;
```

> `.tables`
> `sqlite> .tables`

---

**其它:**

* SQLite命令提示符内命令不需要分号，而语句需要分号(";")
* 大多数命令和语句不区分大小写(GLOB和glob对大小写敏感)
* 命令多以点符号`'.'`开头
* `.help`输出帮助指令
* 键入`sqlite指令`进入命令提示符界面

---

**附加&分离**

* 附加UNITDB数据库
* 基本语法:
> `ATTACH DATABASE file_name AS database_name;`
* 将UNITDB附加到已有数据库TESTDB.db上
> `ATTACH DATABASE 'TESTDB.db' as 'UNITDB';`

* 分离UNITDB数据库
* 基本语法:
> `DETACH DATABASE 'Alias-Name';`
把'UNITDB'从testDB.db中分离出来
> `DETACH DATABASE 'UNITDB';`

* 输出结果:
```
sqlite> .database
seq  name               file
---  ---------------  ----------------------
0    main                 /home/sqlite/testDB.db
2    test                   /home/sqlite/testDB.db
```

* 说明:
> 数据库名称 main 和 temp 被保留用于主数据库和存储临时表及其他临时数据对象的数据库
> 这两个数据库名称可用于每个数据库连接

---

### 其它概念:

* 基本语法
* 数据类型
* 运算符
* 导入与导出
* 数据库:分离(游离)
* 数据库:附加
* 表达式
* NULL
* 序列
* 触发器
* 索引
* ALTER(限制)
* 别名
* Truncate(无)
* SQLite注入
* VACUUM(Vacuum)
* Explain(解释)
* 日期&时间
* 函数

---
