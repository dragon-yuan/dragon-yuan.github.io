---
title: sitemesh布局和修饰框架
categories:
  - Java
tags:
---
#简述
SiteMesh是一个用来在JSP中实现页面布局和装饰的框架组件，能够较容易实现页面中动态内容和
静态装饰外观的分离。

#说明
1.首先通过Maven来管理sitemesh
``` xml
<dependency>
  <groupId>opensymphony</groupId>
  <artifactId>sitemesh</artifactId>
  <version>2.4.2</version>
</dependency>
```

2.在web.xml中配置
``` xml
<filter>
  <filter-name>sitemeshFilter</filter-name>
  <filter-class>com.opensymphony.sitemesh.webapp.SiteMeshFilter</filter-class>
</filter>
<filter-mapping>
  <filter-name>sitemeshFilter</filter-name>
  <url-pattern>/*</url-pattern>
</filter-mapping>
```

3.decorators.xml
装饰器配置文件与web.xml同级放在WEB-INF下。defaultdir为布局文件，pattern表示作用域
``` xml
<?xml version="1.0" encoding="UTF-8"?>
<decorators defaultdir="/WEB-INF/layouts/">
    <!-- 禁用装饰器 -->
    <excludes>
        <pattern>/static/*</pattern>
    </excludes>
    <!-- 加载装饰器 -->
    <decorator name="demo" page="default_demo.jsp">
        <pattern>/demo*</pattern>
    </decorator>
</decorators>
```
