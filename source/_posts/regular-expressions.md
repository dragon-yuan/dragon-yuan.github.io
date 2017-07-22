---
title: 正则表达式 总结
categories:
  - Java
---
<p>网络总结-全部可用</p>

匹配中文：
[\u4e00-\u9fa5]

匹配双字节字符(包括汉字在内)：
[^\x00-\xff]

匹配空白行：
\n\s*\r

匹配Email地址：
/^[^\.@]+@[^\.@]+\.[a-z]+$/

匹配手机号：
/^1(3|4|5|7|8)\d{9}$/

匹配网址URL：
[a-zA-z]+://[^\s]*

匹配国内电话号码：
\d{3}-\d{8}|\d{4}-\{7,8}

匹配腾讯QQ号：
[1-9][0-9]{4,}

匹配中国邮政编码：
[1-9]\d{5}(?!\d)

匹配18位身份证号：
^(\d{6})(\d{4})(\d{2})(\d{2})(\d{3})([0-9]|X)$

匹配(年-月-日)格式日期：
([0-9]{3}[1-9]|[0-9]{2}[1-9][0-9]{1}|[0-9]{1}[1-9][0-9]{2}|[1-9][0-9]{3})-(((0[13578]|1[02])-(0[1-9]|[12][0-9]|3[01]))|((0[469]|11)-(0[1-9]|[12][0-9]|30))|(02-(0[1-9]|[1][0-9]|2[0-8])))

匹配正整数：
^[1-9]\d*$

匹配负整数：
^-[1-9]\d*$

匹配整数：
^-?[1-9]\d*$

匹配非负整数（正整数 + 0）：
^[1-9]\d*|0$

匹配非正整数（负整数 + 0）：
^-[1-9]\d*|0$

匹配正浮点数：
^[1-9]\d*\.\d*|0\.\d*[1-9]\d*$

匹配负浮点数：
^-[1-9]\d*\.\d*|-0\.\d*[1-9]\d*$