---
title: JAVA随机抽取对象
categories:
  - Java
date: 2016-08-08 11:22:33
---
```JAVA
/**
 * @param resultList "最终抽取结果集"
 * @param totalFlag "最多抽取数量"
 * @param canRandomFlag "可以抽取数量"
 * @param personCountNum "当前需要抽取数量"
 */
for (int k = 0; k < personCountNum; k++) {
    double randomNum = Math.random();
    int d = (int)(randomNum * canRandomFlag);
    Object obj = list.get(d); // 获取抽取对象
    resultList.add(obj); // 添加对象到结果集
    list.remove(d); // 移除原始采样组
}
```
