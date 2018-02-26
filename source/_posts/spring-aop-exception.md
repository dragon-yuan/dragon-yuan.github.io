---
title: Spring中AOP对异常的处理
categories:
  - Java
date: 2017-07-23 15:08:01
---
```java
import com.exception.BusinessException;
import java.lang.reflect.Method;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.aop.ThrowsAdvice;

public class ExceptionInterceptorLog implements ThrowsAdvice {
    private static final Logger logger = LoggerFactory.getLogger(ExceptionInterceptorLog.class);

    public ExceptionInterceptorLog() {
    }

    public void afterThrowing(Method method, Object[] args, Object target, BusinessException ex) {
        logger.error("==>ExceptionInterceptorLog.BusinessException");
        logger.error("==>errCode:" + ex.getCode() + " errMsg:" + ex.getMessage());
        logger.error("==>" + ex.fillInStackTrace());
    }

    public void afterThrowing(Method method, Object[] args, Object target, Exception ex) {
        logger.error("==>ExceptionInterceptorLog.Exception");
        logger.error("==>Error class: " + target.getClass().getName());
        logger.error("==>Error method: " + method.getName());

        for(int i = 0; i < args.length; ++i) {
            logger.error("==>args[" + i + "]: " + args[i]);
        }

        logger.error("==>Exception class: " + ex.getClass().getName());
        logger.error("==>" + ex.fillInStackTrace());
        logger.error("==> 堆栈信息{}", ex.toString(), ex);
    }
}
```
在spring-config-aop.xml进行配置
```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans-4.1.xsd
      http://www.springframework.org/schema/aop http://www.springframework.org/schema/aop/spring-aop-4.1.xsd">
    <!-- 异常信息 拦截 -->
    <bean id="exceptionInterceptorLog" class="com.xescm.core.exception.ExceptionInterceptorLog"></bean>
    <aop:config>
        <aop:pointcut id="exceptionTrade" expression="
        execution(* com.controller.*.*(..))
        or execution(* com.controller.*.*(..))
        "/>
        <aop:advisor pointcut-ref="exceptionTrade" advice-ref="exceptionInterceptorLog"/>
    </aop:config>
</beans>
```