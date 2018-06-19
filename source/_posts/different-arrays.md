---
title: 找出两个数组中不相同的元素
categories:
  - Java
date: 2017-01-01 13:50:22
---
// flagArray为String[]
<pre>
String existsArray[] = new String[]{}; // 与之进行比对的字符集
List<String> list1 = Arrays.asList(flagArray);
List<String> list2 = new ArrayList<String>(); // list2用来装载最终字符集
for (String string : existsArray) {
		if (!list1.contains(string)) {
				list2.add(string);
		}
}
</pre>
