---
title: 记录APACHE-HTTPS的配置以及遇到的一些陷阱
categories:
  - Operations
date: 2017-12-03 01:39:27
---
在开启HTTPS之前，需要服务器防火墙（如果有使用iptables或firewall）
<1>httpd.conf
```xml
#监听80和443端口
Listen 80
Listen 443

#加载mod_ssl模块
EnableSendfile on
IncludeOptional conf.d/*.conf
LoadModule ssl_module modules/mod_ssl.so
Include conf.d/ssl.conf
```

<2>ssl.conf
```xml
#注意，在此配置文件中不需要监听443，防止重复监听
#在对443虚拟路径映射的时候，需要填写固定IP，不要使用*代替
<VirtualHost ip:443>
#此处填写域名名称
ServerName domain

SSLEngine on
SSLProtocol all -SSLv2 -SSLv3
SSLCipherSuite HIGH:!RC4:!MD5:!aNULL:!eNULL:!NULL:!DH:!EDH:!EXP:+MEDIUM
SSLHonorCipherOrder on

#SSL加密密钥，可以在APACHE根路径下新建cert并存放密钥文件
SSLCertificateFile /etc/httpd/cert/public.pem
SSLCertificateKeyFile /etc/httpd/cert/214047770560394.key
SSLCertificateChainFile /etc/httpd/cert/chain.pem
```

在配置好文件后，需要重新启动APACHE服务
```sheel
srevice iptables restart
service httpd restart
service httpd status
```

开启301；HTTP重定向到HTTPS
```sheel
#在所需的Directory中，修改AllowOverride为All
<Directory "/var/www/html">
AllowOverride All
</Directory>

#在网站跟路径增加.htaccess，并写入下面脚本
RewriteEngine On
RewriteBase /
RewriteCond %{SERVER_PORT} !^443$
RewriteRule ^(.*)$ https://domain/$1 [R=301,L]
```
