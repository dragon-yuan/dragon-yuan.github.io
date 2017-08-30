---
title: Vue中Keep-Alive缓存的使用
categories:
  - Web Design
date: 2017-08-30 22:59:09
---
Vue提供了一个keep-alive组件用来缓存组件。
首先在vue的主页路由上添加keep-alive，并且判断是否在路由开启keepAlive
```js
<keep-alive>
    <router-view v-if="$route.meta.keepAlive"></router-view>
</keep-alive>
<router-view v-if="!$route.meta.keepAlive"></router-view>
```
在需要缓存的页面路由上添加标志位
```js
keepAlive: ture
```
vue中生命周期相关的有：created,mounted,updated,activited,destroyed。
在页面上可以添加activited钩子函数。
针对keep-alive标签，使用keep-alive在单页中前进后退只触发activited。
```js
created() {
	method_1();
},
activited() {
	method_2();
}
```