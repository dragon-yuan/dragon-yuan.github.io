---
title: ConvertUtils的简单使用
categories:
  - Java
date: 2017-01-01 13:50:22
---
<pre>
import org.apache.commons.beanutils.ConvertUtils;
// 将字符串转换为指定类型
String[] idStringArray = new String[] { "1", "2", "3", "4", "5" };
Long[] idLongArray = (Long[]) ConvertUtils.convert(idString, Long.class);
</pre>
