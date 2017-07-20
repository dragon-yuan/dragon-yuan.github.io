---
title: request.getRequestDispatcher和response.sendRedirect区别
categories:
  - Java
id: 179
date: 2016-08-08 03:55:53
tags:
---

request.getRequestDispatcher(String arg0)是"转向"的意思

response.sendRedirect(String arg0)是重定向<span style="font-size: 12.1599998474121px; line-height: 15.8079996109009px;">的意思</span>

1.request.getRequestDispatcher(String arg0)

转向的特点:

地址栏的URl是不变,如:servlet --A转向到servlet---B的时候,地址栏还是A它本身,但是内容其实上已经是B的内容了

2.response.sendRedirect(String arg0)

重定向的特点:

地址栏的URL是会改变的.如:servlet--A转向到servlet--B的时候,地址栏就变成B了

重定向sendRedirect(String arg0)  跟转向的"forward()"方法有点类似之处:就是在放在它们后面的语句都不会被执行

response不能被传递
