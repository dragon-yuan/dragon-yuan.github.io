---
title: Swagger配置
categories:
  - Java
date: 2018-02-02 23:54:15
---
首先在Maven pom中加入Swagger依赖库
```xml
<!-- 添加swagger支持 -->
<dependency>
	<groupId>io.springfox</groupId>
	<artifactId>springfox-swagger2</artifactId>
	<version>2.5.0</version>
</dependency>
<dependency>
	<groupId>io.springfox</groupId>
	<artifactId>springfox-swagger-ui</artifactId>
	<version>2.5.0</version>
</dependency>
```
SwaggerConfig配置如下即可
```java
@Configuration
@EnableSwagger2
public class SwaggerConfig {
    /**
     * Swagger配置
     * @author: dragon
     * apiInfo - 自定义Swagger基础信息头
     * select - 选择哪些路径和API是需要生成document
     * apis API接口包扫描路径
     *   - 参数 : RequestHandlerSelectors.any() api接口包扫描路径，对所有api进行监控
     *   - 参数 : RequestHandlerSelectors.basePackage(...) 过滤其他包，仅对选中包进行监控
     *   - 参数 : RequestHandlerSelectors.withClassAnnotation(...) 通过类注解形式进行过滤监控
     *   - 参数 : RequestHandlerSelectors.withMethodAnnotation(...) 通过类注解形式进行过滤监控
     * paths 可以根据接口url路径设置哪些请求加入文档，忽略哪些请求
     *   - 参数 : PathSelectors.any() 对所有接口路径进行监控
     *   - 参数 : PathSelectors.regex("/comm.*") 对接口路径进行过滤监控
     */
    @Bean
    public Docket reservationApi() {
        return new Docket(DocumentationType.SWAGGER_2).
                apiInfo(apiInfo())
                .select()
                .apis(RequestHandlerSelectors.basePackage("com.web.restful"))
                .paths(PathSelectors.any())
                .build();
    }

	private ApiInfo apiInfo() {
		return new ApiInfoBuilder().title("Swagger Title")
		        .description("Swaggere Description.").version("1.0").build();
	}

}
```