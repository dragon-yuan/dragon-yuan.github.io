---
title: JAVA中正则表达式的使用Pattern
categories:
  - Java
---
<pre>
String reg = "^([1-9]\\d{0,6}(\\.\\d{0,}){0,1})$|^(10000000(\\.0{0,}){0,1})$";
Pattern pattern = Pattern.compile(reg);
Matcher matcher = pattern.matcher(object);
boolean flag = matcher.matches();
</pre>
