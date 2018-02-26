---
title: Tomcat针对读取文件问题 Not allowed to load local resource解决办法
categories:
  - Java
id: 156
date: 2016-01-06 09:54:21
tags:
---

    Servlet转发到JSP页面后<img style="height:50px; width:50px" name="student" src="C:/jboss/welcome-content/students/'+ studentBasic.photo+ '" />不允许用文件的绝对路径 而需要这样写src<img style="height:50px; width:50px" name="student" src="/students/"+studentBasic.photo+"
