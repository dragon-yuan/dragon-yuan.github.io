---
title: MySQL子查询
categories:
  - MySQL
date: 2017-07-16 13:50:22
---
子查询：
通常在一个SELECT、UPDATE或DELETE语句的WHERE子句中充当查询、修改或删除的条件。
例如：在子查询中使用ORDER BY 子句，将查询结果按照deptno列降序输出。
```sql
SELECT empno, ename, sal, d.deptno FROM scott.emp WHERE deptno IN
(
SELECT deptno FROM scott.emp WHERE empno>7782
)
ORDER BY empno DESC;
```

例：
查询出每个部门的编号，名称，位置，部门人数，平均工资
```sql
SELECT d.deptno,d.dname,d.loc,
  (SELECT  COUNT(empno) FROM emp WHERE emp.deptno=d.deptno GROUP BY deptno)
  con,
  (SELECT AVG(sal) FROM emp WHERE emp.deptno=d.deptno GROUP BY deptno)
  avgsal
FROM dept d
```
