---
title: 浅析Java关键字 transient
categories:
  - Java
date: 2018-01-20 11:11:33
---
```xml
transient官方解释：
Variables may be marked transient to indicate that they are not part of the persistent state of an object.
变量可以被标记为瞬态，表示它们不是对象的持久状态的一部分。
```
Java中transient关键字可以让被修饰的变量不被序列化，只需要实现Serilizable接口，将不需要
序列化的属添加transient，在序列化对象时此属性就不会被序列化到指定的目的地中。