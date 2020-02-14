---
title: MySQL-2
date: 2020-02-14 17:19:48
tags: RDBMS
categories: [软件,数据库]
---

### MySQL-2

**创建并选取数据库**
```
MariaDB [(none)]> CREATE DATABASE TEST1;
Query OK, 1 row affected (0.000 sec)
```

```
MariaDB [(none)]> USE TEST1;
Database changed
```

**创建临时表TABLEST6**
`CREATE TEMPORARY TABLE TABLES6 (B INT, C CHAR(1) );`
```
MariaDB [TEST1]> CREATE TEMPORARY TABLE TABLES6 (B INT, C CHAR(1) );
Query OK, 0 rows affected (0.001 sec)
```

---

**向表内插入字段**
```
ALTER TABLE TABLES6 ADD A INT FIRST;
ALTER TABLE TABLES6 ADD D INT AFTER C;
ALTER TABLE TABLES6 ADD E CHAR AFTER D;
ALTER TABLE TABLES6 ADD G CHAR AFTER E;
```

```
MariaDB [TEST1]> ALTER TABLE TABLES6 ADD A INT FIRST;
Query OK, 0 rows affected (0.001 sec)              
Records: 0  Duplicates: 0  Warnings: 0

MariaDB [TEST1]> ALTER TABLE TABLES6 ADD D INT AFTER C;
Query OK, 0 rows affected (0.001 sec)              
Records: 0  Duplicates: 0  Warnings: 0

MariaDB [TEST1]> ALTER TABLE TABLES6 ADD E CHAR AFTER D;
Query OK, 0 rows affected (0.001 sec)              
Records: 0  Duplicates: 0  Warnings: 0

MariaDB [TEST1]> ALTER TABLE TABLES6 ADD G CHAR AFTER E;
Query OK, 0 rows affected (0.001 sec)              
Records: 0  Duplicates: 0  Warnings: 0
```

**查看表结构**
`SHOW COLUMNS FROM TABLES6;`
```
MariaDB [TEST1]> SHOW COLUMNS FROM TABLES6;
+-------+---------+------+-----+---------+-------+
| Field | Type    | Null | Key | Default | Extra |
+-------+---------+------+-----+---------+-------+
| A     | int(11) | YES  |     | NULL    |       |
| B     | int(11) | YES  |     | NULL    |       |
| C     | char(1) | YES  |     | NULL    |       |
| D     | int(11) | YES  |     | NULL    |       |
| E     | char(1) | YES  |     | NULL    |       |
| G     | char(1) | YES  |     | NULL    |       |
+-------+---------+------+-----+---------+-------+
6 rows in set (0.001 sec)
```

---

**修改字符类型**
```
ALTER TABLE TABLES6 MODIFY A INT(10);
ALTER TABLE TABLES6 MODIFY B INT(10);
ALTER TABLE TABLES6 MODIFY C INT(10);
ALTER TABLE TABLES6 MODIFY D CHAR(10);
ALTER TABLE TABLES6 MODIFY E CHAR(10);
ALTER TABLE TABLES6 MODIFY G CHAR(10);
```
```
MariaDB [TEST1]> ALTER TABLE TABLES6 MODIFY A INT(10);
Query OK, 0 rows affected (0.001 sec)              
Records: 0  Duplicates: 0  Warnings: 0

MariaDB [TEST1]> ALTER TABLE TABLES6 MODIFY B INT(10);
Query OK, 0 rows affected (0.000 sec)              
Records: 0  Duplicates: 0  Warnings: 0

MariaDB [TEST1]> ALTER TABLE TABLES6 MODIFY C INT(10);
Query OK, 0 rows affected (0.001 sec)              
Records: 0  Duplicates: 0  Warnings: 0

MariaDB [TEST1]> ALTER TABLE TABLES6 MODIFY D CHAR(10);
Query OK, 0 rows affected (0.001 sec)              
Records: 0  Duplicates: 0  Warnings: 0

MariaDB [TEST1]> ALTER TABLE TABLES6 MODIFY E CHAR(10);
Query OK, 0 rows affected (0.001 sec)              
Records: 0  Duplicates: 0  Warnings: 0

MariaDB [TEST1]> ALTER TABLE TABLES6 MODIFY G CHAR(10);
Query OK, 0 rows affected (0.001 sec)              
Records: 0  Duplicates: 0  Warnings: 0
```
**查看表结构**
`SHOW COLUMNS FROM TABLES6;`
```
MariaDB [TEST1]> SHOW COLUMNS FROM TABLES6;
+-------+----------+------+-----+---------+-------+
| Field | Type     | Null | Key | Default | Extra |
+-------+----------+------+-----+---------+-------+
| A     | int(10)  | YES  |     | NULL    |       |
| B     | int(10)  | YES  |     | NULL    |       |
| C     | int(10)  | YES  |     | NULL    |       |
| D     | char(10) | YES  |     | NULL    |       |
| E     | char(10) | YES  |     | NULL    |       |
| G     | char(10) | YES  |     | NULL    |       |
+-------+----------+------+-----+---------+-------+
6 rows in set (0.001 sec)
```

