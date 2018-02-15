---
title: MyBatis在insert插入操作时返回主键ID（id为自增）
categories:
  - Java
date: 2017-07-18 22:52:26
---
MySQL用法：
```xml
<insert id="insert" parameterType="" keyProperty="userId" useGeneratedKeys="true">
```
上面配置中，keyProperty表示返回的id要保存到对象的那个属性中useGeneratedKeys表示主键id为自增长模式

Oracle用法：
```xml
<insert id="insert" parameterType="">
   <selectKey resultType="INTEGER" order="BEFORE" keyProperty="userId">  
       SELECT USER.NEXTVAL as USERID from USER
   </selectKey>
    ...
</insert>
```
上面配置中，由于Oracle没有自增长，只有序列这种模仿自增的形式，所以不能使用useGeneratedKeys属性
