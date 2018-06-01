---
title: MapStruct实体与模型之间的映射（初体验）
categories:
  - Java
date: 2018-03-16 17:23:27
---
工程中引入mapstruct依赖
```xml
<dependency>
  <groupId>org.mapstruct</groupId>
  <artifactId>mapstruct</artifactId>
  <version>1.2.0.Final</version>
</dependency>
```
首先对于注解@Mapper(uses = Info.class)这个注解用于表示需要对什么类进行映射。
比如：
```Java
@Mapper(uses = Info.class)
public interface OrderMapper {
    OrderMapper INSTANCE = Mappers.getMapper(OrderMapper.class);
    @Mappings({
        @Mapping(target = "orderCode", source = "resourceCode",
        @Mapping(target = "businessType", constant = "10"),
        @Mapping(target = "weight",
            expression = "java(MapStructConvertor.convertTonToKg(info.getWeight()))")
    )})
    Object infoToObject(Info info);
}
```
```xml
其中@Mapper(uses = Info.class)为需要被转换的类

#单例模式获取实例对象
OrderMapper INSTANCE = Mappers.getMapper(OrderMapper.class);
#其源代码：
T mapper = classLoader.loadClass(clazz.getName() + "Impl").newInstance();

@Mappings,@Mapping为映射对应字段。
target为转换字段，source为源字段，constant，定义常量值，expression可以自定义方法转换
```
```Java
public class MapStructConvertor {
    public static String convertTonToKg(BigDecimal ton) {
        if (ton == null) {
            return "0.00";
        }
        DecimalFormat df = new DecimalFormat("#.00");
        return df.format(ton.multiply(new BigDecimal(1000)));
    }
}
```
