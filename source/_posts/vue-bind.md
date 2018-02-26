---
title: VueJS中的各项绑定(不定期更新)
categories:
  - web
date: 2017-07-13 23:19:22
---
<1> img的src属性绑定url变量
```html
<img v-bind:src="imgUrl"/>
```
<2> DOM元素绑定不可用
```js
:disabled="$route.query.type == 'edit'
```
