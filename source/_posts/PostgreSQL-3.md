---
title: PostgreSQL-3
date: 2020-02-16 04:02:03
tags: [随笔,ORDBMS]
categories: [软件,数据库]
---

### PostgreSQL-3

**TABLES1数据结构**

```
ID  A  B  C  D  TIME
 1  1  1 2020-02-16
 2  2  2 2020-02-16
 3  3  3 2020-02-16 -
 4  1  4 2020-02-16
 5  2  1 2020-02-16
 6  2  7 2020-02-16
 7  3  7 2020-02-16
 8  1  8 2020-02-16
 9  4  1 2020-02-16
10 4  6 2020-02-16
11 1  3 2020-02-16
12 2  2 2020-02-17 -
13 4  9 2020-02-16 -
```

---

> 创建并连接

```
CREATE DATABASE TEST;
\c test;
```

```
postgres=# CREATE DATABASE TEST;
CREATE DATABASE
```

```
postgres=# \c test;
您现在已经连接到数据库 "test",用户 "postgres".
```

> 创建A类表TABLES1

```
CREATE SCHEMA A
CREATE TABLE A.TABLES1 (
ID SERIAL PRIMARY KEY NOT NULL,
A INT NOT NULL, 
B INT NOT NULL,
C INT NOT NULL,
D INT NOT NULL,
TIME DATE);
```

```
test-# CREATE TABLE A.TABLES1 (
test(# ID SERIAL PRIMARY KEY NOT NULL,
test(# A INT NOT NULL, 
test(# B INT NOT NULL,
test(# C INT NOT NULL,
test(# D INT NOT NULL,
test(# TIME DATE);
CREATE SCHEMA
```

---

> 向A类表TABLES1内插入数据

```
INSERT INTO A.TABLES1
(A,B,C,D,TIME)
VALUES
(1, 1, 2, 3, '2020-02-16'),
(2, 2, 4, 6, '2020-02-16'),
(3, 3, 9, 2, '2020-02-16'),
(1, 4, 8, 3, '2020-02-16'),
(2, 1, 1, 1, '2020-02-16'),
(2, 7, 5, 2, '2020-02-16'),
(3, 7, 3, 6, '2020-02-16'),
(1, 8, 7, 7, '2020-02-16'),
(4, 1, 7, 8, '2020-02-16'),
(4, 6, 1, 9, '2020-02-16'),
(1, 3, 8, 1, '2020-02-16'),
(2, 2, 4, 5, '2020-02-17'),
(4, 9, 6, 7, '2020-02-16');
```

```
test=# INSERT INTO A.TABLES1
test-# (A,B,C,D,TIME)
test-# VALUES
test-# (1, 1, 2, 3, '2020-02-16'),
test-# (2, 2, 4, 6, '2020-02-16'),
test-# (3, 3, 9, 2, '2020-02-16'),
test-# (1, 4, 8, 3, '2020-02-16'),
test-# (2, 1, 1, 1, '2020-02-16'),
test-# (2, 7, 5, 2, '2020-02-16'),
test-# (3, 7, 3, 6, '2020-02-16'),
test-# (1, 8, 7, 7, '2020-02-16'),
test-# (4, 1, 7, 8, '2020-02-16'),
test-# (4, 6, 1, 9, '2020-02-16'),
test-# (1, 3, 8, 1, '2020-02-16'),
test-# (2, 2, 4, 5, '2020-02-17'),
test-# (4, 9, 6, 7, '2020-02-16');
INSERT 0 13
```

`SELECT * FROM A.TABLES1;`

```
test=# SELECT * FROM A.TABLES1;
 id | a | b | c | d |    time    
----+---+---+---+---+------------
  1 | 1 | 1 | 2 | 3 | 2020-02-16
  2 | 2 | 2 | 4 | 6 | 2020-02-16
  3 | 3 | 3 | 9 | 2 | 2020-02-16
  4 | 1 | 4 | 8 | 3 | 2020-02-16
  5 | 2 | 1 | 1 | 1 | 2020-02-16
  6 | 2 | 7 | 5 | 2 | 2020-02-16
  7 | 3 | 7 | 3 | 6 | 2020-02-16
  8 | 1 | 8 | 7 | 7 | 2020-02-16
  9 | 4 | 1 | 7 | 8 | 2020-02-16
 10 | 4 | 6 | 1 | 9 | 2020-02-16
 11 | 1 | 3 | 8 | 1 | 2020-02-16
 12 | 2 | 2 | 4 | 5 | 2020-02-17
 13 | 4 | 9 | 6 | 7 | 2020-02-16
(13 行记录)
```

---

> 复制A类表TABLES1结构与表内数据于TABLES2

`SELECT * FROM TABLES2;`

```
test=# SELECT * FROM A.TABLES2;
 id | a | b | c | d |    time    
----+---+---+---+---+------------
  1 | 1 | 1 | 2 | 3 | 2020-02-16
  2 | 2 | 2 | 4 | 6 | 2020-02-16
  3 | 3 | 3 | 9 | 2 | 2020-02-16
  4 | 1 | 4 | 8 | 3 | 2020-02-16
  5 | 2 | 1 | 1 | 1 | 2020-02-16
  6 | 2 | 7 | 5 | 2 | 2020-02-16
  7 | 3 | 7 | 3 | 6 | 2020-02-16
  8 | 1 | 8 | 7 | 7 | 2020-02-16
  9 | 4 | 1 | 7 | 8 | 2020-02-16
 10 | 4 | 6 | 1 | 9 | 2020-02-16
 11 | 1 | 3 | 8 | 1 | 2020-02-16
 12 | 2 | 2 | 4 | 5 | 2020-02-17
 13 | 4 | 9 | 6 | 7 | 2020-02-16
(13 行记录)
```

