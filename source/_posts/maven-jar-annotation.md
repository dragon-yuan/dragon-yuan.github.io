---
title: Maven打包添加源代码
categories:
  - Java
date: 2018-02-05 21:49:03
---
在Maven pom.xml添加插件，打包jar文件时会自动引入注释：
```xml
<build>
    <plugins>
      	<plugin>
	        <!--引入source插件 -->
	        <groupId>org.apache.maven.plugins</groupId>
	        <artifactId>maven-source-plugin</artifactId>
	        <version>3.0.0</version>
	        <!-- 绑定source插件到Maven的生命周期,并在生命周期后执行绑定的source的goal -->
	        <executions>
	          <execution>
	            <!-- 绑定source插件到Maven的生命周期 -->
	            <phase>compile</phase>
	            <!--在生命周期后执行绑定的source插件的goals -->
	            <goals>
	              <goal>jar-no-fork</goal>
	              <goal>test-jar</goal>
	            </goals>
	          </execution>
	        </executions>
      	</plugin>
	</plugins>
</build>
```