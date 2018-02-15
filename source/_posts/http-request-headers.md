---
title: HTTP中Request-Headers详解
categories:
  - Operations
date: 2017-07-11 20:52:38
---
Request Headers：
Accept
作用：浏览器端可以接受的媒体类型,
例如：Accept: text/html 代表浏览器可以接受服务器回发的类型为 text/html
也就是我们常说的html文档,如果服务器无法返回text/html类型的数据,
服务器应该返回一个406错误(non acceptable)通配符 * 代表任意类型
例如 Accept: */*  代表浏览器可以处理所有类型,(一般浏览器发给服务器都是发这个)

Accept-Encoding：
作用：浏览器申明自己接收的编码方法，通常指定压缩方法，是否支持压缩，支持什么压缩方法
（gzip，deflate）
例如： Accept-Encoding: gzip, deflate

Accept-Language：
作用：浏览器申明自己接收的语言。 
语言跟字符集的区别：中文是语言，中文有多种字符集，比如big5，gb2312，gbk等等
例如： Accept-Language: en-us或zh-CN

User-Agent：
作用：告诉HTTP服务器， 客户端使用的操作系统和浏览器的名称和版本.
我们上网登陆论坛的时候，往往会看到一些欢迎信息，其中列出了你的操作系统的名称和版本，
你所使用的浏览器的名称和版本，服务器应用程序就是从User-Agent这个请求报头域中获取到
这些信息User-Agent请求报头域允许客户端将它的操作系统、浏览器和其它属性告诉服务器。
例如： User-Agent: Mozilla/5.0 (Windows NT 6.3; WOW64)
AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36

Referer：
作用：提供了Request的上下文信息的服务器，告诉服务器是从哪个链接过来的

Origin：
作用：告诉Request服务是从何处过来的

Host：
作用：请求报头域主要用于指定被请求资源的Internet主机和端口号它通常从URL中提取出来的

Cookie：
作用：最重要的header, 将cookie的值发送给HTTP服务器
Cookie通过URL编码形式发送，转码网站：http://tool.chinaz.com/tools/urlencode.aspx

Content-Length：
作用：发送给HTTP服务器数据的长度
例如：Content-Length: 38

Content-Type：
作用：发送给HTTP服务器数据的类型
例如：Content-Type: application/json;charset=UTF-8

Connection：
例如：Connection: keep-alive 
当一个网页打开完成后，客户端和服务器之间用于传输HTTP数据的TCP连接不会关闭，
如果客户端再次访问这个服务器上的网页，会继续使用这一条已经建立的连接
例如：Connection: close 
代表一个Request完成后，客户端和服务器之间用于传输HTTP数据的TCP连接会关闭，
当客户端再次发送Request，需要重新建立TCP连接。

Authorization：
Authorization消息头的用户名和口令的值可以容易地编码和解码，通过Base64
例如：客户端的请求（用户名“"Aladdin”，口令, password “open sesame”）
Authorization: Basic QWxhZGRpbjpvcGVuIHNlc2FtZQ==
print encode_base64('Aladdin:open sesame'), "\n";
print decode_base64('QWxhZGRpbjpvcGVuIHNlc2FtZQ=='), "\n";
