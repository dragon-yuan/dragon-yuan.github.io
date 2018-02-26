---
title: Maven中的dependencyManagement
categories:
  - Java
date: 2018-01-20 11:11:33
---
```xml
# pom.xml
# 只是对版本进行管理，不会实际引入jar包
<dependencyManagement>
      <dependencies>
            <dependency>
                <groupId>org.springframework</groupId>
                <artifactId>spring-core</artifactId>
                <version>3.2.7</version>
            </dependency>
    </dependencies>
</dependencyManagement>
# 实际下载jar包 
<dependencies>
       <dependency>  
                <groupId>org.springframework</groupId>
                <artifactId>spring-core</artifactId>
       </dependency>
</dependencies>
```