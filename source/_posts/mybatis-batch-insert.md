---
title: 按指定数量拆分List及Mybatis批量插入
categories:
  - Java
date: 2018-01-03 22:44:15
---
当数据量过多需要插入到数据库时，因为数据库连接需要的时间较长，所以可以选择连接池并批量插入数据，从而提高效率。
1.按指定数量拆分List
```java
final int LIST_SIZE = 50;
List<Object> objList = new ArrayList<>();
// 如果小于50个对象，直接插入
if (objList.size() <= LIST_SIZE) {
    for (Object obj : objList) {
        mapper.insert(obj);
    }
} else {
    Object[] params = objList.toArray(new Object[]{});
    int len = params.length;
    for (int i = 1; i <= len / LIST_SIZE; i++) {
        Object[] tmp = Arrays.copyOfRange(params, (i - 1) * LIST_SIZE, i * LIST_SIZE);
        List<Object> paramList = Arrays.asList(tmp);
        mapper.insertByBatch(paramList);
        if (len / LIST_SIZE == i && len % LIST_SIZE > 0) {
            tmp = Arrays.copyOfRange(params, objList.size() / LIST_SIZE * LIST_SIZE, len);
            paramList = Arrays.asList(tmp);
            mapper.insertByBatch(paramList);
        }
    }
}
```
2.Mybatis批量插入数据
```xml
<insert id="insertByBatch" parameterType="java.util.List">
    INSERT INTO table (id, code, name) VALUES
    <foreach collection="paramList" item="param" index="index" separator=",">
        (#{param.id}, #{param.code}, #{param.name}
    </foreach>
</insert>
```