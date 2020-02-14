---
title: MySQL-3
date: 2020-02-14 20:36:41
tags: RDBMS
categories: [软件,数据库]
---

### MySQL-3

```
SHOW DATABASES;
CREATE DATABLE TEST1;
USE TEST1;
```
```
MariaDB [(none)]> CREATE DATABASE TEST1;
Query OK, 1 row affected (0.000 sec)

MariaDB [(none)]> USE TEST1;
Database changed
```

分别建立TABLES1,TABLES2(唯一键值)
```
CREATE TABLE TABLES1(
ID INT NOT NULL AUTO_INCREMENT,
A VARCHAR(100) NOT NULL,
B VARCHAR(100) NOT NULL,
C VARCHAR(100) NOT NULL,
D VARCHAR(100) NOT NULL,
TIME DATE,
PRIMARY KEY ( ID, A, B )
)ENGINE=InnoDB DEFAULT CHARSET=utf8;
```

---

```
CREATE TABLE TABLES2(
ID INT NOT NULL AUTO_INCREMENT,
A VARCHAR(100) NOT NULL,
B VARCHAR(100) NOT NULL,
C VARCHAR(100) NOT NULL,
D VARCHAR(100) NOT NULL,
TIME DATE,
UNIQUE ( ID, A, B )
)ENGINE=InnoDB DEFAULT CHARSET=utf8;
```

```
MariaDB [TEST1]> CREATE TABLE TABLES1(
    -> ID INT NOT NULL AUTO_INCREMENT,
    -> A VARCHAR(100) NOT NULL,
    -> B VARCHAR(100) NOT NULL,
    -> C VARCHAR(100) NOT NULL,
    -> D VARCHAR(100) NOT NULL,
    -> TIME DATE,
    -> PRIMARY KEY ( ID, A, B )
    -> )ENGINE=InnoDB DEFAULT CHARSET=utf8;
Query OK, 0 rows affected (0.061 sec)
```

```
MariaDB [TEST1]> CREATE TABLE TABLES2(
    -> ID INT NOT NULL AUTO_INCREMENT,
    -> A VARCHAR(100) NOT NULL,
    -> B VARCHAR(100) NOT NULL,
    -> C VARCHAR(100) NOT NULL,
    -> D VARCHAR(100) NOT NULL,
    -> TIME DATE,
    -> UNIQUE ( ID, A, B )
    -> )ENGINE=InnoDB DEFAULT CHARSET=utf8;
Query OK, 0 rows affected (0.006 sec)
```

---

**向TABLES1插入数据**
* 4
```
INSERT INTO TABLES1
(A,B,C,D,TIME)
VALUES
("1","2","3","4",NOW());
```
* 1
```
INSERT INTO TABLES1
(A,B,C,D,TIME)
VALUES
("2","3","4","5",'2020-02-13');
```

```
MariaDB [TEST1]> INSERT INTO TABLES1
    -> (A,B,C,D,TIME)
    -> VALUES
    -> ("1","2","3","4",NOW());
Query OK, 1 row affected, 1 warning (0.003 sec)

MariaDB [TEST1]> INSERT INTO TABLES1 (A,B,C,D,TIME) VALUES ("1","2","3","4",NOW());
Query OK, 1 row affected, 1 warning (0.001 sec)

MariaDB [TEST1]> INSERT INTO TABLES1 (A,B,C,D,TIME) VALUES ("1","2","3","4",NOW());
Query OK, 1 row affected, 1 warning (0.001 sec)

MariaDB [TEST1]> INSERT INTO TABLES1 (A,B,C,D,TIME) VALUES ("1","2","3","4",NOW());
Query OK, 1 row affected, 1 warning (0.001 sec)

MariaDB [TEST1]> INSERT INTO TABLES1
    -> (A,B,C,D,TIME)
    -> VALUES
    -> ("2","3","4","5",'2020-02-13');
Query OK, 1 row affected (0.002 sec)
```

---

**复制TABLES1内数据到TABLES2**
```
INSERT INTO TABLES2 (ID,A,B,C,D,TIME)
SELECT ID,A,B,C,D,TIME
FROM TABLES1;
```

