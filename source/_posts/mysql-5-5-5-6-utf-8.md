---
title: MySQL 5.5/5.6的修改字符集编码为UTF-8
categories:
  - Operations
date: 2016-02-10 03:15:48
---

登录MySQL查看用SHOW VARIABLES LIKE ‘character%’;下字符集

<span style="color: rgb(0, 34, 0); font-family: georgia; font-size: 15px; line-height: 22.5px;">1、在[client]字段里加入default-character-set=utf8，如下：</span>  
`  
[client]  
port = 3306  
socket = /var/lib/mysql/mysql.sock  
default-character-set=utf8  
`  
<span style="color: rgb(0, 34, 0); font-family: georgia; font-size: 15px; line-height: 22.5px;">2、在[mysqld]字段里加入character-set-</span>[server](http://www.ha97.com/tag/server)<span style="color: rgb(0, 34, 0); font-family: georgia; font-size: 15px; line-height: 22.5px;">=utf8，如下：</span>  
`  
[mysqld]  
port = 3306  
socket = /var/lib/mysql/mysql.sock  
character-set-server=utf8  
`  
<span style="color: rgb(0, 34, 0); font-family: georgia; font-size: 15px; line-height: 22.5px;">3、在[mysql]字段里加入default-character-set=utf8，如下：</span>  
`  
[mysql]  
no-auto-rehash  
default-character-set=utf8`

`<span style="color: #002200;"><span style="line-height: 22.5px;">修改完成后，service mysql restart重启mysql服务就生效</span></span>`

`<span><span style="color: #002200;"><span style="line-height: 22.5px;">使用SHOW VARIABLES LIKE ‘character%’;查看，发现数据库编码全已改成utf8。</span></span></span>`
