---
title: Mybatis中Mapper.xml映射文件
categories:
  - Java
date: 2017-07-16 15:32:21
---
if : Mybatis核心 对sql语句进行灵活操作，通过表达式进行判断，对sql进行灵活拼接、组装。
对查询条件进行判断，如果输入参数不为空才进行查询条件拼接。
```xml
<select id="findUserList">
  select * from user
  where 1=1
  <if test="id!=null and id!=''">
    and id=#{id}
  </if>
  <if test="username!=null and username!=''">
    and username like '%${username}%'
  </if>
</select>
```

where : 也可以把where写成下面的形式 :
```xml
<select id="findUserList">
  select * from user
  <where>
  <if test="id!=null and id!=''">
  and id=#{id}
  </if>
  <if test="username!=null and username!=''">
  and username like '%${username}%'
  </if>
  </where>
</select>
```

foreach : 向sql传递数组或List，Mybatis使用foreach解析，如下：如果我们需要传入多个ID
来查询多个用户的信息，这也就可以使用foreach。我们先考虑下如果只写sql语句是如下：
```xml
<select id="selectUserByList" parameterType="java.util.List" resultType="user">
  select * from user
  <where>
    <if test="list!=null">
      <foreach collection="list" item="item" open="and id in("separator=","close=")">
        #{item.id}
      </foreach>
    </if>
  </where>
</select>
```

如果需要使用到IN关键字，需要传入List并用foreach遍历放入IN中
```java
<foreach item="item" index="index" collection="list" open="(" separator="," close=")">
    #{item}
</foreach>
```


choose : 标签是按顺序判断其内部when标签中的test条件出否成立，如果有一个成立，则choose
结束。当choose中所有when的条件都不满则时，则执行otherwise中的sql类似于Java的switch语句，
choose为switch，when为case，otherwise则为default。
```xml
<select id="getUserList_choose">  
    SELECT *  
      FROM User u   
    <where>  
        <choose>  
            <when test="username !=null ">  
                u.username LIKE CONCAT(CONCAT('%', #{username, jdbcType=VARCHAR}),'%')  
            </when >  
            <when test="sex != null and sex != '' ">  
                AND u.sex = #{sex, jdbcType=INTEGER}  
            </when >  
            <when test="birthday != null ">  
                AND u.birthday = #{birthday, jdbcType=DATE}  
            </when >  
            <otherwise>  
            </otherwise>  
        </choose>  
    </where>    
</select>
```