---

**修改字段名称**
```
ALTER TABLE TABLES6 CHANGE G F BIGINT;
ALTER TABLE TABLES6 CHANGE F F CHAR(10);
```

```
MariaDB [TEST1]> ALTER TABLE TABLES6 CHANGE G F BIGINT;
Query OK, 0 rows affected (0.001 sec)              
Records: 0  Duplicates: 0  Warnings: 0

MariaDB [TEST1]> ALTER TABLE TABLES6 CHANGE F F CHAR(10);
Query OK, 0 rows affected (0.001 sec)              
Records: 0  Duplicates: 0  Warnings: 0
```

---

**修改默认值**
```
ALTER TABLE TABLES6
MODIFY D BIGINT NOT NULL DEFAULT 1000;
```
```
ALTER TABLE TABLES6
MODIFY E BIGINT NOT NULL DEFAULT 1000;
```
```
ALTER TABLE TABLES6
MODIFY F BIGINT NOT NULL DEFAULT 100;
```
`ALTER TABLE TABLES6 ALTER F SET DEFAULT 1000;`

```
MariaDB [TEST1]> ALTER TABLE TABLES6
    -> MODIFY D BIGINT NOT NULL DEFAULT 1000;
Query OK, 0 rows affected (0.001 sec)              
Records: 0  Duplicates: 0  Warnings: 0

MariaDB [TEST1]> ALTER TABLE TABLES6
    -> MODIFY E BIGINT NOT NULL DEFAULT 1000;
Query OK, 0 rows affected (0.001 sec)              
Records: 0  Duplicates: 0  Warnings: 0

MariaDB [TEST1]> ALTER TABLE TABLES6
    -> MODIFY F BIGINT NOT NULL DEFAULT 100;
Query OK, 0 rows affected (0.001 sec)              
Records: 0  Duplicates: 0  Warnings: 0

MariaDB [TEST1]> ALTER TABLE TABLES6 ALTER F SET DEFAULT 1000;
Query OK, 0 rows affected (0.001 sec)              
Records: 0  Duplicates: 0  Warnings: 0
```

**查看表结构**
`SHOW COLUMNS FROM TABLES6;`
```
MariaDB [TEST1]> SHOW COLUMNS FROM TABLES6;
+-------+------------+------+-----+---------+-------+
| Field | Type       | Null | Key | Default | Extra |
+-------+------------+------+-----+---------+-------+
| A     | int(10)    | YES  |     | NULL    |       |
| B     | int(10)    | YES  |     | NULL    |       |
| C     | int(10)    | YES  |     | NULL    |       |
| D     | bigint(20) | NO   |     | 1000    |       |
| E     | bigint(20) | NO   |     | 1000    |       |
| F     | bigint(20) | NO   |     | 1000    |       |
+-------+------------+------+-----+---------+-------+
6 rows in set (0.002 sec)
```

