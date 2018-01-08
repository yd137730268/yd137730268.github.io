---  
layout: post  
title: SpringBatch  
date: 2018-01-08  
categories: blog  
tags: [Java]  
description: SpringBatch  
  
---  

# Spring Batch 

Doc : <https://docs.spring.io/spring-batch/4.0.x/reference/html/index.html>

## Job  
@EnableBatchProcessing
* JobOperator
* JobLauncher
* JobPository
* JobExplorer
* JobRegistor
* JobExecutionListener
* JobParametersValidator
* Job Feature
1. only allow one data source when @EnableBatchProcessing (AbstractBatchConfiguration.getConfigurer)
* Job Configuration

## Step
* ItemReader
* ItemReaderListener
* ItemProcessor
* ItemProcessListener
* ItemWriter
* ItemWriterListener
* Step Feature
1. Split Flows with with parallelisation: <flow>
2. Commit interval : commit-interval
3. complete once reader return null 
4. filter data once processor return null
* Step Configuration

