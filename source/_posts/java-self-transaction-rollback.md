---
title: Service手动回滚事务
categories:
  - Java
date: 2019-02-21 22:32:11
---
很多业务场景下，可以使用自动回滚事务。
如在一个Service中，可以使用注解形式整体回滚事务。
```java
@Transactional(rollbackFor = Exception.class)
public Boolean xxx() {
	boolean flag = true;
	if (flag) {
		// 正确处理业务
	} else {
		throw new RuntimeException("xxx");
	}
}
```

但也可能遇到如果对外提供API方法（RPC）需要捕获异常的处理业务的话，对于接口调用方仅需要知道错误信息即可，无需了解堆栈信息，此时try-catch后可以手动回滚事务。
```java
TransactionAspectSupport.currentTransactionStatus().setRollbackOnly();
```