---
title: Spring Boot中使用@ConditionalOnExpression注解
categories:
  - Java
date: 2018-01-20 23:18:10
---
```java
// properties中可以配置isEnabled的值，true即开启Bean注入，false为不注入
@Configuration
@ConditionalOnExpression("${isEnabled}")
public class SomeConfiguration {
    @Bean
    public ... ...(... ...) {
        // 实现
    }
}
```