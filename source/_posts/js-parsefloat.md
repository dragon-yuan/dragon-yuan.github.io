---
title: 使用JS保留两位小数
categories:
  - Java
date: 2017-03-07 17:22:26
---
<pre>
由于js显示的值为varchar类型，所以显示小数需要转换成float类型，并用toFixed保留位数
<code>parseFloat(value).toFixed(2)</code>
</pre>
