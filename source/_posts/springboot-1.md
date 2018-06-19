---
title: Spring Boot 优雅的入门篇
categories:
  - Java
date: 2017-01-01 00:00:00
---
#前言
<pre>
Spring一直是很火的一个开源框架，之前使用Struts2+Spring框架居多，Spring Boot在社区中
热度一直很高，所以决定花时间来了解和学习，为自己做技术储备。
</pre>

#正文
<pre>
Spring Boot其实就是Spring,它做了那些没有它你也会去做的Spring Bean配置。它使用“习惯优
于配置”（项目中存在大量的配置，此外还内置了一个习惯性的配置，让你无需手动进行配置）的理
念让你的项目快速运行起来。使用Spring Boot很容易创建一个独立运行（运行jar,内嵌Servlet
容器）、准生产级别的基于Spring框架的项目，使用Spring Boot你可以不用或者只需要很少的
Spring配置。
</pre>

#Maven构建项目
``` xml
<!-- SpringBoot -->
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-web</artifactId>
</dependency>
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot</artifactId>
</dependency>
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-autoconfigure</artifactId>
</dependency>
<!-- 添加对jsp视图解析的支持 -->
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-tomcat</artifactId>
</dependency>
<dependency>
  <groupId>org.apache.tomcat.embed</groupId>
  <artifactId>tomcat-embed-jasper</artifactId>
</dependency>
<dependency>
  <groupId>javax.servlet</groupId>
  <artifactId>javax.servlet-api</artifactId>
</dependency>
<dependency>
  <groupId>javax.servlet</groupId>
  <artifactId>jstl</artifactId>
</dependency>
<!-- Druid -->
<dependency>
  <groupId>com.alibaba</groupId>
  <artifactId>druid</artifactId>
  <version>1.0.29</version>
</dependency>
<!-- 下面两个引入为了操作数据库 -->
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>
<dependency>
  <groupId>mysql</groupId>
  <artifactId>mysql-connector-java</artifactId>
</dependency>
<!-- 只需引入spring-boot-devtools 即可实现热部署 -->
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-devtools</artifactId>
</dependency>
<!-- Log4j -->
<dependency>
  <groupId>log4j</groupId>
  <artifactId>log4j</artifactId>
  <version>1.2.17</version>
</dependency>
```

#应用注解类
<pre>
@SpringBootApplication是Sprnig Boot项目的核心注解，主要目的是开启自动配置。
@RestController 一般用作与接口方式的Controller，返回值为JSON，等价于@Controller+@ResponseBody的结合
@Controller 一般用作页面模式的Controller，返回值可为ModelAndView
@EnableAutoConfiguration 允许自动加载配置
@EnableScheduling Spring计划任务
@Autowired 自动注入
@RequestMapping("/view.do") 请求入口
@ResponseBody和@RequestParam同时使用，表示接受前端请求值，并响应返回值
@Repository Dao层注解，用于标注数据访问组件
@Transactional 事务
@Service Service层注解，用于标注业务层组件
</pre>

#写在最后
<pre>
Hello World : 初始化一个Spring Boot，添加一个控制类，启动即可。
</pre>
