---
title: Druid连接池配置连接属性utf8mb4
categories:
  - Java
date: 2018-05-15 14:52:16
---
由于在配置了MySQL数据库，表的编码类型为utf8mb4以后需要重新启动数据库，可由于线上场景的等一些问题的影响，可用过druid设置编码方式。从而让emoji表情可以保存。😈
```java
// 配置druid支持表情
String connectionInitSqls = "SET NAMES utf8mb4";
StringTokenizer tokenizer = new StringTokenizer(connectionInitSqls, ";");
druidDataSource.setConnectionInitSqls(Collections.list(tokenizer));
```
