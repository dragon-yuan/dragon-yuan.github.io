---
title: SQL中获取前后一个月
categories:
  - Java
date: 2017-10-23 22:07:24
---
```sql
date_add(NOW(), interval 1 MONTH)
#date_add()增加
#date_sub()减少
```
`month`月份；`minute`分钟；`second`秒；