```
MariaDB [TEST1]> INSERT INTO TABLES2 (ID,A,B,C,D,TIME)
    -> SELECT ID,A,B,C,D,TIME
    -> FROM TABLES1;
Query OK, 5 rows affected (0.001 sec)
Records: 5  Duplicates: 0  Warnings: 0
```

---

**复制TABLES1内数据到TABLES3**
* 查看标结构
> `SHOW CREATE TABLE TABLES1 \G;`

**将表内结构规划语句拷贝并执行,并命名为TABLES3**
**复制数据**
```
INSERT INTO TABLES3 (ID,A,B,C,D,TIME)
SELECT ID,A,B,C,D,TIME
FROM TABLES1;
```
```
MariaDB [TEST1]> SHOW CREATE TABLE TABLES1 \G;
*************************** 1. row ***************************
       Table: TABLES1
Create Table: CREATE TABLE `TABLES1` (
  `ID` int(11) NOT NULL AUTO_INCREMENT,
  `A` varchar(100) NOT NULL,
  `B` varchar(100) NOT NULL,
  `C` varchar(100) NOT NULL,
  `D` varchar(100) NOT NULL,
  `TIME` date DEFAULT NULL,
  PRIMARY KEY (`ID`,`A`,`B`)
) ENGINE=InnoDB AUTO_INCREMENT=6 DEFAULT CHARSET=utf8
1 row in set (0.000 sec)

ERROR: No query specified
```

```
CREATE TABLE `TABLES3` (
  `ID` int(11) NOT NULL AUTO_INCREMENT,
  `A` varchar(100) NOT NULL,
  `B` varchar(100) NOT NULL,
  `C` varchar(100) NOT NULL,
  `D` varchar(100) NOT NULL,
  `TIME` date DEFAULT NULL,
  PRIMARY KEY (`ID`,`A`,`B`)
) ENGINE=InnoDB AUTO_INCREMENT=6 DEFAULT CHARSET=utf8
;
```

```
MariaDB [TEST1]> CREATE TABLE `TABLES3` (
    ->   `ID` int(11) NOT NULL AUTO_INCREMENT,
    ->   `A` varchar(100) NOT NULL,
    ->   `B` varchar(100) NOT NULL,
    ->   `C` varchar(100) NOT NULL,
    ->   `D` varchar(100) NOT NULL,
    ->   `TIME` date DEFAULT NULL,
    ->   PRIMARY KEY (`ID`,`A`,`B`)
    -> ) ENGINE=InnoDB AUTO_INCREMENT=6 DEFAULT CHARSET=utf8;
Query OK, 0 rows affected (0.042 sec)
```

```
INSERT INTO TABLES3 (ID,A,B,C,D,TIME)
SELECT ID,A,B,C,D,TIME
FROM TABLES1;
```

---

`SHOW TABLES;`
```
MariaDB [TEST1]> SHOW TABLES;
+-----------------+
| Tables_in_TEST1 |
+-----------------+
| TABLES1         |
| TABLES2         |
| TABLES3         |
+-----------------+
3 rows in set (0.000 sec)
```

```
SELECT * FROM TABLES1;
SELECT * FROM TABLES2;
SELECT * FROM TABLES3;
```

```
MariaDB [TEST1]> SELECT * FROM TABLES1;
+----+---+---+---+---+------------+
| ID | A | B | C | D | TIME       |
+----+---+---+---+---+------------+
|  1 | 1 | 2 | 3 | 4 | 2020-02-14 |
|  2 | 1 | 2 | 3 | 4 | 2020-02-14 |
|  3 | 1 | 2 | 3 | 4 | 2020-02-14 |
|  4 | 1 | 2 | 3 | 4 | 2020-02-14 |
|  5 | 2 | 3 | 4 | 5 | 2020-02-13 |
+----+---+---+---+---+------------+
5 rows in set (0.000 sec)
```

```
MariaDB [TEST1]> SELECT * FROM TABLES2;
+----+---+---+---+---+------------+
| ID | A | B | C | D | TIME       |
+----+---+---+---+---+------------+
|  1 | 1 | 2 | 3 | 4 | 2020-02-14 |
|  2 | 1 | 2 | 3 | 4 | 2020-02-14 |
|  3 | 1 | 2 | 3 | 4 | 2020-02-14 |
|  4 | 1 | 2 | 3 | 4 | 2020-02-14 |
|  5 | 2 | 3 | 4 | 5 | 2020-02-13 |
+----+---+---+---+---+------------+
5 rows in set (0.000 sec)
```

