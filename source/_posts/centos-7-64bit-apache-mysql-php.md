---
title: 'CentOS-7-64bit 配置Apache + MySQL + PHP '
categories:
  - Operations
date: 2015-10-17 08:40:51
---

<span style="word-wrap: break-word; font-size: 16px; color: #000000;">**一、配置防火墙，开启80端口、3306端口**</span>

<span style="word-wrap: break-word; color: #000000; font-size: 16px;">**CentOS 7.0默认使用的是firewall作为防火墙，这里改为iptables防火墙。**</span>

<span style="word-wrap: break-word; color: #000000; font-size: 16px;">**1、关闭firewall：**</span>

<span style="word-wrap: break-word; color: #64451d;"><span style="word-wrap: break-word; font-size: 16px; color: #000000;">**#停止firewall服务**</span>  
</span>

<div id="codeText" class="codeText" style="word-wrap: break-word; border: 1px solid #dddddd; width: 1041.453125px; overflow: auto; margin: 0px 0px 1.1em; padding: 0px; word-break: break-all; letter-spacing: 0.1px; font-style: normal; font-variant: normal; font-weight: normal; font-stretch: normal; font-size: 12px; line-height: normal; font-family: Consolas, monospace; background: #ffffff;">

1.  <span style="word-wrap: break-word; color: #000000; font-size: 16px;">**systemctl stop firewalld.service**</span>

</div>

<span style="word-wrap: break-word; font-family: 宋体, Arial; line-height: 26px; font-size: 24px; color: #e53333;"><span style="word-wrap: break-word; font-size: 16px; color: #000000;"><span style="word-wrap: break-word;">**#禁止firewall开机启动**</span></span></span>

<div id="codeText" class="codeText" style="word-wrap: break-word; border: 1px solid #dddddd; width: 1041.453125px; overflow: auto; margin: 0px 0px 1.1em; padding: 0px; word-break: break-all; letter-spacing: 0.1px; font-stretch: normal; font-size: 12px; line-height: normal; font-family: Consolas, monospace; color: #666666; background-image: initial; background-attachment: initial; background-size: initial; background-origin: initial; background-clip: initial; background-position: initial; background-repeat: initial;">

1.  <span style="word-wrap: break-word; color: #000000; font-size: 16px;">**systemctl disable firewalld.service**</span>

</div>

<span style="word-wrap: break-word; font-family: 宋体, Arial; font-size: 12px; line-height: 26px; color: #64451d;"> </span>

<span style="word-wrap: break-word; color: #000000; font-size: 16px;">**2、安装iptables防火墙**</span>

<span style="word-wrap: break-word; color: #64451d;"><span style="word-wrap: break-word; font-size: 16px; color: #000000;"><span style="word-wrap: break-word;">**#安装**</span></span>  
</span>

<div id="codeText" class="codeText" style="word-wrap: break-word; border: 1px solid #dddddd; width: 1041.453125px; overflow: auto; margin: 0px 0px 1.1em; padding: 0px; word-break: break-all; letter-spacing: 0.1px; font-stretch: normal; font-size: 12px; line-height: normal; font-family: Consolas, monospace; color: #666666; background-image: initial; background-attachment: initial; background-size: initial; background-origin: initial; background-clip: initial; background-position: initial; background-repeat: initial;">

1.  <span style="word-wrap: break-word; color: #000000; font-size: 16px;">**yum install iptables-services**</span>

</div>

<span style="word-wrap: break-word; font-family: 宋体, Arial; line-height: 26px; font-size: 16px; color: #000000;"><span style="word-wrap: break-word;">**#编辑防火墙配置文件**</span></span><span style="color: #666666; font-family: 宋体, Arial; font-size: 12px; line-height: 26px;"> </span>

<div id="codeText" class="codeText" style="word-wrap: break-word; border: 1px solid #dddddd; width: 1041.453125px; overflow: auto; margin: 0px 0px 1.1em; padding: 0px; word-break: break-all; letter-spacing: 0.1px; font-stretch: normal; font-size: 12px; line-height: normal; font-family: Consolas, monospace; color: #666666; background-image: initial; background-attachment: initial; background-size: initial; background-origin: initial; background-clip: initial; background-position: initial; background-repeat: initial;">

1.  <span style="word-wrap: break-word; color: #000000; font-size: 16px;">**vi /etc/sysconfig/iptables**</span>

</div>

<span style="word-wrap: break-word; color: #000000; font-size: 16px;">**# Firewall configuration written by system-config-firewall**</span>

<span style="word-wrap: break-word; color: #000000; font-size: 16px;">**# Manual customization of this file is not recommended.**</span>

<span style="word-wrap: break-word; color: #000000; font-size: 16px;">***filter**</span>

