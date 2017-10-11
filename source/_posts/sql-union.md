---
title: SQL UNION和UNION ALL操作符
categories:
  - Java
date: 2017-10-11 22:22:29
---
UNION操作符用于合并两个或多个SELECT语句的结果集。
UNION内部的 SELECT语句必须拥有相同数量的列。列也必须拥有相似的数据类型。
同时，每条 SELECT语句中的列的顺序必须相同。
UNION操作符选取不同的值。如果允许重复的值，请使用 UNION ALL。
```sql
SELECT column_name(s) FROM table_name1
UNION
SELECT column_name(s) FROM table_name2
```