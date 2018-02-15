---
title: CharSequence类型
categories:
  - Java
date: 2017-07-12 21:52:26
---
String是Java中的字符串，它继承于CharSequence。
String继承于CharSequence，也就是说String也是CharSequence类型。
CharSequence是一个接口，它只包括length(),charAt(int),subSequence(int,int)这几个API接口。
除了String实现了CharSequence之外，StringBuffer和StringBuilder也实现了CharSequence接口。
需要说明的是，CharSequence就是字符序列。
String, StringBuilder和StringBuffer本质上都是通过字符数组实现的。

对于一个抽象类或者是接口类，不能使用new来进行赋值，但是可通过下面的方式来进行实例的创建：
```java
CharSequence cs="hello";
```
但是不能这样来创建：
```java
CharSequence cs=new CharSequence("hello");
```

```java
// 比较字符串是否相等
public static boolean equals(CharSequence cs1, CharSequence cs2) {
    return cs1 == cs2?true:(cs1 != null && cs2 != null?(cs1 instanceof String && cs2 instanceof String?cs1.equals(cs2):CharSequenceUtils.regionMatches(cs1, false, 0, cs2, 0, Math.max(cs1.length(), cs2.length()))):false);
}
```
