---
title: 关于时间的处理，以及MyBatis中对时间的处理
categories:
  - Java
date: 2017-10-25 22:04:19
---
`java`
```java
// String -> Date
SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd");
Date date = sdf.parse(dateString);
```
```java
// Date -> String
String dateString = (new SimpleDateFormat("yyyy-MM-dd")).format(new Date());
```
```java
// 在日期上增加数个整月
Calendar cal = Calendar.getInstance();
cal.setTime(new Date());
cal.add(Calendar.MONTH, 1);
Date date = cal.getTime();
```
`mysql`
```sql
# 时间转换
DATE_FORMAT(NOW(),'%b %d %Y %h:%i %p')  
DATE_FORMAT(NOW(),'%m-%d-%Y')  
DATE_FORMAT(NOW(),'%d %b %y')  
DATE_FORMAT(NOW(),'%d %b %Y %T:%f') 
```
`mybatis`
```xml
<![CDATA[>]]>
<![CDATA[>=]]>
<![CDATA[<]]>
<![CDATA[<=]]>
```