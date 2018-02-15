---
title: HttpSessionListener与WebListener注解的应用
categories:
  - Java
date: 2017-11-29 21:19:26
---
对于Session来说主要就是它的创建和销毁。
对于`HttpSessionListener`这个接口，有两个方法：
```java
@Override
public void sessionCreated(HttpSessionEvent httpSessionEvent) {
	logger.info("Session创建...");
	HttpSession session = httpSessionEvent.getSession();
}

@Override
public void sessionDestroyed(HttpSessionEvent httpSessionEvent) {
    logger.info("Session销毁...");
}
```
当浏览器第一次访问网站的时候，WEB服务器会新建一个HttpSession对象 ，并触发 HttpSession创建事件 ，如果注册了HttpSessionListener事件监听器，则会调用HttpSessionListener事件监听器的sessionCreated方法。
相反，当访问结束超时的时候，WEB服务器会销毁相应的HttpSession对象，并触发 HttpSession销毁事件，同时调用所注册HttpSessionListener事件监听器的sessionDestroyed方法。
通过httpSessionEvent.getSession()可以获取到新增session的id。通过这个方式，也可以记录当前在线人数。


@WebListener注解
此注解来自servlet-api(javax.servlet.annotation.WebListener)
WebListener注解将一个实现了特定监听器接口的类定义为监听器，这样就不需要在配置文件中配置监听器的相关描述信息
简化了之前WEB.XML中的配置
```xml
<listener>  
   <listener-class>MySessionListener</listener-class>
</listener> 
```
