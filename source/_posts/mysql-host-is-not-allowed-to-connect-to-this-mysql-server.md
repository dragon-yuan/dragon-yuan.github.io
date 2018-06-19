---
title: Mysql远程连接 Host * is not allowed to connect to this MySQL server
categories:
  - Operations
date: 2016-02-09 06:49:02
---

mysql -u root -p

mysql>use mysql;

mysql>update user set host ='%'where user ='root';

mysql>flush privileges;

<span style="color: #444444;">#修改host值（以通配符%的内容增加主机/IP地址，当然也可以直接增加某个特定IP地址</span>

<span style="color: #444444;">如果执行update语句时出现</span><span style="color: #0000ff;">ERROR 1062 (23000): Duplicate entry '%-root' for key 'PRIMARY'</span><span style="color: #444444;"> 错误</span>

<span style="color: #444444;">需要select host from user where user = 'root';</span>

<span style="color: #444444;">查看一下host是否已经有了%这个值，如果有了直接执行下面的flush privileges;</span>

<span style="color: #444444;">quit</span>
