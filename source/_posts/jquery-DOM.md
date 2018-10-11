---
title: jQuery对DOM元素的操作
categories:
  - Web Design
date: 2016-12-07 22:14:26
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

通过text选中Select组
$("#object option:contains('"+paramsName+"')").attr("selected", true);

通过ID取消Select选中
$('#object').find('option:selected').removeAttr('selected');
</pre>

<code>
// 获取问号传参数据
function getQuery(name) {
    var reg = new RegExp("(^|&)" + name + "=([^&]*)(&|$)", "i");
    var r = window.location.search.substr(1).match(reg);
    if (r != null) return decodeURI(r[2]); return null;
}
</code>
