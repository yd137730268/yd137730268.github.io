---
layout: post
title: maven test report
date: 2016-04-01
categories: blog
tags: [maven]
description: maven test report

---

单元测试和集成测试报告，javadoc maven配置：

单元测试和集成测试报告，javadoc maven配置：


```
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>
	<groupId>org.jacoco</groupId>
	<artifactId>test</artifactId>
	<version>1.0.0-SNAPSHOT</version>
	<name>TestPluginProject</name>
	<packaging>war</packaging>



	<dependencies>
		<dependency>
			<groupId>junit</groupId>
			<artifactId>junit</artifactId>
			<version>4.10</version>
			<scope>test</scope>
		</dependency>
	</dependencies>

	<properties>
		<maven.compiler.source>1.7</maven.compiler.source>
		<maven.compiler.target>1.7</maven.compiler.target>
	</properties>

	<build>
		<sourceDirectory>src/main/java</sourceDirectory>
		<testSourceDirectory>src/test/java</testSourceDirectory>
		<plugins>

			<!-- jacoco coverage -->
			<plugin>
				<groupId>org.jacoco</groupId>
				<artifactId>jacoco-maven-plugin</artifactId>
				<version>0.5.3.201107060350</version>
				<executions>
					<execution>
						<id>JaCoCo Agent</id>
						<phase>test-compile</phase>
						<goals>
							<goal>
        prepare-agent
       </goal>
						</goals>
					</execution>
					<execution>
						<id>JaCoCo Report</id>
						<phase>test</phase>
						<goals>
							<goal>
        report
       </goal>
						</goals>
					</execution>
				</executions>
			</plugin>

			<!-- surefire unit and integration test -->
			<plugin>
				<groupId>org.apache.maven.plugins</groupId>
				<artifactId>maven-surefire-plugin</artifactId>
				<version>2.7.2</version>
				<configuration>
					<includes>
						<include>**/*Test.java</include>
					</includes>
				</configuration>
				<executions>
					<execution>
						<id>run-integration-test</id>
						<phase>integration-test</phase>
						<goals>
							<goal>test</goal>
						</goals>
						<configuration>
							<reportsDirectory>target/surefire-reports/integrationTest</reportsDirectory>
							<includes>
								<include>**/*IT.java</include>
							</includes>
						</configuration>
					</execution>
				</executions>
			</plugin>

			<!-- javadoc -->
			<plugin>
				<groupId>org.apache.maven.plugins</groupId>
				<artifactId>maven-javadoc-plugin</artifactId>
				<version>2.8</version>
				<configuration>
					<outputDirectory>target\javadoc</outputDirectory>
					<reportOutputDirectory>target\javadoc</reportOutputDirectory>
				</configuration>
				<executions>
					<execution>
						<id>attach-javadocs</id>
						<phase>site</phase>
						<goals>
							<goal>aggregate</goal>
						</goals>
					</execution>
				</executions>
			</plugin>

			<!-- site -->
			<plugin>
				<groupId>org.apache.maven.plugins</groupId>
				<artifactId>maven-site-plugin</artifactId>
				<version>3.0-beta-3</version>
				<!-- <configuration>
					 <reportPlugins> 
					  <plugin>
						<groupId>org.apache.maven.plugins</groupId>
						<artifactId>maven-surefire-report-plugin</artifactId>
						<version>2.3</version>
						</plugin>
					 </reportPlugins>
				</configuration> -->
			</plugin>
		</plugins>
	</build>


	<reporting>
		<plugins>
			<!-- unit test surefire-report:report -->
			<plugin>
				<groupId>org.apache.maven.plugins</groupId>
				<artifactId>maven-surefire-report-plugin</artifactId>
				<version>2.3</version>
				<configuration>
					<outputName>surefire-unit-report</outputName>
					<reportsDirectory>target/surefire-reports
					</reportsDirectory>
				</configuration>
			</plugin>
			<!-- integration test surefire-report:report -->
			<plugin>
				<groupId>org.apache.maven.plugins</groupId>
				<artifactId>maven-surefire-report-plugin</artifactId>
				<version>2.3</version>
				<configuration>
					<outputName>surefire-integration-report</outputName>
					<reportsDirectory>target/surefire-reports/integrationTest
					</reportsDirectory>
				</configuration>
			</plugin>
		</plugins>
	</reporting>
</project>
```


<img src="/assets/image/test.png" alt="替代文本" title="标题文本" width="200" height = "100" />

