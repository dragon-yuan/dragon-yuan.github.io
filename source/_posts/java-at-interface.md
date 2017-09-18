---
title: Java注释@interface的用法
categories:
  - Java
date: 2017-07-18 21:30:59
---
注解大都用在开发框架中。
Java用 @interface Annotation{} 定义一个注解 @Annotation，一个注解是一个类。
用@Retention(RetentionPolicy.CLASS)修饰的注解，表示注解的信息被保留在class文件(字节码文件)中当程序编译时，
但不会被虚拟机读取在运行的时候;
用@Retention(RetentionPolicy.SOURCE )修饰的注解,表示注解的信息会被编译器抛弃，不会留在class文件中，注解的
信息只会留在源文件中;
用@Retention(RetentionPolicy.RUNTIME )修饰的注解，表示注解的信息被保留在class文件(字节码文件)中当程序编译
时，会被虚拟机保留在运行时，所以他们可以用反射的方式读取。

定义个一注解@MyTarget，用RetentionPolicy.RUNTIME修饰;
```java
@Retention(RetentionPolicy.RUNTIME)  
public @interface MyTarget{
}
```

注解@Target也是用来修饰注解的元注解，它有一个属性ElementType也是枚举类型，
值为：ANNOTATION_TYPE,CONSTRUCTOR,FIELD,LOCAL_VARIABLE,METHOD,PACKAGE,PARAMETER,TYPE  
如@Target(ElementType.METHOD) 修饰的注解表示该注解只能用来修饰在方法上。  
```java
@Target(ElementType.METHOD)  
@Retention(RetentionPolicy.RUNTIME)  
public @interface MyTarget{
	String value() default "val";
}
```