```
MariaDB [TEST1]> SELECT * FROM TABLES3;
+----+---+---+---+---+------------+
| ID | A | B | C | D | TIME       |
+----+---+---+---+---+------------+
|  1 | 1 | 2 | 3 | 4 | 2020-02-14 |
|  2 | 1 | 2 | 3 | 4 | 2020-02-14 |
|  3 | 1 | 2 | 3 | 4 | 2020-02-14 |
|  4 | 1 | 2 | 3 | 4 | 2020-02-14 |
|  5 | 2 | 3 | 4 | 5 | 2020-02-13 |
+----+---+---+---+---+------------+
5 rows in set (0.000 sec)
```

---

**统计表TABLES1内A列与B列中重复的数据**

```
SELECT COUNT(*) as repetitions, A, B
FROM TABLES1
GROUP BY A, B
HAVING repetitions > 1;
```

```
MariaDB [TEST1]> SELECT COUNT(*) as repetitions, A, B
    -> FROM TABLES1
    -> GROUP BY A, B
    -> HAVING repetitions > 1;
+-------------+---+---+
| repetitions | A | B |
+-------------+---+---+
|           4 | 1 | 2 |
+-------------+---+---+
1 row in set (0.000 sec)
```

---

**过滤重复数据并输出TABLES1内数据**
```
SELECT DISTINCT A, B
FROM TABLES1;
或
SELECT A, B
FROM TABLES2
GROUP BY (C);
```

```
MariaDB [TEST1]> SELECT DISTINCT A, B
    -> FROM TABLES1;
+---+---+
| A | B |
+---+---+
| 1 | 2 |
| 2 | 3 |
+---+---+
2 rows in set (0.000 sec)

MariaDB [TEST1]> SELECT A, B
    -> FROM TABLES2
    -> GROUP BY (C);
+---+---+
| A | B |
+---+---+
| 1 | 2 |
| 2 | 3 |
+---+---+
2 rows in set (0.001 sec)
```

---

**删除TABLES1内重复数据**
```
CREATE TABLE tmp SELECT A, B, C, D FROM TABLES1 GROUP BY (C);
DROP TABLE TABLES1;
ALTER TABLE tmp RENAME TO TABLES1;
```

```
MariaDB [TEST1]> CREATE TABLE tmp SELECT A, B, C, D FROM TABLES1 GROUP BY (C);
Query OK, 2 rows affected (0.027 sec)
Records: 2  Duplicates: 0  Warnings: 0

MariaDB [TEST1]> DROP TABLE TABLES1;
Query OK, 0 rows affected (0.002 sec)

MariaDB [TEST1]> ALTER TABLE tmp RENAME TO TABLES1;
Query OK, 0 rows affected (0.002 sec)
```

`SELECT * FROM TABLES1;`

```
MariaDB [TEST1]> SELECT * FROM TABLES1;
+---+---+---+---+
| A | B | C | D |
+---+---+---+---+
| 1 | 2 | 3 | 4 |
| 2 | 3 | 4 | 5 |
+---+---+---+---+
2 rows in set (0.000 sec)
```

---

**或设置主键以清理TABLEST2内重复数据**
```
ALTER IGNORE TABLE TABLES2
ADD PRIMARY KEY (A, B);
```

```
MariaDB [TEST1]> ALTER IGNORE TABLE TABLES2
    -> ADD PRIMARY KEY (A, B);
Query OK, 5 rows affected (0.059 sec)              
Records: 5  Duplicates: 3  Warnings: 0
```

`SELECT * FROM TABLES2;`

```
MariaDB [TEST1]> SELECT * FROM TABLES2;
+----+---+---+---+---+------------+
| ID | A | B | C | D | TIME       |
+----+---+---+---+---+------------+
|  1 | 1 | 2 | 3 | 4 | 2020-02-14 |
|  5 | 2 | 3 | 4 | 5 | 2020-02-13 |
+----+---+---+---+---+------------+
2 rows in set (0.000 sec)
```


