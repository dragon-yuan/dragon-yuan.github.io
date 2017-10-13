---
title: SQL中UNION和UNION ALL操作符
categories:
  - Java
date: 2017-10-11 22:22:29
---
UNION操作符用于合并两个或多个SELECT语句的结果集。
UNION内部的SELECT语句必须拥有相同数量的列。列也必须拥有相似的数据类型。
同时，每条SELECT语句中的列的顺序必须相同。
UNION操作符选取的是不同的值。如需要重复的值，需要用UNION ALL。
```sql
SELECT column_name(s) FROM table_name1
UNION
SELECT column_name(s) FROM table_name2
```