<span style="word-wrap: break-word; color: #000000; font-size: 16px;">**:INPUT ACCEPT [0:0]**</span>

<span style="word-wrap: break-word; color: #000000; font-size: 16px;">**:FORWARD ACCEPT [0:0]**</span>

<span style="word-wrap: break-word; color: #000000; font-size: 16px;">**:OUTPUT ACCEPT [0:0]**</span>

<span style="word-wrap: break-word; color: #000000; font-size: 16px;">**-A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT**</span>

<span style="word-wrap: break-word; color: #000000; font-size: 16px;">**-A INPUT -p icmp -j ACCEPT**</span>

<span style="word-wrap: break-word; color: #000000; font-size: 16px;">**-A INPUT -i lo -j ACCEPT**</span>

<span style="word-wrap: break-word; color: #000000; font-size: 16px;">**-A INPUT -m state --state NEW -m tcp -p tcp --dport 22 -j ACCEPT**</span>

<span style="word-wrap: break-word; color: #000000; font-size: 16px;">**-A INPUT -m state --state NEW -m tcp -p tcp --dport 80 -j ACCEPT**</span>

<span style="word-wrap: break-word; color: #000000; font-size: 16px;">**-A INPUT -m state --state NEW -m tcp -p tcp --dport 3306 -j ACCEPT**</span>

<span style="word-wrap: break-word; color: #000000; font-size: 16px;">**-A INPUT -j REJECT --reject-with icmp-host-prohibited**</span>

<span style="word-wrap: break-word; color: #000000; font-size: 16px;">**-A FORWARD -j REJECT --reject-with icmp-host-prohibited**</span>

<span style="word-wrap: break-word; color: #000000; font-size: 16px;">**COMMIT**</span>

<span style="word-wrap: break-word; color: #64451d;"><span style="word-wrap: break-word; font-size: 16px; color: #000000;">**:wq! #保存退出**</span>  

</span>

```shell
*filter
:INPUT ACCEPT [0:0]
:FORWARD ACCEPT [0:0]
:OUTPUT ACCEPT [0:0]
:RH-Firewall-1-INPUT - [0:0]
-A INPUT -j RH-Firewall-1-INPUT
-A FORWARD -j RH-Firewall-1-INPUT
-A RH-Firewall-1-INPUT -i lo -j ACCEPT
-A RH-Firewall-1-INPUT -p icmp --icmp-type any -j ACCEPT
-A RH-Firewall-1-INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
-A RH-Firewall-1-INPUT -m state --state NEW -p tcp --dport 21 -j ACCEPT
-A RH-Firewall-1-INPUT -m state --state NEW -m tcp -p tcp --dport 22 -j ACCEPT
-A RH-Firewall-1-INPUT -m state --state NEW -m tcp -p tcp --dport 80 -j ACCEPT
-A RH-Firewall-1-INPUT -m state --state NEW -m tcp -p tcp --dport 443 -j ACCEPT
-A RH-Firewall-1-INPUT -m state --state NEW -m tcp -p tcp --dport 3306 -j ACCEPT
-A RH-Firewall-1-INPUT -m state --state NEW -m tcp -p tcp --dport 4433 -j ACCEPT
-A RH-Firewall-1-INPUT -m state --state NEW -m tcp -p tcp --dport 5293 -j ACCEPT
-A RH-Firewall-1-INPUT -m state --state NEW -m tcp -p tcp --dport 7777 -j ACCEPT
-A RH-Firewall-1-INPUT -m state --state NEW -m tcp -p tcp --dport 8666 -j ACCEPT
-A RH-Firewall-1-INPUT -m state --state NEW -m tcp -p tcp --dport 9000 -j ACCEPT
-A RH-Firewall-1-INPUT -j REJECT --reject-with icmp-host-prohibited
-A FORWARD -j REJECT --reject-with icmp-host-prohibited
COMMIT
```

<span style="word-wrap: break-word; color: #64451d;"><span style="word-wrap: break-word; font-size: 16px; color: #000000;">** #最后重启防火墙使配置生效**</span>  
</span>

<div id="codeText" class="codeText" style="word-wrap: break-word; border: 1px solid #dddddd; width: 1041.453125px; overflow: auto; margin: 0px 0px 1.1em; padding: 0px; word-break: break-all; letter-spacing: 0.1px; font-stretch: normal; font-size: 12px; line-height: normal; font-family: Consolas, monospace; color: #666666; background-image: initial; background-attachment: initial; background-size: initial; background-origin: initial; background-clip: initial; background-position: initial; background-repeat: initial;">

1.  <span style="word-wrap: break-word; color: #000000; font-size: 16px;">**systemctl restart iptables.service**</span>

</div>

