---
title: jQuery解析JSON
categories:
  - Web Design
date: 2017-01-01 13:50:22
---
<pre>
使用全局的JSON对象
function strToJson(str){
    return JSON.parse(str);
}

eval方式解析
function strToJson(str){
     var json = eval('(' + str + ')');
     return json;
}
</pre>
