---
title: PostgreSQL-2
date: 2020-02-15 22:18:52
tags: [ODBMS,随笔]
categories: [软件,数据库]
---

### PortgreSQL-2

* 使用前几章MySQL中所规定的数据模型
* 默认超级管理员权限

---

* 创建数据库test1
> `CREATE DATABASE TEST1;`

```
postgres=# CREATE DATABASE TEST1;
CREATE DATABASE
```

* 查看所有数据库
> `\l`

```
postgres=# \l
                                     数据库列表
   名称    |  拥有者  | 字元编码 |  校对规则   |    Ctype    |       存取权限        
-----------+----------+----------+-------------+-------------+-----------------------
 postgres  | postgres | UTF8     | zh_CN.UTF-8 | zh_CN.UTF-8 | 
 template0 | postgres | UTF8     | zh_CN.UTF-8 | zh_CN.UTF-8 | =c/postgres          +
           |          |          |             |             | postgres=CTc/postgres
 template1 | postgres | UTF8     | zh_CN.UTF-8 | zh_CN.UTF-8 | =c/postgres          +
           |          |          |             |             | postgres=CTc/postgres
 test1     | postgres | UTF8     | zh_CN.UTF-8 | zh_CN.UTF-8 | 
(4 行记录)
```

* 连接数据库，默认用户`postgres`
> `\c test1;`

```
postgres=# \c test1;
您现在已经连接到数据库 "test1",用户 "postgres".
```

---

* 模式A
> `CREATE SCHEMA A;`

```
test1=# CREATE SCHEMA A;
CREATE SCHEMA
```

* 表`A.tables1`
```
CREATE TABLE A.tables1(
ID SERIAL PRIMARY KEY NOT NULL,
A TEXT NOT NULL,
B INT NOT NULL,
C CHAR(1) UNIQUE,
D REAL,
TIME DATE);
```

```
test1=# CREATE SCHEMA A;
CREATE SCHEMA
test1=# CREATE TABLE A.tables1(
test1(# ID SERIAL PRIMARY KEY NOT NULL,
test1(# A TEXT NOT NULL,
test1(# B INT NOT NULL,
test1(# C CHAR(1) UNIQUE,
test1(# D REAL,
test1(# TIME DATE);
CREATE TABLE
```

* 索引
> `CREATE UNIQUE INDEX A_INDEX ON A.TABLES1 (A);`

```
test1=# CREATE UNIQUE INDEX A_INDEX ON A.TABLES1 (A);
CREATE INDEX
```

* 别名
> `SELECT G.ID, G.A, G.B, G.C, G.D FROM TABLES1 AS G;`

```
test1=# SELECT G.ID, G.A, G.B, G.C, G.D FROM A.TABLES1 AS G;
 id | a | b | c | d 
----+---+---+---+---
(0 行记录)
```

---

* 开启事务
> `BEGIN;或者BEGIN TRANSACTION;`

```
test1=# BEGIN TRANSACTION;
BEGIN
```

* 插入

```
INSERT INTO A.tables1 
(A,B,C,D,TIME) 
VALUES 
(1, 2, 1, 4, '2020-02-14' ),
(1, 2, 2, 4, '2020-02-14' ),
(1, 2, 3, 4, '2020-02-14' ),
(1, 2, 4, 4, '2020-02-14' ),
(1, 2, 0, 4, '2020-02-13' );
```

```
test1=# INSERT INTO A.tables1 
(A,B,C,D,TIME) 
VALUES 
(1, 2, 1, 4, '2020-02-14' ),
(2, 2, 2, 4, '2020-02-14' ),
(3, 2, 3, 4, '2020-02-14' ),
(4, 2, 4, 4, '2020-02-14' ),
(0, 2, 0, 4, '2020-02-13' );
INSERT 0 5
```

* 更新
```
UPDATE A.TABLES1 SET A = 2 WHERE ID =1;
UPDATE A.TABLES1 SET A = 1 WHERE ID =1;
```

`SELECT * FROM A.TABLES1;`

```
test1=# SELECT * FROM A.TABLES1;
 id | a | b | c | d |    time    
----+---+---+---+---+------------
  3 | 1 | 2 | 1 | 4 | 2020-02-14
  4 | 2 | 2 | 2 | 4 | 2020-02-14
  5 | 3 | 2 | 3 | 4 | 2020-02-14
  6 | 4 | 2 | 4 | 4 | 2020-02-14
  7 | 0 | 2 | 0 | 4 | 2020-02-13
(5 行记录)
```

* 修改
```
ALTER TABLE A.TABLES1 ADD E CHAR(1);
ALTER TABLE A.TABLES1 ADD F CHAR(1);
```

```
test1=# ALTER TABLE A.TABLES1 ADD E CHAR(1);
ALTER TABLE
test1=# ALTER TABLE A.TABLES1 ADD F CHAR(1);
ALTER TABLE
```

`SELECT * FROM A.TABLES1;`

```
test1=# SELECT * FROM A.TABLES1;
 id | a | b | c | d |    time    | e | f 
----+---+---+---+---+------------+---+---
  3 | 1 | 2 | 1 | 4 | 2020-02-14 |   | 
  4 | 2 | 2 | 2 | 4 | 2020-02-14 |   | 
  5 | 3 | 2 | 3 | 4 | 2020-02-14 |   | 
  6 | 4 | 2 | 4 | 4 | 2020-02-14 |   | 
  7 | 0 | 2 | 0 | 4 | 2020-02-13 |   | 
(5 行记录)
```

* 锁
> `LOCK TABLE A.TABLES1 IN ACCESS EXCLUSIVE MODE;`

```
test1=# LOCK TABLE A.TABLES1 IN ACCESS EXCLUSIVE MODE;
LOCK TABLE
```

* 关闭事务
> `COMMIT;或者END TRANSACTION;`

```
test1=# END TRANSACTION;
COMMIT
```

---

* 查询表格是否存在
```
\d
\d A.table1
SELECT * FROM A.tables1;
```

```
test1=# \d A.TABLES1;
                                数据表 "a.tables1"
 栏位 |     类型     | 校对规则 |  可空的  |                 预设                  
------+--------------+----------+----------+---------------------------------------
 id   | integer      |          | not null | nextval('a.tables1_id_seq'::regclass)
 a    | text         |          | not null | 
 b    | integer      |          | not null | 
 c    | character(1) |          |          | 
 d    | real         |          |          | 
 time | date         |          |          | 
 e    | character(1) |          |          | 
 f    | character(1) |          |          | 
索引：
    "tables1_pkey" PRIMARY KEY, btree (id)
    "a_index" UNIQUE, btree (a)
    "tables1_c_key" UNIQUE CONSTRAINT, btree (c)
```

```
test1=# SELECT * FROM A.tables1;
 id | a | b | c | d |    time    | e | f 
----+---+---+---+---+------------+---+---
  3 | 1 | 2 | 1 | 4 | 2020-02-14 |   | 
  4 | 2 | 2 | 2 | 4 | 2020-02-14 |   | 
  5 | 3 | 2 | 3 | 4 | 2020-02-14 |   | 
  6 | 4 | 2 | 4 | 4 | 2020-02-14 |   | 
  7 | 0 | 2 | 0 | 4 | 2020-02-13 |   | 
(5 行记录)
```

---

* 删除
> `DROP SCHEMA A CASCADE;`
> `DROP TABLE TABLES1;`
> `DROP DATABASE TEST1;`

```
test1=# DROP SCHEMA A CASCADE;
注意:  递归删除 表 a.tables
```

```
postgres=# DROP DATABASE TEST1;
DROP DATABASE
```

---

