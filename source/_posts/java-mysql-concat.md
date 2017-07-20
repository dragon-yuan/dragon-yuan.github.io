---
title: MySQL中CONCAT值为空的问题解决办法
categories:
  - MySQL
date: 2017-07-10 22:12:26
---
```sql
在MySQL中concat函数有一个特点就是有一个值为null那么不管第二个字符有多少内容都返回为空了，
这个特性让我们在实例应用中可能觉得不方便，但实现就是这样我们需要使用其它办法来解决。
返回结果为连接参数产生的字符串。如有任何一个参数为NULL，则返回值为NULL。

使用个IFNULL可以判断一下字段是否为空：
MySQL内置的IFNULL函数可以用在查询时候为NULL值字段给一个默认值：
SELECT CONCAT(IFNULL(code,''),telephone) FROM info
```
