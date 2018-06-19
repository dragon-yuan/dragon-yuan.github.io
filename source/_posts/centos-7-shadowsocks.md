---
title: Centos 7安装配置Shadowsocks
categories:
  - Operations
date: 2015-10-17 07:52:38
---

## [源网页](源网页https:/www.ifshow.com/centos-7-installation-and-configuration-shadowsocks/)

## 1\. 安装shadowsocks

<pre style="border: 1px solid #7fb5ff; font-family: 'Courier 10 Pitch', Courier, monospace; font-size: 13px; margin-top: 0px; margin-bottom: 1.625em; outline: 0px; padding: 0.75em 1.625em; vertical-align: baseline; font-stretch: normal; line-height: 1.5; overflow: auto; color: #373737; background: #d9e9ff;">yum install python-setuptools && easy_install pip
pip install shadowsocks</pre>

## 2\. 新建shadowsocks的配置文件

<pre style="border: 1px solid #7fb5ff; font-family: 'Courier 10 Pitch', Courier, monospace; font-size: 13px; margin-top: 0px; margin-bottom: 1.625em; outline: 0px; padding: 0.75em 1.625em; vertical-align: baseline; font-stretch: normal; line-height: 1.5; overflow: auto; color: #373737; background: #d9e9ff;">mkdir -p /etc/shadowsocks
vi /etc/shadowsocks/config.json</pre>

输入以下内容：

<pre style="border: 1px solid #7fb5ff; font-family: 'Courier 10 Pitch', Courier, monospace; font-size: 13px; margin-top: 0px; margin-bottom: 1.625em; outline: 0px; padding: 0.75em 1.625em; vertical-align: baseline; font-stretch: normal; line-height: 1.5; overflow: auto; color: #373737; background: #d9e9ff;">{
 "server":"0.0.0.0",
 "server_port":8888,
 "local_address": "127.0.0.1",
 "local_port":1080,
 "password":"mypassword",
 "timeout":300,
 "method":"aes-256-cfb",
 "fast_open": false,
 "workers": 1
}</pre>

说明：服务器IP，服务端口（建议自定义），本地监听IP，本地监听端口，密码（建议自定义），超时时间，加密算法，关闭fast-open，工作进程数量为1。

## 3\. 新建shadowsocks的.service文件

<pre style="border: 1px solid #7fb5ff; font-family: 'Courier 10 Pitch', Courier, monospace; font-size: 13px; margin-top: 0px; margin-bottom: 1.625em; outline: 0px; padding: 0.75em 1.625em; vertical-align: baseline; font-stretch: normal; line-height: 1.5; overflow: auto; color: #373737; background: #d9e9ff;">vi /etc/systemd/system/shadowsocks-server.service</pre>

输入以下内容：

<pre style="border: 1px solid #7fb5ff; font-family: 'Courier 10 Pitch', Courier, monospace; font-size: 13px; margin-top: 0px; margin-bottom: 1.625em; outline: 0px; padding: 0.75em 1.625em; vertical-align: baseline; font-stretch: normal; line-height: 1.5; overflow: auto; color: #373737; background: #d9e9ff;">[Unit]
Description=Shadowsocks Server
After=network.target

[Service]
Type=forking
PIDFile=/run/shadowsocks/server.pid
PermissionsStartOnly=true
ExecStartPre=/bin/mkdir -p /run/shadowsocks
ExecStartPre=/bin/chown root:root /run/shadowsocks
ExecStart=/usr/bin/ssserver --pid-file /var/run/shadowsocks/server.pid -c /etc/shadowsocks/config.json -d start
Restart=on-abort
User=root
Group=root
UMask=0027

[Install]
WantedBy=multi-user.target</pre>

## 4\. 运行shadowsocks服务并设置为开机自启：

<pre style="border: 1px solid #7fb5ff; font-family: 'Courier 10 Pitch', Courier, monospace; font-size: 13px; margin-top: 0px; margin-bottom: 1.625em; outline: 0px; padding: 0.75em 1.625em; vertical-align: baseline; font-stretch: normal; line-height: 1.5; overflow: auto; color: #373737; background: #d9e9ff;">systemctl start shadowsocks-server.service
systemctl enable shadowsocks-server.service</pre>

## 5\. 防火墙开放shadowsocks服务端口：

<pre style="border: 1px solid #7fb5ff; font-family: 'Courier 10 Pitch', Courier, monospace; font-size: 13px; margin-top: 0px; margin-bottom: 1.625em; outline: 0px; padding: 0.75em 1.625em; vertical-align: baseline; font-stretch: normal; line-height: 1.5; overflow: auto; color: #373737; background: #d9e9ff;">firewall-cmd --permanent --add-port=8888/tcp
firewall-cmd --reload</pre>

## 6\. 常用操作

升级shadowsocks

<pre style="border: 1px solid #7fb5ff; font-family: 'Courier 10 Pitch', Courier, monospace; font-size: 13px; margin-top: 0px; margin-bottom: 1.625em; outline: 0px; padding: 0.75em 1.625em; vertical-align: baseline; font-stretch: normal; line-height: 1.5; overflow: auto; color: #373737; background: #d9e9ff;">pip install -U shadowsocks</pre>

卸载shadowsocks

<pre style="border: 1px solid #7fb5ff; font-family: 'Courier 10 Pitch', Courier, monospace; font-size: 13px; margin-top: 0px; margin-bottom: 1.625em; outline: 0px; padding: 0.75em 1.625em; vertical-align: baseline; font-stretch: normal; line-height: 1.5; overflow: auto; color: #373737; background: #d9e9ff;">pip uninstall shadowsocks
</pre>

查询已安装的shadowsocks

<pre style="border: 1px solid #7fb5ff; font-family: 'Courier 10 Pitch', Courier, monospace; font-size: 13px; margin-top: 0px; margin-bottom: 1.625em; outline: 0px; padding: 0.75em 1.625em; vertical-align: baseline; font-stretch: normal; line-height: 1.5; overflow: auto; color: #373737; background: #d9e9ff;">pip search "shadowsocks"</pre>

停止shadowsocks服务

<pre style="border: 1px solid #7fb5ff; font-family: 'Courier 10 Pitch', Courier, monospace; font-size: 13px; margin-top: 0px; margin-bottom: 1.625em; outline: 0px; padding: 0.75em 1.625em; vertical-align: baseline; font-stretch: normal; line-height: 1.5; overflow: auto; color: #373737; background: #d9e9ff;">systemctl stop shadowsocks-server.service</pre>