---

> 输出A类表TABLES1与A类表TABLES2内ID等于6或3与7或4的行

```
SELECT * FROM A.TABLES1 WHERE ID=6 OR ID=3
UNION
SELECT * FROM A.TABLES2 WHERE ID=7 OR ID=4;
```

`SELECT * FROM A.TABLES1 WHERE ID=6 OR ID=3 UNION SELECT * FROM A.TABLES2 WHERE ID=7 OR ID=4;`

```
test=# SELECT * FROM A.TABLES1 WHERE ID=6 OR ID=3              
UNION
SELECT * FROM A.TABLES2 WHERE ID=7 OR ID=4;
 id | a | b | c | d |    time    
----+---+---+---+---+------------
  6 | 2 | 7 | 5 | 2 | 2020-02-16
  3 | 3 | 3 | 9 | 2 | 2020-02-16
  4 | 1 | 4 | 8 | 3 | 2020-02-16
  7 | 3 | 7 | 3 | 6 | 2020-02-16
(4 行记录)
```

---

> 输出并查询A类表TABLES1内ID等于3或等于4的行

`SELECT * FROM A.TABLES1 WHERE ID=3 OR ID=4;`

```
test=# SELECT * FROM A.TABLES1 WHERE ID=3 OR ID=4;
 id | a | b | c | d |    time    
----+---+---+---+---+------------
  3 | 3 | 3 | 9 | 2 | 2020-02-16
  4 | 1 | 4 | 8 | 3 | 2020-02-16
(2 行记录)
```

---

> 以偏移量为三为前提，输出并查询A类表TABLES1内的三条数据

`SELECT * FROM A.TABLES1 LIMIT 3 OFFSET 3;`

```
test=# SELECT * FROM A.TABLES1 LIMIT 3 OFFSET 3;
 id | a | b | c | d |    time    
----+---+---+---+---+------------
  4 | 1 | 4 | 8 | 3 | 2020-02-16
  5 | 2 | 1 | 1 | 1 | 2020-02-16
  6 | 2 | 7 | 5 | 2 | 2020-02-16
(3 行记录)
```

---

> 以偏移量为一为前提与排除所有重复数据为前提，输出并查询A类表TABLES1内的四条数据

`SELECT DISTINCT A,B,C FROM A.TABLES1 LIMIT 4 OFFSET 1;`

```
test=# SELECT DISTINCT A,B,C FROM A.TABLES1 LIMIT 4 OFFSET 1;
 a | b | c 
---+---+---
 1 | 3 | 8
 2 | 1 | 1
 2 | 7 | 5
 1 | 1 | 2
(4 行记录)
```

---

> 将A类表TABLES1内B列的结果基于A列进行分组并求和，分组数量小于10且为降序输出

```
SELECT A, SUM(B) FROM A.TABLES1 
GROUP BY A 
HAVING count(A) < 10 
ORDER BY A DESC;
```

`SELECT A, SUM(B) FROM A.TABLES1 GROUP BY A HAVING count(A) < 10 ORDER BY A DESC;`

```
test=# SELECT A, SUM(B) FROM A.TABLES1 GROUP BY A HAVING count(A) < 10 ORDER BY A DESC;
 a | sum 
---+-----
 4 |  16
 3 |  10
 2 |  12
 1 |  16
(4 行记录)
```

* 执行逻辑
1. 将B映射于A，并对A的数值类型进行分组
2. SUM()函数将B中映射于A的数值进行求和
3. 降序输出且组的数量不能大于10

---

> 删除两表内所有数据
`TRUNCATE TABLE A.TABLES1;`

```
test=# TRUNCATE TABLE A.TABLES1;
TRUNCATE TABLE
```

`TRUNCATE A.TABLES2;`

```
test=# TRUNCATE TABLE A.TABLES2;
TRUNCATE TABLE
```

`DROP TABLE A.TABLES1;`

`DROP TABLE A.TABLES2;`

```
test=# DROP TABLE A.TABLES1;
DROP TABLE
```

```
test=# DROP TABLE A.TABLES2;
DROP TABLE
```

`DROP DATABASE TEST;`

```
postgres=# DROP DATABASE TEST;
DROP DATABASE
```

---

* 没必要去设计特别复杂的逻辑语句,有时适当分句往往能提高工作效率

---

**相关概念:**

|概念|作用|
|:----|:----|
|SELECT|查询|
|FROM|来源于...|
|DISTINCT|唯一|
|WHERE|条件|
|AND&OR|逻辑与和逻辑或|
|LIKE|类似于...|
|LIMIT|限制查询结果的输出数量|
|OFFSET|查询结果偏移|
|ORDER BY (ASC/DESC)|排序|
|GROUP BY|分组|
|HAVING|分组之上再设置分组条件|
|WITH|子句封装，将使用指令进行封装以便一键执行|
|UNION|连接|
|VIEW|创建视图|
|WHERE可以嵌套查询语句|所执行嵌套的语句被称为内部查询/子查询|
|内聚函数|可以称为内置函数|
|TRUNCATE TABLE|删除表数据|

---

**常用内聚函数参考**

* COUNT 函数:用于计算数据库表中的行数
* MAX 函数:用于查询某一特定列中最大值
* MIN 函数:用于查询某一特定列中最小值
* AVG 函数:用于计算某一特定列中平均值
* SUM 函数:用于计算数字列所有值的总和
* ARRAY 函数:用于输入值(包括null)添加到数组中
* Numeric 函数:完整列出一个SQL中所需的操作数的函数
* String 函数:完整列出一个SQL中所需的操作字符的函数

**其他函数类型**

* 数学函数
* 三角函数
* 字符函数
* 操作符函数
* 类型转换函数

---
