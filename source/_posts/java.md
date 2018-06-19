---
title: Java基本数据类型
categories:
  - Java
date: 2016-06-21 02:29:25
---

<span style="font-family: 'Microsoft YaHei';">[Java](http://lib.csdn.net/base/17 "Java EE知识库")语言是静态类型的（statical typed)，也就是说所有变量和表达式的类型再编译时就已经完全确定。由于是statical typed，导致Java语言也是强类型（Strong typed）的。强类型意味着每个变量都具有一种类型，每个表达式具有一种类型，并且每种类型都是严格定义的，类型限制了变量可以hold哪些值，表达式最终产生什么值。同时限制了这些值可以进行的操作类型以及操作的具体方式。所有的赋值操作，无论是显式的还是在方法调用中通过参数传递，都要进行类型兼容性检查。</span>

# <a style="color: #ff9900;" name="t0"></a><span style="color: #ff0000;">**<span style="font-family: 'Microsoft YaHei'; font-size: 14px;">1\. 数据类型：</span>**</span>

<span style="font-family: 'Microsoft YaHei';">在java源代码中，每个变量都必须声明一种类型（type）。有两种类型：primitive type和reference type。引用类型引用对象（reference to object），而基本类型直接包含值（directly contain value）。因此，Java数据类型（type）可以分为两大类：基本类型（primitive types）和引用类型（reference types）。primitive types 包括boolean类型以及数值类型（numeric types）。numeric types又分为整型（integer types）和浮点型（floating-point type）。整型有5种：byte short int long char(char本质上是一种特殊的int)。浮点类型有float和double。关系整理一下如下图：</span>

<span style="font-family: 'Microsoft YaHei';">![](http://img.blog.csdn.net/20140531091306906)</span>

转载：原链接：http://blog.csdn.net/bingduanlbd/article/details/27790287 感谢博主
