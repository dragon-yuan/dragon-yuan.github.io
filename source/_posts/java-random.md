---
title: JAVA随机生成6位验证码
categories:
  - Java
---
<pre>
public static String createRandomCode() {
		String code = "";
		Random r = new Random();
		for (int i = 0; i < 6; i++) {
			code += r.nextInt(10);
		}
		return code;
}
</pre>
