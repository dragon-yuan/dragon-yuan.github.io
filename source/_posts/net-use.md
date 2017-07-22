---
title: net use错误原因解决
categories:
  - Operations
id: 128
date: 2015-09-22 09:31:03
tags:
---

(1)"发生系统错误 1326。 登录失败： 未知的用户名或错误密码。" 

在远程机的"控制面板-文件夹选项-查看-简单的文件共享",去掉选取,然后再尝试连接。简单文件共享会把网络连接权限都归为 guest连接，是无法访问C$等管理共享的. 

(2)"发生系统错误 1327。 登陆失败：用户帐户限制。  
可能的原因包括不允许空密码，登陆时间限制，或强制的策略限。"在远程机的"控制面板－管理工具－本地安全策略－安全选项－用户权限"指派里，禁用"空密码用户只能进行控制台登陆". 

(3)"//IP/c$"时提示找不到网络途径。  
在"网络和拨号连接"中"本地连接"中选取"Internet协议(TCP/IP)"属性，进入"高级TCP/IP设置"选"WINS设置"里面有一项"启用TCP/IP的NETBIOS

/////////////////////////////////////////////////////////////////////////////

问：net use 找不到网络路径 net use z:>\\192.168.0.2\C$ "18553262" /user:adminis

Net use 会记录新的网络连接。

1，只有nt/2000/xp及以上系统才可以建立ipc$。如果你用的是98/me是没有该功能的。 

2，确认你的命令没有打错。正确的命令是： net use \\目标IP\ipc$ "密码" /user:"用户名" 

注意别多了或少了空格。当用户名和密码中不包含空格时两边的双引号可以省略。空密码用""表示。 

3，根据返回的错误号分析原因：   
错误号5，拒绝访问 ： 很可能你使用的用户不是管理员权限的，先提升权限；   
错误号51，Windows 无法找到网络路径 : 网络有问题；   
错误号53，找不到网络路径 ： ip地址错误；目标未开机；目标lanmanserver服务未启动；目标有防火墙（端口过滤）；   
错误号67，找不到网络名 ： 你的lanmanworkstation服务未启动；目标删除了ipc$；   
错误号1219，提供的凭据与已存在的凭据集冲突 ： 你已经和对方建立了一个ipc$，请删除再连。   
错误号1326，未知的用户名或错误密码 ： 原因很明显了；   
错误号1792，试图登录，但是网络登录服务没有启动 ： 目标NetLogon服务未启动。（连接域控会出现此情况）   
错误号2242，此用户的密码已经过期 ： 目标有帐号策略，强制定期要求更改密码。