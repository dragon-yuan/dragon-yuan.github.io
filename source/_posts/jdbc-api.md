---
title: JDBC常用四大API
categories:
  - Java
id: 153
date: 2015-12-23 10:34:58
tags:
---

1\.  DriverManager  获取数据库的驱动

2\.  Conntion  数据库连接对象

3\.  Statement / PrepareStatement 数据库语句对象

4\. ResultSet  结果封装

<1>  导入数据库Jar包

<2> getConnection(url,user,pwd)

<3> createStatement()

       prepareStatement(String sql)

<4> int executeUpdate()  增删改

       executeQuery()  查询
