---  
layout: post  
title: springboot  
date: 2017-10-25  
categories: blog  
tags: [Java]  
description: springboot  
  
---  

=========== Spring boot===========

1. document : 
	http://projects.spring.io/spring-boot/#quick-start
	http://www.cnblogs.com/larryzeal/p/5799195.html#c4-2
2. create maven project like this :
	/20170523_springboot
		/20170523_springboot/src/main/java
		/20170523_springboot/src/main/java/hello/SampleController.java
		/20170523_springboot/src/main/resources
		/20170523_springboot/src
		/20170523_springboot/src/main
		/20170523_springboot/src/test
		/20170523_springboot/src/test/java
		/20170523_springboot/src/test/resources
		/20170523_springboot/target
		/20170523_springboot/pom.xml
3. 	pom.xml : 
	<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>
	<groupId>20170523_springboot</groupId>
	<artifactId>20170523_springboot</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	<build>
		<plugins>
			<plugin>
				<groupId>org.springframework.boot</groupId>
				<artifactId>spring-boot-maven-plugin</artifactId>
			</plugin>
		</plugins>
	</build>
	<parent>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-parent</artifactId>
		<version>1.5.3.RELEASE</version>
	</parent>
	<dependencies>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-web</artifactId>
		</dependency>
	</dependencies>
	</project>
4. SampleController.java :
	package hello;
	import org.springframework.boot.*;
	import org.springframework.boot.autoconfigure.*;
	import org.springframework.stereotype.*;
	import org.springframework.web.bind.annotation.*;

	@Controller
	@EnableAutoConfiguration
	public class SampleController {

		@RequestMapping("/")
		@ResponseBody
		String home() {
			return "Hello World!";
		}

		public static void main(String[] args) throws Exception {
			SpringApplication.run(SampleController.class, args);
		}
	}
5. build package : 
	mvn install package 
6. startup :
	java -jar target/20170523_springboot-0.0.1-SNAPSHOT.jar
7. open URL : http://localhost:8080/

8. web container : 
	//tomcat 
	//compile('org.springframework.boot:spring-boot-starter-web')
	//compile 'org.springframework.boot:spring-boot-starter-tomcat'
	//compile 'org.apache.tomcat.embed:tomcat-embed-jasper'
	
	//Jetty
	//compile ('org.springframework.boot:spring-boot-starter-web') {
    	//   exclude group: 'org.springframework.boot', module: 'spring-boot-starter-tomcat'
    	//}
    	compile 'org.springframework.boot:spring-boot-starter-jetty'
	// !! Only for localhost startup or embed web container, please remove it when you use non-embad jetty server
	compile 'org.eclipse.jetty:apache-jsp'
	
	//Undertow : does not support JSPs.
	//compile ('org.springframework.boot:spring-boot-starter-web') {
    	//   exclude group: 'org.springframework.boot', module: 'spring-boot-starter-tomcat'
    	//}
    	//compile 'org.springframework.boot:spring-boot-starter-undertow:1.5.6.RELEASE'
