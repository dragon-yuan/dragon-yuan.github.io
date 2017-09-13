---
title: Linux中crontab定时任务
categories:
  - Operations
date: 2017-09-13 22:09:17
---
crontab命令的功能是在一定的时间间隔调度一些命令的执行

文件/etc/crontab中每行任务的描述格式如下:
```html
minute - 从0到59的整数 
hour - 从0到23的整数 
day - 从1到31的整数 (必须是指定月份的有效日期)
month - 从1到12的整数 (或如Jan或Feb简写的月份)
dayofweek - 从0到7的整数，0或7用来描述周日 (或用Sun或Mon简写来表示)
command - 需要执行的命令(可用as ls /proc >> /tmp/proc或 执行自定义脚本的命令)

root表示以root用户身份来运行
run-parts表示后面跟着的是一个文件夹，要执行的是该文件夹下的所有脚本
```

crontab服务的启动关闭
```html
sbin/service crond start //启动服务
/sbin/service crond stop //关闭服务
/sbin/service crond restart //重启服务
/sbin/service crond reload //重新载入配置
```