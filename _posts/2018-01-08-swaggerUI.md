---  
layout: post  
title: swaggerUI  
date: 2018-01-08  
categories: blog  
tags: [Java]  
description: swaggerUI Restful API doc (spring boot)
  
---  

## dependency 
```
	compile "io.springfox:springfox-swagger2:2.6.0"
	compile 'io.springfox:springfox-swagger-ui:2.6.0'
```
## add class
```java
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

import springfox.documentation.builders.ApiInfoBuilder;
import springfox.documentation.builders.PathSelectors;
import springfox.documentation.builders.RequestHandlerSelectors;
import springfox.documentation.service.ApiInfo;
import springfox.documentation.spi.DocumentationType;
import springfox.documentation.spring.web.plugins.Docket;
import springfox.documentation.swagger2.annotations.EnableSwagger2;

@Configuration
@EnableSwagger2
public class Swagger2 {

	@Bean  
    public Docket createRestApi() {  
        return new Docket(DocumentationType.SWAGGER_2)  
                .apiInfo(apiInfo())  
                .select()  
                .apis(RequestHandlerSelectors.basePackage("com.citi.hnw.controller"))
//                .apis(RequestHandlerSelectors.any())  
                .paths(PathSelectors.any())  
                .build();  
    }  
  
    private ApiInfo apiInfo() {
        return new ApiInfoBuilder()  
                .title("HNW Web Interface API")  
                .description("HNW Web Interface API")  
                .version("1.0")
                .build();  
    }  
}
```
