---
title: VueJS中的filters使用
categories:
  - web
date: 2017-07-22 20:02:21
---
filters: 
```js
someFilter(way) {
    let unitName = '';
    switch (way) {
        case '01': { unitName = '名称1'; break; }
        case '02': { unitName = '名称2'; break; }
        case '03': { unitName = '名称3'; break; }
    }
    return unitName;
}

// 其他方法调用
var val = this.someFilter(value);
```