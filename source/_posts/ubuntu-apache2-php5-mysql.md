---
title: Ubuntu--apache2+php5+mysql
categories:
  - Operations
date: 2015-09-25 14:41:57
---

sudo apt-get install build-essential autoconf automake1.9 cvs subversion

sudo apt-get install apache2

sudo apt-get install php5

sudo apt-get install mysql-server libapache2-mod-auth-mysql php5-mysql

Mysql的启动/停止/重启  
sudo /etc/init.d/mysql start  
sudo /etc/init.d/mysql stop  
sudo /etc/init.d/mysql restart

/*

Mysql 安装完后设置root密码  
mysql -uroot    (一开始root用户的密码为空所以可以进去， 如果在安装的时候您在界面中设置了password  
可跳过此步)  
进入mysql控制台：  
set password for 'root'@'localhost'=PASSWORD('yourpassword');  
如果成功， mysql提示 ： Query OK 0rows affected（0.00sec）

*/

安装完成配置  
//    sudo gedit /etc/apach2/apach2.conf配置apache服务器  
//    sudo gedit  /etc/php5/apach2/php.ini 配置php在文本框中找到"; extension=mysql.so"， 去掉；表示apache启动时加载与mysql连接的模块， 然后保存，

重启apache服务器。sudo /etc/init.d/apache2 restart
