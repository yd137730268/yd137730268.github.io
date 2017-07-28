---  
layout: post  
title: Spring Cloud  
date: 2017-07-28  
categories: blog  
tags: [Java]  
description: Spring Cloud  
  
---  
  
# Spring Cloud 简介
基于[Spring Cloud Brixton.SR5](http://cloud.spring.io/spring-cloud-static/Brixton.SR5/)，Spring Cloud微服务实战
* 服务组建化；按业务组织团队；智能端点和哑管道；去中心化治理；基础设施自动化；容错设计；演进式设计。基于Spring boot实现的微服务架构开发工具。
* Spring Cloud 常用组件: 
1. Spring Cloud Config: 配置管理工具；支持使用git存储配置文件，并支持客户端配置信息的刷新加密解密等。
2. Spring Cloud Netflix :核心组件
2.1 Eureka: 服务治理组件，包括服务注册中心，服务注册与发现机制；
2.2 Hystrix： 容错管理组件，实现断路器模式；
2.3 Ribbon： 客户端负载均衡的服务调用；
2.4 Feign： 声明式调用组件；
2.5 Zuul： 网关组件；
2.6 Archaius： 外部化配置组件；
3. Spring Cloud bus： 事件消息总线；
4. Spring Cloud Cluster ： 针对Zookeeper，redis，Hazelcast，Consul的选举算法和通用状态模式实现；
5. Spring Cloud Cloudfoundry: 与pivotal cloudfoundry的整合；
6. Spring Cloud consul ： 服务发现与配置管理工具；
7. Spring Cloud stream: 通过Redis，Rabbit或者kafka实现的消费微服务；
8. Spring Cloud AWS: 简化整合Amazon web service的组件；
9. Spring Cloud Security ：安全工具包，提供在Zuul代理中的对OAuth2客户端请求的中继器；
10. Spring Cloud Sleuth: 分布式跟踪实现，整合Zipkin;
11. Spring Cloud Zookeeper：基于Zookeeper的服务发现与配置管理组件；
12. Spring Cloud Starters： Spring Cloud的基本组件，基于Spring boot风格项目的基础依赖；
13. Spring Cloud CLI ：用于在Groovy中快速创建Spring Cloud应用的Spring boot CLI插件。
14. Spring Boot Admin ： 管理spring cloud 实例

中文文档： https://www.springcloud.cc/spring-cloud-dalston.html
英文文档： http://cloud.spring.io/spring-cloud-static/Dalston.SR1/

## Spring Boot Admin
管理所有Spring Cloud Service，能监测实例的内存，配置，和状态
### * Admin Server :
1. gradle dependency:
```
	compile 'de.codecentric:spring-boot-admin-server:1.5.2'
 	compile 'de.codecentric:spring-boot-admin-server-ui:1.5.2'
 	compile 'de.codecentric:spring-boot-admin-server-ui-hystrix:1.5.2'
 	compile 'de.codecentric:spring-boot-admin-server-ui-turbine:1.5.2'
 	compile 'org.jolokia:jolokia-core:1.3.6'
```
2. application.yml:
```
spring:
  profiles.active: local
  application.name: CloudCore-AdminServer
  boot.admin.monitor:
    read-timeout: 10000
    connect-timeout: 10000
    period: 5000
server.port: 9001
logging.config: classpath:logback.xml
---
spring:
  profiles: local
``` 
3. add annotation ```@EnableAdminServer```
### *  Admin Client :
1. gradle dependency :
```
	compile 'de.codecentric:spring-boot-admin-starter-client:1.5.2'
```
2. application.yml:
```
spring.boot.admin.url: http://localhost:9001
management.security.enabled: false
```

## Spring Cloud Zipkin
监测请求在Spring Cloud service 调用的一个层次关系和耗时
### * zipkin server:
1. gradle dependency :
```
 	compile 'io.zipkin.java:zipkin-server'
 	compile 'io.zipkin.java:zipkin-autoconfigure-ui'
```
2. add annotation ```@EnableZipkinServer```
### * zipkin client:
1. gradle dependency :
```
    compile("org.springframework.cloud:spring-cloud-starter-sleuth")
    compile("org.springframework.cloud:spring-cloud-sleuth-zipkin")
```
2. application.yml :
```
spring.sleuth.sampler.percentage: 1.0
```

## Spring Cloud Eureka
提供服务的注册
### * zipkin server:
1. gradle dependency:
```
	compile("org.springframework.cloud:spring-cloud-starter-eureka")
	compile("org.springframework.cloud:spring-cloud-starter-eureka-server")
```
2. application.yml
```
server.port: 8086

spring:
  profiles:
    active: local
  application:
    name: CloudCore-RegisterServer

logging.config: classpath:logback.xml
    
---
spring:
  profiles: local
  boot.admin.url: http://localhost:9001
management.security.enabled: false
eureka:
  instance.hostname: localhost
  client:
    register-with-eureka: false
    fetch-registry: false
    serviceUrl.defaultZone: http://localhost:8086/eureka/
    
---
spring:
  profiles: unix1
  boot.admin.url: http://sd-0924-8856:9001
management.security.enabled: false
eureka:
  instance.hostname: sd-a418-d630
  client.serviceUrl.defaultZone: http://sd-1d9b-2fd9:8086/eureka/

---
spring:
  profiles: unix2
  boot.admin.url: http://sd-0924-8856:9001
management.security.enabled: false
eureka:
  instance.hostname: sd-1d9b-2fd9
  client.serviceUrl.defaultZone: http://sd-a418-d630:8086/eureka/

```
3. add annotation ```@EnableEurekaServer```
### * zipkin client:
1. gradle dependency:
```
	compile 'org.springframework.cloud:spring-cloud-starter-eureka'
```
2. application.yml
```
eureka.client.serviceUrl.defaultZone: http://sd-a418-d630:8086/eureka/,http://sd-1d9b-2fd9:8086/eureka/
```
3. add annotation 
```
@EnableDiscoveryClient
@EnableEurekaClient
```

## Spring Cloud Config
提供配置的集中管理，支持git/svn/local 
### * Config server:
1. gradle dependency:
```
	compile 'org.springframework.cloud:spring-cloud-config-server'
```
2. application.yml : local,native is for local config, unix,native is for git repo
```
server.port: 8087

spring:
  profiles:
    active: local,native
  application:
    name: CloudCore-ConfigServer

logging.config: classpath:logback.xml

---
# only native can use local config files
spring:
  profiles: native

---
spring:
  profiles: local
  cloud.config.server.native.searchLocations: file:///C:/Users/user/git/hnwmonitor/CloudCore-ConfigServer/config
  boot.admin.url: http://localhost:9001
management.security.enabled: false
eureka.client.serviceUrl.defaultZone: http://localhost:8086/eureka/   

---
spring:
  profiles: unix
  cloud.config.server.git:
    uri: https://user@cedt-icg-bitbucket.nam.nsroot.net/bitbucket/scm/hnw/hnwmonitor.git
    username: dy83694
    password: *****
    searchPaths: CloudCore-ConfigServer/config
  boot.admin.url: http://sd-0924-8856:9001
management.security.enabled: false
eureka.client.serviceUrl.defaultZone: http://sd-a418-d630:8086/eureka/,http://sd-1d9b-2fd9:8086/eureka/
```
3. add annotation ```@EnableConfigServer```
### * Config client:
1. gradle dependency:
```
	compile("org.springframework.cloud:spring-cloud-starter-config")
```
2. bootstrap.yml: fetch configuration by config server, or get info config server by eureka server 
```
server.port: 8085
spring:
  application.name: CloudService-WebService
  cloud.config:
    label: master
    profile: local
#    uri: http://localhost:8087/
    discovery:
      enabled: true
      serviceId: CloudCore-ConfigServer
  profiles:
    active: local
---
spring:
  profiles: local
eureka.client.serviceUrl.defaultZone: http://localhost:8086/eureka/
---
spring:
  profiles: unix
eureka.client.serviceUrl.defaultZone: http://sd-a418-d630:8086/eureka/,http://sd-1d9b-2fd9:8086/eureka/
```

## Spring Cloud Zuul
提供网关服务，解决多个服务的访问问题
### * Zuul server:
1. gradle dependency:
```
	compile 'org.springframework.cloud:spring-cloud-starter-zuul'
```
2. application.yml
```
zuul:
  forceOriginalQueryStringEncoding: true
  routes:
    RETAIL-DOCSEARCH:
      path: /docService/**
      serviceId: CLOUDSERVICE-DOCSEARCH
      stripPrefix: false
    RETAIL-HNWSUPPORT:
      path: /hnwMonitor/**
      serviceId: CLOUDSERVICE-HNWSUPPORT
      stripPrefix: false
ribbon:
  ConnectTimeout: 10000
  ReadTimeout: 10000
  MaxAutoRetriesNextServer: 2
hystrix.command.default.execution.isolation.thread.timeoutInMilliseconds: 10000
```
3. add annotation ```@EnableZuulProxy```

## Spring Cloud Feign
提供服务的声明式调用，简化服务之间的调用问题
### * Feign client:
1. gradle dependency:
```
	compile("org.springframework.cloud:spring-cloud-starter-feign")
```
2. add annotation```@EnableFeignClients```

  
