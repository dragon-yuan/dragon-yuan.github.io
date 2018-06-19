---
title: JAVA随机生成6位验证码
categories:
  - Java
date: 2016-08-01 11:22:33
---
初学JAVA时期的代码：
```JAVA
public static String createRandomCode() {
		String code = "";
		Random r = new Random();
		for (int i = 0; i < 6; i++) {
			code += r.nextInt(10);
		}
		return code;
}
```
