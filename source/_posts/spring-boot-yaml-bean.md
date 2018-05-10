---
title: Spring Boot加载yaml配置到Bean
categories:
  - Java
date: 2018-05-10 22:11:15
---
Spring Boot可能遇到项目启动无法加载yaml配置的情况，可以使用如下配置注入PropertySourcesPlaceholderConfigurer
```java
@Bean
public static PropertySourcesPlaceholderConfigurer properties() {
    PropertySourcesPlaceholderConfigurer configurer = new PropertySourcesPlaceholderConfigurer();
    YamlPropertiesFactoryBean yaml = new YamlPropertiesFactoryBean();
    yaml.setResources(new ClassPathResource("xxx.yml"));
    configurer.setProperties(yaml.getObject());
    return configurer;
}
```
