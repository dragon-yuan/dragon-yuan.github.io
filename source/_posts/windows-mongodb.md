---
title: Windows环境下mongodb配置
categories:
  - Java
date: 2017-10-31 20:30:52
---
<1>首先安装mongodb不多说了。
<2>配置：
1.在自定义的工作空间下新建Data文件夹
2.在Data下新建db和log文件夹
3.在log文件夹下新建MongoDB.log文件
<3>开启Mongodb Service
通过cmd找到mongodb的安装路径并进入bin文件夹下
```xml
#".....\Data\db"为配置中第二项的路径
#".....\Data\log\MongoDB.log"为配置中第三项的路径
mongod -dbpath ".....\Data\db" -logpath ".....\Data\log\MongoDB.log" -install -serviceName "MongoDB"
```
开启服务 net start mongodb
关闭服务 net stop mongodb
<4>删除Mongodb Service
```xml
#".....\Data\db"为配置中第二项的路径
#".....\Data\log\MongoDB.log"为配置中第三项的路径
mongod -dbpath ".....\Data\db" -logpath ".....\Data\log\MongoDB.log" -remove -serviceName "MongoDB"
```