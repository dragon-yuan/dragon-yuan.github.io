---
title: VueJS中watch的使用
categories:
  - web
date: 2017-07-28 22:42:30
---
Watch可谓是 Vue中比较重要的部分，检测数据变动后视图更新的重要环节。
```js
// data中定义一个aShow = false 作为显示变量

watch: {
  'aForm.obj': function (val, oldVal) {
    if (val !== '') {
      this.aShow = true;
    } else {
      this.aShow = false;
    }
	}
}
```
