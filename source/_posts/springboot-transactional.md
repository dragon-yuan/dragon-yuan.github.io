---
title: Spring Boot事务管理
categories:
  - Java
date: 2018-01-01 00:00:00
---
#前言
在开发时，由于数操作在顺序执行的过程中，任何一步操作都有可能发生异常，异常会导致后续操
作无法完成，此时由于业务逻辑并未正确的完成，之前成功操作数据的并不可靠，需要在这种情况
下进行回退。事务的作用就是为了保证用户的每一个操作都是可靠的，事务中的每一步操作都必须
成功执行，只要有发生异常就回退到事务开始未进行操作的状态。事务管理是Spring框架中最为常
用的功能之一，在开发应用时，大部分情况下也都需要使用事务。

#事务回滚规则
事务管理器回滚一个事务的推荐方法是在当前事务的上下文内抛出异常。事务管理器会捕捉任何未
处理的异常，然后依据规则决定是否回滚抛出异常的事务。

#操作
用@Transactional注解来声明一个函数需要被事务管理，一般在service层使用@Transactional
来对各个业务逻辑进行事务管理的配置。

@Transactional 可以作用于接口、接口方法、类以及类方法上。当作用于类上时，该类的所有
public方法将都具有该类型的事务属性，同时，也可以在方法级别使用该标注来覆盖类级别的定义。

虽然@Transactional 注解可以作用于接口、接口方法、类以及类方法上，但是 Spring建议不
要在接口或者接口方法上使用该注解，因为这只有在使用基于接口的代理时它才会生效。

@Transactional 注解应该只被应用到public方法上，这是由Spring AOP的本质决定的。
如果在protected、private或者默认可见性的方法上使用@Transactional注解，这将被忽略，
也不会抛出任何异常。

@EnableTransactionManagement
开启注解事务管理，等同于xml配置文件中的 <tx:annotation-driven />

#对于查询的注解处理
不需要事务管理的(只查询的)方法
@Transactional(propagation=Propagation.NOT_SUPPORTED)
在整个方法运行前就不会开启事务
@Transactional(propagation=Propagation.NOT_SUPPORTED,readOnly=true)
这样就做成一个只读事务，可以提高效率
