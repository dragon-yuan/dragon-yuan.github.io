---
title: 在Java中对static的理解
categories:
  - Java
date: 2016-06-27 03:46:53
---

<span style="color: rgb(255, 0, 0);">static是不允许用来修饰局部变量</span>。不要问为什么，这是Java语法的规定。

在《Java编程思想》P86页有这样一段话：

<span style="color: rgb(0, 0, 255);">“static方法就是没有this的方法。在static方法内部不能调用非静态方法，反过来是可以的。而且可以在没有创建任何对象的前提下，仅仅通过类本身来调用static方法。这实际上正是static方法的主要用途。”</span>

<span style="color: rgb(0, 0, 255);"><span style="color: rgb(0, 0, 0);">简而言之，一句话来描述就是：</span></span>方便在没有创建对象的情况下来进行调用（方法/变量）。

<span style="color: rgb(0, 0, 255);"><span style="color: rgb(0, 0, 0);"><span style="color: rgb(255, 0, 0);"><span style="color: rgb(0, 0, 0);">很显然，被static关键字修饰的方法或者变量不需要依赖于对象来进行访问，只要类被加载了，就可以通过类名去进行访问。</span></span></span></span>

<span style="color: rgb(0, 0, 255);"><span style="color: rgb(0, 0, 0);">static可以用来修饰类的成员方法、类的成员变量，另外可以编写static代码块来优化程序性能。</span></span>

<span style="color: #000000;">感谢</span><span style="font-size: 12.1599998474121px; line-height: 1.3em;">尊重作者劳动成果，原文链接：</span>[http://www.cnblogs.com/dolphin0520/p/3799052.html](http://www.cnblogs.com/dolphin0520/p/3799052.html)
