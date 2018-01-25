---
title: Java Builder设计模式
categories:
  - Java
date: 2018-01-25 23:01:55
---
适用场景：复杂对象的组装和创建
建造者模式，是为了将构建复杂对象的过程和它的部件解耦。
它允许用户可以只通过指定复杂对象的类型和内容就可以构建它们。
使用者可以在不知道内部的具体构建细节。
```java
public class Address {
    private final String province;
    private final String city;
    private final String area;
    private final String street;

    public static class Builder {
        private String province;
        private String city;
        private String area;
        private String street;

        public Builder() {

        }

        public Builder province(String province) {
            this.province = province;
            return this;
        }

        public Builder city(String city) {
            this.city = city;
            return this;
        }

        public Builder area(String area) {
            this.area = area;
            return this;
        }

        public Builder street(String street) {
            this.street = street;
            return this;
        }

        public Address build() {
            return new Address(this);
        }
    }

    private Address(Builder builder) {
        province = builder.province;
        city = builder.city;
        area = builder.area;
        street = builder.street;
    }

}

```