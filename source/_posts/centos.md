---
title: Centos中二级域名绑定二级目录的方法
categories:
  - Operations
date: 2016-05-05 05:25:26
---

用文本编辑器打开Apache安装目录/etc/httpd/conf\httpd.conf，找到“#Load[Module](http://www.aliyun.com/zixun/aggregation/72666.html) rewrite_module modules/mod_rewrite.so”这行，去掉[前面](http://www.aliyun.com/zixun/aggregation/54488.html)的“#”;继续[查找](http://www.aliyun.com/zixun/aggregation/20541.html)“AllowOverride None”，修改为“AllowOverride All”，然后，重启Apache即可。

如此，就打开了mod_rewrite模块，其功能非常的强大，这里我只讲如何绑定二级域名。

[同样](http://www.aliyun.com/zixun/aggregation/53635.html)，我们在httpd.conf文件最后输入以下语句：

RewriteEngine on

RewriteMap lowercase int:tolower

RewriteMap vhost txt:/etc/httpd/vhost.map

RewriteCond ${lowercase:%{SERVER_NAME}} ^(.+)$

RewriteCond ${vhost:%1} ^(/.*)$

RewriteRule ^/(.*)$ %1/$1

然后重启Apache

这样，我们就能够自由设置绑定二级域名了。

温馨提示：这个httpd.conf大家注意备份，我就曾经不小心误删，弄的极其的凄惨呀!!

之后在/etc/httpd(即Apache安装目录)下新建一个vhost.map，用文本编辑器来绑定，极其简单，我的是这样写的：

bbs.xxx.com /var/www/html/bbs

home.xxx.com /var/www/html/home

potplayer.xxx.com /var/www/html/potplayer

我们可以随意把二级域名与目录绑定，保存就行，并且[不用](http://www.aliyun.com/zixun/aggregation/20432.html)重启Apache，非常方便。

#### 本文章全部来源于互联网，版权归属于原作者。本站所有转载文章言论不代表本站观点，如是侵犯了原作者的权利请发邮件联系站长（plu_huajuan@163.com），收到后立即删除。
