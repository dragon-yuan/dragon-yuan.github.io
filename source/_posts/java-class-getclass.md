---
title: Java关于对象的遍历，类的反射
categories:
  - Java
date: 2017-11-19 17:40:23
---
Class类是整个Java反射机制的源头，Class类本身表示Java对象的类型，可通过一个Object对象的getClass()方法取得一个对象的类型，
此函数返回的就是一个Class类。

Field提供有关类或接口的属性的信息，以及对他的动态访问权限。
Method提供关于类或接口上的方法的信息。

```java
Ojbect obj = new Object();
Class<? extends Object> objClass = obj.getClass();
Field[] fields = objClass.getDeclaredFields();
for (int k = 0; k < fields.length; k++) {
	String fieldName = fields[k].getName();
	Method m = obj.getClass().getMethod("get" + fieldName.substring(0, 1).toUpperCase() + fieldName.substring(1));
	Object value = m.invoke(obj);
	System.out.println(fieldName + " : " + value);
}
```