---
title: 关于Java的序列化和serialVersionUID作用
categories:
  - Java
id: 180
date: 2016-08-10 03:34:42
tags:
---

**Java的序列化**

当两个进程在进行远程通信时，彼此可以发送各种类型的数据。无论是何种类型的数据，都会以二进制序列的形式在网络上传送。

发送方需要把这个Java对象转换为字节序列，才能在网络上传送；接收方则需要把字节序列再恢复为Java对象。 

1.把Java对象转换为字节序列的过程称为对象的序列化。 

2.把字节序列恢复为Java对象的过程称为对象的反序列化。 

* * *

对象的序列化主要有两种用途： 

1.把对象的字节序列永久地保存到硬盘上，通常存放在一个文件中 

2.在网络上传送对象的字节序列

* * *

* * *

**serialVersionUID**

简单来说，Java的序列化机制是通过判断类的serialVersionUID来验证版本一致性的。

在进行反序列化时，JVM会把传来的字节流中的serialVersionUID与本地相应实体类的serialVersionUID进行比较，如果相同就认为是一致的，可以进行反序列化，否则就会出现序列化版本不一致的异常（nvalidCastException）

serialVersionUID有两种显示的生成方式：    

一是默认的1L，比如：private static final long serialVersionUID = 1L;        

二是根据类名、接口名、成员方法及属性等来生成一个64位的哈希字段，比如 ：private static final  long  serialVersionUID = xxxxL;

本文来源于网络总结
