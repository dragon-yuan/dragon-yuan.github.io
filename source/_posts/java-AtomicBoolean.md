---
title: AtomicBoolean介绍与使用
categories:
  - Java
date: 2017-07-12 22:52:26
---
AtomicBoolean是Java.util.concurrent.atomic包下的原子变量，这个包里面提供了一组原子类。
其基本的特性就是在多线程环境下，当有多个线程同时执行这些类的实例包含的方法时，具有排他性，
即当某个线程进入方法，执行其中的指令时，不会被其他线程打断，而别的线程就像自旋锁一样，一
直等到该方法执行完成，才由JVM从等待队列中选择一个另一个线程进入，这只是一种逻辑上的理解。
实际上是借助硬件的相关指令来实现的，不会阻塞线程(或者说只是在硬件级别上阻塞了)。

例如AtomicBoolean，在这个Boolean值的变化的时候不允许在之间插入，保持操作的原子性。
方法和举例：compareAndSet(boolean expect, boolean update)。
这个方法主要两个作用:
1. 比较AtomicBoolean和expect的值，如果一致，执行方法内的语句。其实就是一个if语句。
2. 把AtomicBoolean的值设成update。
较最要的是这两件事是一气呵成的，这连个动作之间不会被打断，任何内部或者外部的语句都不可能
在两个动作之间运行。为多线程的控制提供了解决的方案。

```java
import java.util.concurrent.TimeUnit;
public class BarWorker implements Runnable {
	 private static boolean exists = false;  
	 private String name;  

	 public BarWorker(String name) {   
		  this.name = name;  
   }  

	 @Override  
	 public void run() {   
		 if (!exists) {  
			     try {  
			      TimeUnit.SECONDS.sleep(1);  
			     } catch (InterruptedException e1) {  
			      // do nothing
			     }  
			     exists = true;  
			     System.out.println(name + " enter");  
			     try {  
			      System.out.println(name + " working");  
			      TimeUnit.SECONDS.sleep(2);  
			     } catch (InterruptedException e) {  
			      // do nothing  
			     }  
			     System.out.println(name + " leave");  
			     exists = false;  
	    } else {  
	     System.out.println(name + " give up");  
	    }
   }

	 public static void main(String[] args) {
		 BarWorker bar1 = new BarWorker("bar1");
		 BarWorker bar2 = new BarWorker("bar2");
		 new Thread(bar1).start();
		 new Thread(bar2).start();
	}
}
```

输出如下：
bar1 enter
bar2 enter
bar1 working
bar2 working
bar1 leave
bar2 leave

用AtomicBoolean进行线程同步，代码如下：
```java
import java.util.concurrent.TimeUnit;
import java.util.concurrent.atomic.AtomicBoolean;
public class BarWorker2 implements Runnable {
	 private static AtomicBoolean exists = new AtomicBoolean(false);  
	 private String name;  

	 public BarWorker2(String name) {   
		  this.name = name;  
   }  

	 @Override  
	 public void run() {   
		 if (exists.compareAndSet(false, true)) {     
		     System.out.println(name + " enter");  
		     try {  
			      System.out.println(name + " working");  
			      TimeUnit.SECONDS.sleep(2);  
		     } catch (InterruptedException e) {  
		    	  // do nothing  
		     }  
		     System.out.println(name + " leave");  
		     exists.set(false);    
	    } else {  
	         System.out.println(name + " give up");  
	    }  
   }

	 public static void main(String[] args) {
		 BarWorker2 bar1 = new BarWorker2("bar1");
		 BarWorker2 bar2 = new BarWorker2("bar2");
		 new Thread(bar1).start();
		 new Thread(bar2).start();
	}
}
```
执行结果如下：
bar1 enter
bar1 working
bar2 give up
bar1 leave

可以看出仅仅一个线程进行工作，因为exists.compareAndSet(false, true)提供了原子性操作，
比较和赋值操作组成了一个原子操作, 中间不会提供可乘之机。
