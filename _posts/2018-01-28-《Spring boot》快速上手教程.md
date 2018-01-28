---
layout: post
title: 《Spring boot》快速上手教程
date: 2018-01-28
categories: java
tags: [Spring-boot]
---

## 一 框架简介

Spring Boot 简化了基于 Spring 的开发，你只需要运行 “run” 就能创建一个独立的，产品级别的 Spring 应用。
特点：

1. 化繁为简，简化配置
2. 下一代 java 框架
3. 提供一系列大型项目常用的非功能性特征，比如：内嵌服务器，安全，指标，健康检测，外部化配置
4. 专为微服务设计，详情了解 Spring Cloud


## 二 环境准备

1. 安装 Maven
2. 安装 Java

这两个软件的安装网上教程众多，此处不赘述。

## 三 Hello Spring-Boot

### 2.1 初始化项目

// to do

### 2.2 编写 `Hello World`

// to do

### 2.3 启动项目

#### 1. `IED` 启动

右键选中项目，点击 `Run ***Aplication`，在浏览器打开配置地址，即可看到结果。

#### 2. Maven 启动

（1） 进入项目目录

（2） 运行 `mvn spring-boot:run`

#### 3. 编译打包，通过 java 命令启动

（1） 进入项目目录

（2） 运行 `mvn install`

（3） 进入 `./target` 目录

（4） 找到该目录下的 `.jar` 文件，假设为 `test-0.0.1-SNAPSHOT.jar`

（5） 运行命令 `java -jar test-0.0.1-SNAPSHOT.jar` 即可启动项目

## 四 项目配置管理

### 4.1 配置文件选择



## 五 Controller 的使用


## 六 数据库操作


## 七 事务管理


## 八 表单验证


## 九 用 APO 来处理请求


## 十 异常处理


> {{ page.date | date_to_string }}，原创文章，转载请注明出处
