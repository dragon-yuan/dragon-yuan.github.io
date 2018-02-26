---
title: Array.prototype.slice.call(arguments)
categories:
  - web
date: 2017-07-18 22:20:22
---
首先，slice有两个用法，一个是String.slice,一个是Array.slice，第一个返回的是字符串，
第二个返回的是数组。
Array.prototype.slice.call(arguments)能够将arguments转成数组。
```js
// length:2
var a = {'first','second'};
Array.prototype.slice.call(a); //  ["first", "second"]

var a = {};
Array.prototype.slice.call(a); //  [undefined, undefined]
```
