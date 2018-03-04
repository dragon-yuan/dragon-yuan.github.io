---
title: 数据库查询字段后，指定格式化类型
categories:
  - Java
date: 2018-03-04 19:04:51
---
推荐使用工具类：
```xml
<dependency>
  <groupId>com.fasterxml.jackson.core</groupId>
  <artifactId>jackson-annotations</artifactId>
</dependency>
```
应用场景中的使用：
1.在对时间的处理，查询数据库获取的时间格式为Date，获取到的数据形式为毫秒级别，此时，可以使用注解：
```Java
@DateTimeFormat(pattern = "yyyy-MM-dd HH:mm:ss")
@JsonFormat(pattern = "yyyy-MM-dd HH:mm:ss", timezone = "GMT+8")
```
处理时间格式，将其转换为通用时间格式。
2.如存储的数据格式为字符串，但有与之对应的枚举格式，场景如下：
```Java
@JsonFormat(shape = JsonFormat.Shape.OBJECT)
public enum BusinessTypeEnum {
    BUSINESS_ONE("1", "1"),
    BUSINESS_TWO("2", "2");

    private String code;
    private String desc;

    BusinessTypeEnum(String code, String desc) {
        this.code = code;
        this.desc = desc;
    }
    public String getCode() {
        return code;
    }
    public void setCode(String code) {
        this.code = code;
    }
    public String getDesc() {
        return desc;
    }
    public void setDesc(String desc) {
        this.desc = desc;
    }
}
```
可以加入上面注解，此注解可以将枚举类以对象的方式进行序列化。
在<pre>shape</pre>中有如下转换形式，可按需使用。
```Java
public static enum Shape {
  ANY,
  NATURAL,
  SCALAR,
  ARRAY,
  OBJECT,
  NUMBER,
  NUMBER_FLOAT,
  NUMBER_INT,
  STRING,
  BOOLEAN;
}
```