---

**修改表TABLES6的存储引擎**
`ALTER TABLE TABLES6 ENGINE = MYISAM;`
```
MariaDB [TEST1]> ALTER TABLE TABLES6 ENGINE = MYISAM;
Query OK, 0 rows affected (0.001 sec)              
Records: 0  Duplicates: 0  Warnings: 0
```

---

**查看存储结构**
`SHOW TABLE STATUS LIKE 'TABLES6';`
```
MariaDB [TEST1]> SHOW TABLE STATUS LIKE 'TABLES6';
Empty set (0.000 sec)
```

---

**修改TABLES6为TABLES4**
`ALTER TABLE TABLES6 RENAME TO TABLES4;`
```
MariaDB [TEST1]> ALTER TABLE TABLES6 RENAME TO TABLES4;
Query OK, 0 rows affected (0.000 sec)
```

---

**创建索引并删除多余索引**
```
ALTER TABLE TABLES4 ADD INDEX (B);
ALTER TABLE TABLES4 ADD INDEX (A);
ALTER TABLE TABLES4 DROP INDEX B;
```
```
MariaDB [TEST1]> ALTER TABLE TABLES4 ADD INDEX (B);
Query OK, 0 rows affected (0.001 sec)              
Records: 0  Duplicates: 0  Warnings: 0

MariaDB [TEST1]> ALTER TABLE TABLES4 ADD INDEX (A);
Query OK, 0 rows affected (0.002 sec)              
Records: 0  Duplicates: 0  Warnings: 0

MariaDB [TEST1]> ALTER TABLE TABLES4 DROP INDEX B;
Query OK, 0 rows affected (0.002 sec)              
Records: 0  Duplicates: 0  Warnings: 0
```

---

**设A为主键(作为主键索引,A值不能为空)**
```
ALTER TABLE TABLES4 MODIFY A INT NOT NULL;
ALTER TABLE TABLES4 ADD PRIMARY KEY (B);
ALTER TABLE TABLES4 DROP PRIMARY KEY;
ALTER TABLE TABLES4 ADD PRIMARY KEY (A);
```
```
MariaDB [TEST1]> ALTER TABLE TABLES4 ADD PRIMARY KEY (B);
Query OK, 0 rows affected (0.001 sec)              
Records: 0  Duplicates: 0  Warnings: 0

MariaDB [TEST1]> ALTER TABLE TABLES4 DROP PRIMARY KEY;
Query OK, 0 rows affected (0.001 sec)              
Records: 0  Duplicates: 0  Warnings: 0

MariaDB [TEST1]> ALTER TABLE TABLES4 ADD PRIMARY KEY (A);
Query OK, 0 rows affected (0.001 sec)              
Records: 0  Duplicates: 0  Warnings: 0
```

---

**列出索引**
`SHOW INDEX FROM TABLES4;`

```
MariaDB [TEST1]> SHOW INDEX FROM TABLES4;
+---------+------------+----------+--------------+-------------+-----------+-------------+----------+--------+------+------------+---------+---------------+
| Table   | Non_unique | Key_name | Seq_in_index | Column_name | Collation | Cardinality | Sub_part | Packed | Null | Index_type | Comment | Index_comment |
+---------+------------+----------+--------------+-------------+-----------+-------------+----------+--------+------+------------+---------+---------------+
| TABLES4 |          0 | PRIMARY  |            1 | A           | A         |           0 |     NULL | NULL   |      | BTREE      |         |               |
| TABLES4 |          1 | A        |            1 | A           | A         |        NULL |     NULL | NULL   |      | BTREE      |         |               |
+---------+------------+----------+--------------+-------------+-----------+-------------+----------+--------+------+------------+---------+---------------+
2 rows in set (0.000 sec)
```

---

**删除TABLES4**
`DROP TABLE TABLES4;`

```
MariaDB [TEST1]> DROP TABLE TABLES4;
Query OK, 0 rows affected (0.000 sec)
```

---


