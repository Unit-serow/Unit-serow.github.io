---
title: SQL-2
date: 2020-02-13 13:34:51
tags: 随笔
categories: [软件,数据库]
---

### SQL-GURD

* 增/删/改/查

**增:**
* INSERT INTO 语句
* 基本插入语句
* 语法一(不指定列名):
```
INSERT INTO table_name
VALUES (value1,value2,value3,...);
```
* 语法二(指定列名):
```
INSERT INTO table_name (column1,column2,column3,...)
VALUES (value1,value2,value3,...);
```

---

**删:**
* DELETE 语句
* 基本删除语句
* 语法:
```
DELETE FROM table_name
WHERE some_column=some_value;
```
* 如果未对WHERE语句进行规定，所有的记录都会被删除

---

**改:**
* UPDATE 语句
* 基本修改(更新)语句
* 语法:
```
UPDATE table_name
SET column1=value1,column2=value2,...
WHERE some_column=some_value;
```
> uptate 表名
> set 列名=指定值...
> where 过滤规则
* 如果未对WHERE语句进行规定，所有的记录都会被更新

---

**查:**
* SELECT 语句
* 基本查询语句
* 语法:
```
SELECT column_name,column_name 
FROM table_name;
```
```
SELECT * FROM table_name;
SELECT 表名 FROM 表内指定列
```

* DISTINCT 关键字
* 常用于`SELECT DISTINCT`
* 返回所选被查询列中唯一不同(distinct)的值(筛选列内重复值并进行排除)
* 语法:
```
SELECT DISTINCT column_name,column_name 
FROM table_name;
```

---

### 条件语句:

**WHERE 子句**
* 用于配置所选执行语句的过滤条件
* 语法:
```
SELECT column_name,column_name 
FROM table_name
WHERE column_name operator value;
```
* WHERE子句中的运算符:

|运算符|描述|
|:----|:----|
|=|等于|
|<>,!=|不等于|
|>|大于|
|<|小于|
|>=|大于等于|
|<=|小于等于|
|BETWEEN|在某个范围内|
|LIKE|搜索某种模式|
|IN|指定针对某个列的多个可能值|

---

**LIKE 操作符**
* 用于在WHERE子句中搜索列中搜索列的指定模式
* 语法:
```
SELECT column_name(s)
FROM table_name
WHERE column_name LIKE pattern;
```

---

**SQL函数参考:**

|函数|描述|
|:----|:----|
|AVG|平均值|
|COUNT|计数(不含Null)|
|FIRST|第一个记录的值|
|MAX|最大值|
|MIN|最小值|
|STDEV|样本标准差|
|STDEVP|总体标准差|
|SUM|求和|
|VAR|样本方差|
|VARP|总体方差|
|UCASE|转化为全大写字母|
|LCASE|转化为全小写字母|
|MID|取中值|
|LEN|计算字符串长度|
|INSTR|获得子字符串在母字符串的起始位置|
|LEFT|取字符串左边子串|
|RIGHT|取字符串右边子串|
|ROUND|数值四舍五入取整|
|MOD|取余|
|NOW|获得当前时间的值|
|FORMAT|字符串格式化|
|DATEDIFF|获得两个时间的差值|

---

