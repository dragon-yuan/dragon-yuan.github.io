---
title: jQuery对DOM元素的操作
categories:
  - Java
date: 2016-12-07 22:14:26
tags:
---
<pre>
获取单选按钮的值
$('input[name="object"]:checked').val();

获取select选中的值
$("#object").find("option:selected").val();

判断是不是空
$.trim($("#object").val()) == "")

通过Value选择单选按钮
$(":radio[name='object'][value='"+object+"']").attr("checked",'checked');

通过Value选择Select组
$("#object option[value='"+object+"']").attr("selected","selected");

通过name选择单选按钮
$(":radio[name='name'][value='"+value+"']").attr("checked",'checked');

通过name遍历获取复选框选中元素
$("input:checkbox[name='supplyCheckBox']:checked").each(function(i) {

});
</pre>
