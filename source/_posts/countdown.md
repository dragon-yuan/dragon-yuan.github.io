---
title: 初识JAVA倒计时
categories:
  - Java
---
<1>.先获取到服务器的时间
var nowTdrCommon =<%=System.currentTimeMillis()%>; //服务器时间
var nowTdrCommon1 =<%=System.currentTimeMillis()%>; //服务器时间

<2>.获取到结束时间（结束时间为obj）
var EndDateTime_cd = obj;
var EndDateTime_s = EndDateTime_cd.replace(/-/g, "/");
nowTdrCommon = nowTdrCommon + 1000;
var date1 = new Date(nowTdrCommon); //开始时间
var date2 = new Date(EndDateTime_s); //结束时间
var date3 = date2.getTime() - date1.getTime(); //时间差的毫秒数

//计算出相差天数
var days = Math.floor(date3 / (24 * 3600 * 1000));

//计算出小时数
var leave1 = date3 % (24 * 3600 * 1000); //计算天数后剩余的毫秒数
var hours = Math.floor(leave1 / (3600 * 1000));

//计算相差分钟数
var leave2 = leave1 % (3600 * 1000); //计算小时数后剩余的毫秒数
var minutes = Math.floor(leave2 / (60 * 1000));

//计算相差秒数
var leave3 = leave2 % (60 * 1000); //计算分钟数后剩余的毫秒数
var seconds = Math.round(leave3 / 1000);

<3>.比较时间，并输出显示剩余时间
if (date3 < 0) {
		return "0";
} else {
		return "<span><strong>" + days + "天</strong></span><span><strong>"
+ hours + "时</strong></span><span><strong>" + minutes
+ "分</strong></span><span><strong>" + seconds
+ "秒</strong></span>";
}
