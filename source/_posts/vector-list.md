---
title: ArrayList和LinkedList何时使用
categories:
  - Java
date: 2016-06-30 06:05:11
---

1、如果你需要高效的查询，而不在乎插入和删除的效率，使用ArrayList(不同步JDK1.2) Vector(同步 JDK1.0,过时不用)

2、如果你需要大量的插入和删除，而不关心查询，则应使用LinkedList

ArrayList：对象数量变化少，简单对象，随机访问元素频繁 (查找)

LinkedList：对象数量变化大，对象复杂，插入和删除频繁 (插入，删除)
