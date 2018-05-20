---
title: Spring事务的七种传播行为，四种特性
categories:
  - Java
date: 2018-01-16 22:57:15
---
```xml
spring默认传播行为。
如果有事务，那么加入事务，没有的话新建一个。
@Transactional(propagation=Propagation.REQUIRED)

容器不为这个方法开启事务
@Transactional(propagation=Propagation.NOT_SUPPORTED)

创建一个新的事务，原来的挂起，新的执行完毕，继续执行老的事务
两个事务没有依赖关系，可以实现新事务回滚了，但外部事务继续执行
@Transactional(propagation=Propagation.REQUIRES_NEW)

必须在一个已有的事务中执行,否则抛出异常
@Transactional(propagation=Propagation.MANDATORY)

必须在一个没有的事务中执行，否则抛出异常
@Transactional(propagation=Propagation.NEVER)

如果其他bean调用这个方法，在其他bean中声明事务，那就用事务，如果其他bean没有声明事务，那就不用事务。
@Transactional(propagation=Propagation.SUPPORTS)

如果当前存在事务，则在嵌套事务内执行，如果当前不存在事务，则创建一个新的事务，嵌套事务使用数据库中的保存点来实现，即嵌套事务回滚不影响外部事务，但外部事务回滚将导致嵌套事务回滚。
@Transactional(propagation=Propagation.Nested)
```

```xml
四种特性：
1、原子性：事务包含的所有操作要么全部成功，要么全部失败回滚。
2、一致性：事务必须使数据库从一个一致性状态变换到另一个一致性状态，也就是说一个事务执行之前和执行之后都必须处于一致性状态。
3、持久性：事务一旦被提交了，那么对数据库中的数据的改变就是永久性的，即便是在数据库系统遇到故障的情况下也不会丢失提交事务的操作。
4、隔离性：当多个用户并发访问数据库时，比如操作同一张表时，数据库为每一个用户开启的事务，不能被其他事务的操作所干扰，多个并发事务之间要相互隔离。
```
