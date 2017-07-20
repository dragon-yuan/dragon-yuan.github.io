---
title: Linux部署Java Web项目
categories:
  - Operations
id: 160
date: 2016-02-10 11:36:03
tags:
---

下载java - jdk，地址：<span style="font-size: 12.1599998474121px; line-height: 1.3em;">http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html</span>

<div><span style="font-size: 16px;">tar -zxvf  jdk-8u65-linux-i586.gz</span></div>

<div><span style="font-size: 16px;">mv jdk1.8.0_65  java</span></div>

<div><span style="font-size: 16px;">cd java</span></div>

<div><span><span></span></span>

# 配置环境变量

<span><span></span></span>

<span style="line-height: 1.5;">vim /etc/profile</span>

<span><span></span></span>

<div style="font-size: 16px;">JAVA_HOME=~/java</div>

<span><span></span></span>

<div style="font-size: 16px;">  
PATH=$JAVA_HOME/bin:$PATH</div>

<span><span></span></span>

<div style="font-size: 16px;">  
CLASSPATH=$JAVA_HOME/jre/lib/ext:$JAVA_HOME/lib/tools.jar</div>

<span><span></span></span>

<div style="font-size: 16px;">  
export PATH JAVA_HOME CLASSPATH</div>

<span><span></span></span><span><span></span></span>

<div>

<div style="font-size: 16px;">source /etc/profile</div>

<div style="font-size: 16px;">验证是否成功java -version</div>

<div style="font-size: 16px;"><span style="font-size: 16px;"><span style="font-size: 16px;"><span style="font-size: 16px;"><span style="font-size: 16px;"><span style="font-size: 12.1599998474121px; line-height: 15.8079996109009px;">下载tomcat linux的包，地址：</span>[http://tomcat.apache.org/download-80.cgi](http://tomcat.apache.org/download-80.cgi)<span style="font-size: 12.1599998474121px; line-height: 15.8079996109009px;">，下载的版本是8.0</span></span></span></span></span></div>

<div>解压后进入tomcat/bin/startup.sh查看是否成功</div>

<div><span><span><span></span></span></span>

<div><span style="font-size: 16px;">在Linux下面的防火墙里面开放8080端口 会用命令如下：</span></div>

<span><span><span></span></span></span>

<div><span style="font-size: 16px;">vim /etc/sysconfig/iptables</span></div>

<span><span><span></span></span></span><span><span><span></span></span></span>

<div><span style="font-size: 16px;">重启</span><span style="font-size: 12.1599998474121px; line-height: 1.3em;">service iptables restart </span></div>

<span><span><span></span></span></span><span><span><span></span></span></span>

<div><span><span><span><span><span><span><span></span></span></span></span></span></span></span>

# Linux中设置tomcat的开机启动

<span><span><span><span><span><span><span></span></span></span></span></span></span></span><span><span><span><span><span><span><span></span></span></span></span></span></span></span>

<div><span style="font-size: 16px;">vim /etc/rc.d/rc.local</span></div>

<span><span><span><span><span><span><span></span></span></span></span></span></span></span>

<div><span style="font-size: 16px;">export JAVA_HOME=~/java</span></div>

<span><span><span><span><span><span><span></span></span></span></span></span></span></span>

<div><span style="font-size: 16px;">export CLASSPATH=.:$JAVA_HOME/jre/lib/rt.jar:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar</span></div>

<span><span><span><span><span><span><span></span></span></span></span></span></span></span>

<div><span style="font-size: 16px;">export PATH=$PATH:$JAVA_HOME/bin</span></div>

<span><span><span><span><span><span><span></span></span></span></span></span></span></span>

<div><span style="font-size: 16px;">export CATALINA_HOME=~/tomcat/</span></div>

<span><span><span><span><span><span><span></span></span></span></span></span></span></span>

<div>~/tomcat/bin/startup.sh</div>

<span><span><span><span><span><span><span></span></span></span></span></span></span></span><span><span><span><span><span><span><span></span></span></span></span></span></span></span>

<div>最后导出war包，然后放入webapp中</div>

<span><span><span><span><span><span></span></span></span></span></span></span></div>

<span><span></span></span></div>

</div>

</div>
