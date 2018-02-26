---
title: 将MyEclipse的默认编码改成UTF-8
categories:
  - Java
id: 152
date: 2015-12-23 03:48:49
tags:
---

<span style="color: rgb(69, 69, 69); font-family: arial, 宋体, sans-serif, tahoma, 'Microsoft YaHei'; font-size: 14px; line-height: 24px;">都修改成UTF8的方法：</span>  
<span style="color: rgb(69, 69, 69); font-family: arial, 宋体, sans-serif, tahoma, 'Microsoft YaHei'; font-size: 14px; line-height: 24px;">1、windows->Preferences...打开"首选项"对话框， 左侧导航树，导航到general->Workspace，右侧 Text file encoding，选择Other，改变为UTF-8，以后新建立工程其属性对话框中的Text file encoding即为UTF-8。</span>

<span style="color: rgb(69, 69, 69); font-family: arial, 宋体, sans-serif, tahoma, 'Microsoft YaHei'; font-size: 14px; line-height: 24px;">2、 windows->Preferences...打开"首选项"对话框，左侧导航树，导航到general->Content Types，右侧Context Types树，点开Text，选择Java Source File，在下面的Default encoding输入框中输入UTF-8，点Update，则设置Java文件编码为UTF-8。其他java应用开发相关的文件 如：properties、XML等已经由MyEclipse缺省指定，分别为ISO8859-1，UTF-8，如开发中确需改变编码格式则可以在此指定。</span>