<span style="word-wrap: break-word; font-family: 宋体, Arial; line-height: 26px; font-size: 16px; color: #000000;"><span style="word-wrap: break-word;">**#设置防火墙开机启动**</span></span>

<div id="codeText" class="codeText" style="word-wrap: break-word; border: 1px solid #dddddd; width: 1041.453125px; overflow: auto; margin: 0px 0px 1.1em; padding: 0px; word-break: break-all; letter-spacing: 0.1px; font-stretch: normal; font-size: 12px; line-height: normal; font-family: Consolas, monospace; color: #666666; background-image: initial; background-attachment: initial; background-size: initial; background-origin: initial; background-clip: initial; background-position: initial; background-repeat: initial;">

1.  <span style="word-wrap: break-word; color: #000000; font-size: 16px;">**systemctl enable iptables.service**</span>
1.  <span style="word-wrap: break-word; color: #000000; font-size: 16px;">**systemctl disable iptables.service**</span>

</div>

<span style="word-wrap: break-word; color: #64451d;"><span style="word-wrap: break-word; font-size: 16px; color: #000000;">**二、关闭SELINUX**</span>  
<span style="word-wrap: break-word; font-size: 16px; color: #000000;">**#修改配置文件**</span>  
</span>

<div id="codeText" class="codeText" style="word-wrap: break-word; border: 1px solid #dddddd; width: 1041.453125px; overflow: auto; margin: 0px 0px 1.1em; padding: 0px; word-break: break-all; letter-spacing: 0.1px; font-stretch: normal; font-size: 12px; line-height: normal; font-family: Consolas, monospace; color: #666666; background-image: initial; background-attachment: initial; background-size: initial; background-origin: initial; background-clip: initial; background-position: initial; background-repeat: initial;">

1.  <span style="word-wrap: break-word; color: #000000; font-size: 16px;">**vi /etc/selinux/config**</span>

</div>

<span style="word-wrap: break-word; color: #000000; font-size: 16px;">**#SELINUX=enforcing #注释掉**</span>

<span style="word-wrap: break-word; color: #000000; font-size: 16px;">**#SELINUXTYPE=targeted #注释掉**</span>

<span style="word-wrap: break-word; color: #000000; font-size: 16px;">**SELINUX=disabled #增加**</span>

<span style="word-wrap: break-word; color: #000000; font-size: 16px;">**:wq! #保存退出**</span>

<span style="word-wrap: break-word; color: #64451d;"><span style="word-wrap: break-word; font-size: 16px; color: #000000;">**#使配置立即生效**</span>  
</span>

<div id="codeText" class="codeText" style="word-wrap: break-word; border: 1px solid #dddddd; width: 1041.453125px; overflow: auto; margin: 0px 0px 1.1em; padding: 0px; word-break: break-all; letter-spacing: 0.1px; font-stretch: normal; font-size: 12px; line-height: normal; font-family: Consolas, monospace; color: #666666; background-image: initial; background-attachment: initial; background-size: initial; background-origin: initial; background-clip: initial; background-position: initial; background-repeat: initial;">

1.  <span style="word-wrap: break-word; color: #000000; font-size: 16px;">**setenforce 0**</span>

</div>

<span style="word-wrap: break-word; font-family: 宋体, Arial; line-height: 26px; font-size: 16px; color: #000000;">**三.安装apache**</span>  

<div id="codeText" class="codeText" style="word-wrap: break-word; border: 1px solid #dddddd; width: 1041.453125px; overflow: auto; margin: 0px 0px 1.1em; padding: 0px; word-break: break-all; letter-spacing: 0.1px; font-stretch: normal; font-size: 12px; line-height: normal; font-family: Consolas, monospace; color: #666666; background-image: initial; background-attachment: initial; background-size: initial; background-origin: initial; background-clip: initial; background-position: initial; background-repeat: initial;">

1.  <span style="word-wrap: break-word; color: #000000; font-size: 16px;">**yum install httpd**</span>

</div>

<span style="word-wrap: break-word; font-family: 宋体, Arial; line-height: 26px; font-size: 16px; color: #000000;">**可能会用到的：**</span>

<span style="word-wrap: break-word; font-size: 16px; color: #000000;">**systemctl start httpd.service #启动apache**</span>

<span style="word-wrap: break-word; font-size: 16px; color: #000000;">**systemctl stop httpd.service #停止apache**</span>

<span style="word-wrap: break-word; font-size: 16px; color: #000000;">**systemctl restart httpd.service #重启apache**</span>

<span style="word-wrap: break-word; font-size: 16px; color: #000000;">**systemctl enable httpd.service #设置apache开机启动**</span>

CentOS 7的yum源中貌似没有正常安装mysql时的mysql-sever文件，需要去官网上下载

<table style="padding: 0px; margin: 0px; font-family: Verdana, Arial, Tahoma; font-size: 14px; line-height: 25px;" border="0" cellspacing="0" cellpadding="0">

<tbody style="padding: 0px; margin: 0px;">

<tr style="padding: 0px; margin: 0px;">

<td style="padding: 0px; margin: 0px;">

<div style="padding: 0px; margin: 0px;">

<div style="padding: 0px; margin: 0px;"># wget http://dev.mysql.com/get/mysql-community-release-el7-5.noarch.rpm</div>

<div style="padding: 0px; margin: 0px;"># rpm -ivh mysql-community-release-el7-5.noarch.rpm</div>

<div style="padding: 0px; margin: 0px;"># yum install mysql-community-server</div>

</div>

</td>

</tr>

</tbody>

</table>

成功安装之后重启mysql服务

<table style="padding: 0px; margin: 0px; font-family: Verdana, Arial, Tahoma; font-size: 14px; line-height: 25px;" border="0" cellspacing="0" cellpadding="0">

<tbody style="padding: 0px; margin: 0px;">

<tr style="padding: 0px; margin: 0px;">

<td style="padding: 0px; margin: 0px;">

<div style="padding: 0px; margin: 0px;">

<div style="padding: 0px; margin: 0px;"># service mysqld restart</div>

</div>

</td>

</tr>

</tbody>

</table>

初次安装mysql是root账户是没有密码的

设置密码的方法

<table style="padding: 0px; margin: 0px; font-family: Verdana, Arial, Tahoma; font-size: 14px; line-height: 25px;" border="0" cellspacing="0" cellpadding="0">

<tbody style="padding: 0px; margin: 0px;">

<tr style="padding: 0px; margin: 0px;">

<td style="padding: 0px; margin: 0px;">

<div style="padding: 0px; margin: 0px;">

<div style="padding: 0px; margin: 0px;"># mysql -uroot</div>

<div style="padding: 0px; margin: 0px;">mysql> set password for ‘root’@‘localhost’ = password('mypasswd');</div>

<div style="padding: 0px; margin: 0px;">mysql> exit</div>

</div>

</td>

</tr>

</tbody>

</table>

<span style="word-wrap: break-word; font-family: 宋体, Arial; line-height: 26px; font-size: 16px; color: #000000;">**五.安装php**</span>  

<div id="codeText" class="codeText" style="word-wrap: break-word; border: 1px solid #dddddd; width: 1041.453125px; overflow: auto; margin: 0px 0px 1.1em; padding: 0px; word-break: break-all; letter-spacing: 0.1px; font-stretch: normal; font-size: 12px; line-height: normal; font-family: Consolas, monospace; color: #666666; background-image: initial; background-attachment: initial; background-size: initial; background-origin: initial; background-clip: initial; background-position: initial; background-repeat: initial;">

1.  <span style="word-wrap: break-word; color: #000000; font-size: 16px;">**yum install php**</span>

</div>

<span style="word-wrap: break-word; font-family: 宋体, Arial; line-height: 26px; font-size: 16px; color: #000000;">**安装PHP组件，使PHP支持mysql**</span>

<div id="codeText" class="codeText" style="word-wrap: break-word; border: 1px solid #dddddd; width: 1041.453125px; overflow: auto; margin: 0px 0px 1.1em; padding: 0px; word-break: break-all; letter-spacing: 0.1px; font-stretch: normal; font-size: 12px; line-height: normal; font-family: Consolas, monospace; color: #666666; background-image: initial; background-attachment: initial; background-size: initial; background-origin: initial; background-clip: initial; background-position: initial; background-repeat: initial;">

1.  <span style="word-wrap: break-word; color: #000000; font-size: 16px;">**yum install php-mysql php-gd libjpeg* php-ldap php-odbc php-pear php-xml php-xmlrpc php-mbstring php-bcmath php-mhash**</span>

</div>

<span style="word-wrap: break-word; font-family: 宋体, Arial; line-height: 26px; font-size: 16px; color: #000000;">**重启对应服务**</span>

<div id="codeText" class="codeText" style="word-wrap: break-word; border: 1px solid #dddddd; width: 1041.453125px; overflow: auto; margin: 0px 0px 1.1em; padding: 0px; word-break: break-all; letter-spacing: 0.1px; font-stretch: normal; font-size: 12px; line-height: normal; font-family: Consolas, monospace; color: #666666; background-image: initial; background-attachment: initial; background-size: initial; background-origin: initial; background-clip: initial; background-position: initial; background-repeat: initial;">

1.  <span style="word-wrap: break-word; color: #000000; font-size: 16px;">**systemctl restart mysqld.service**</span>
2.  <span style="word-wrap: break-word; color: #000000; font-size: 16px;">**systemctl restart httpd.service**</span>

</div>
