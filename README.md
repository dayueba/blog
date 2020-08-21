# NotOnlyJava
不仅仅是Java基础知识

整理和总结网上一些写的好的文章，并进行一些补充和修改。

## 目录

- [Java](#Java)
  - [基础](#基础)
  - [容器](#容器)
  - [并发](#并发)
  - jvm
  - [其它](#其它)
- [数据库](#数据库)
  - [MySQL](#MySQL)
  - [Redis](#Redis)
  - [MongoDB](#MongoDB)
- [框架](#框架)
  - [Spring](#Spring)
  - [SpringBoot](#SpringBoot)
  - [MyBatis](#MyBatis)
- [数据结构与算法](#数据结构和算法)
  - [数据结构](#数据结构)
  - [算法](#算法)
- [全文搜索引擎](#全文搜索引擎)
  - [Elasticsearch](#Elasticsearch)
- [消息队列](#消息队列)
  - [RabbitMQ](#RabbitMQ)
- [系统设计](#系统设计)
  - [必备知识](#必备知识)
  - [认证授权(JWT、SSO)](#认证授权)
  - [大型网站架构](#大型网站架构)
    - [性能测试](#性能测试)
    - [高并发](#高并发)
    - [高可用](#高可用)
- [脚本语言](#脚本语言)
  - [Python](#Python)
  - [JavaScript](#JavaScript)
- [必会工具](#必会工具)
  - [Git](#Git)
  - [Docker](#Docker)
- [网络](#网络)
- [操作系统](#操作系统)
  - [Linux](#Linux)
- [学习资源](#学习资源)
  - [学习方法](#学习方法)
  - [书籍](#书籍)
  - [优质博客](#优质博客)
  - [实战项目](#实战项目)
  - [优质课程](#优质课程)
- [待办](#待办)
- [说明](说明)

## Java

### 基础

**基础知识**

- **[Java 基础知识](https://snailclimb.gitee.io/javaguide/#/docs/java/Java基础知识)**

- **[Java 基础知识疑难点/易错点](https://snailclimb.gitee.io/javaguide/#/docs/java/Java疑难点)**

- [【选看】J2EE 基础知识](https://snailclimb.gitee.io/javaguide/#/docs/java/J2EE基础知识)

**重要知识点**

- [枚举](https://snailclimb.gitee.io/javaguide/#/docs/java/basic/用好Java中的枚举真的没有那么简单)（很重要的一个数据结构，用好枚举真的没有那么简单！）
- [Java 常见关键字总结：final、static、this、super!](https://snailclimb.gitee.io/javaguide/#/docs/java/basic/final,static,this,super)
- [什么是反射机制?反射机制的应用场景有哪些?](https://snailclimb.gitee.io/javaguide/#/docs/java/basic/reflection)
- 注解
- [代理模式详解：静态代理+JDK/CGLIB 动态代理实战（动态代理和静态代理的区别？JDK动态代理 和 CGLIB 动态代理的区别？）](https://snailclimb.gitee.io/javaguide/#/docs/java/basic/java-proxy)

**其它**

- [JAD反编译](https://snailclimb.gitee.io/javaguide/#/docs/java/JAD反编译tricks)
- [手把手教你定位常见Java性能问题](https://snailclimb.gitee.io/javaguide/#/./docs/java/手把手教你定位常见Java性能问题)

### 容器

- **[Java容器常见面试题/知识点总结](https://snailclimb.gitee.io/javaguide/#/docs/java/collection/Java集合框架常见面试题)**
- 源码分析：[ArrayList 源码](https://snailclimb.gitee.io/javaguide/#/docs/java/collection/ArrayList)，[LinkedList 源码](https://snailclimb.gitee.io/javaguide/#/docs/java/collection/LinkedList)，[HashMap(JDK1.8)源码](https://snailclimb.gitee.io/javaguide/#/docs/java/collection/HashMap)，[ConcurrentHashMap源码](https://snailclimb.gitee.io/javaguide/#/docs/java/collection/ConcurrentHashMap)

### 并发

- 多线程学习指南

**面试题总结**

- **[Java 并发基础常见面试题总结](https://snailclimb.gitee.io/javaguide/#/docs/java/Multithread/JavaConcurrencyBasicsCommonInterviewQuestionsSummary)**
- **[Java 并发进阶常见面试题总结](https://snailclimb.gitee.io/javaguide/#/docs/java/Multithread/JavaConcurrencyAdvancedCommonInterviewQuestions)**

**面试常问知识点**

- [并发容器总结](https://snailclimb.gitee.io/javaguide/#/docs/java/Multithread/并发容器总结)
- 线程池：[Java线程池学习总结](https://snailclimb.gitee.io/javaguide/#/./docs/java/Multithread/java线程池学习总结)，[拿来即用的线程池最佳实践](https://snailclimb.gitee.io/javaguide/#/./docs/java/Multithread/best-practice-of-threadpool)

- [乐观锁与悲观锁](https://snailclimb.gitee.io/javaguide/#/docs/essential-content-for-interview/面试必备之乐观锁与悲观锁)
- [万字图文深度解析 ThreadLocal](https://snailclimb.gitee.io/javaguide/#/docs/java/Multithread/ThreadLocal)
- [JUC 中的 Atomic 原子类总结](https://snailclimb.gitee.io/javaguide/#/docs/java/Multithread/Atomic)
- [AQS 原理以及 AQS 同步组件总结](https://snailclimb.gitee.io/javaguide/#/docs/java/Multithread/AQS)

### 其它

1. I/O: [BIO,NIO,AIO 总结](https://snailclimb.gitee.io/javaguide/#/docs/java/BIO-NIO-AIO)
2. Java8：[Java 8 新特性总结](https://snailclimb.gitee.io/javaguide/#/docs/java/What's New in JDK8/Java8Tutorial)，[Java 8 学习资源推荐](https://snailclimb.gitee.io/javaguide/#/docs/java/What's New in JDK8/Java8教程推荐)，[Java8 forEach 指南](https://snailclimb.gitee.io/javaguide/#/docs/java/What's New in JDK8/Java8foreach指南)
3. Java9-java14：[一文带你看遍JDK9~14的重要新特性！](https://snailclimb.gitee.io/javaguide/#/./docs/java/jdk-new-features/new-features-from-jdk8-to-jdk14)
4. Java编程规范：**[Java 编程规范以及优雅 Java 代码实践总结](https://snailclimb.gitee.io/javaguide/#/docs/java/Java编程规范)**、[告别编码5分钟，命名2小时！史上最全的Java命名规范参考！](https://snailclimb.gitee.io/javaguide/#/docs/java/java-naming-conventions)
5. 设计模式：[设计模式系列文章](https://snailclimb.gitee.io/javaguide/#/docs/system-design/设计模式)

## 数据库

### MySQL

**总结：**

1. **[【推荐】MySQL/数据库 知识点总结](https://snailclimb.gitee.io/javaguide/#/docs/database/MySQL)**
2. **[阿里巴巴开发手册数据库部分的一些最佳实践](https://snailclimb.gitee.io/javaguide/#/docs/database/阿里巴巴开发手册数据库部分的一些最佳实践)**
3. **[一千行MySQL学习笔记](https://snailclimb.gitee.io/javaguide/#/docs/database/一千行MySQL命令)**
4. [MySQL高性能优化规范建议](https://snailclimb.gitee.io/javaguide/#/docs/database/MySQL高性能优化规范建议)
5. [一条SQL语句在MySQL中如何执行的](https://snailclimb.gitee.io/javaguide/#/docs/database/一条sql语句在mysql中如何执行的)
6. **[关于数据库中如何存储时间的一点思考](https://snailclimb.gitee.io/javaguide/#/docs/database/关于数据库存储时间的一点思考)**

**面试必问：**

- 索引：[数据库索引总结](docs/database/MySQL/index.md)
- 锁：
- 存储引擎：
- 事务：[事务隔离级别(图文详解)](https://snailclimb.gitee.io/javaguide/#/docs/database/事务隔离级别(图文详解))

**提高**

- 分库分表
- 读写分离

### Redis

- [关于缓存的一些重要概念(Redis前置菜)](https://snailclimb.gitee.io/javaguide/#/docs/database/Redis/some-concepts-of-caching)
- [Redis 常见问题总结](https://snailclimb.gitee.io/javaguide/#/docs/database/Redis/redis-all)
- Redis系列文章合集：
  1. 数据结构和算法：[5种基本数据结构](https://snailclimb.gitee.io/javaguide/#/docs/database/Redis/redis-collection/Redis(1)——5种基本数据结构)，[跳跃表](https://snailclimb.gitee.io/javaguide/#/docs/database/Redis/redis-collection/Redis(2)——跳跃表)，[神奇的HyperLoglog解决统计问题](https://snailclimb.gitee.io/javaguide/#/docs/database/Redis/redis-collection/Reids(4)——神奇的HyperLoglog解决统计问题)，[亿级数据过滤和布隆过滤器](https://snailclimb.gitee.io/javaguide/#/docs/database/Redis/redis-collection/Redis(5)——亿级数据过滤和布隆过滤器)，[GeoHash查找附近的人](https://snailclimb.gitee.io/javaguide/#/docs/database/Redis/redis-collection/Redis(6)——GeoHash查找附近的人)
  2. [持久化](https://snailclimb.gitee.io/javaguide/#/docs/database/Redis/redis-collection/Redis(7)——持久化)
  3. [发布订阅与Stream](https://snailclimb.gitee.io/javaguide/#/docs/database/Redis/redis-collection/Redis(8)——发布订阅与Stream)
  4. [史上最强【集群】入门实践教程](https://snailclimb.gitee.io/javaguide/#/docs/database/Redis/redis-collection/Redis(9)——集群入门实践教程)
  5. [Redis数据类型、编码、底层数据结构的关系看这篇](https://snailclimb.gitee.io/javaguide/#/docs/database/Redis/redis-collection/Redis(10)——Redis数据类型、编码、数据结构的关系)

### MongoDB

**基础知识：**

- [快速入门](http://www.macrozheng.com/#/reference/mongodb_start)

## 框架

### Spring

- [Spring中都用到了那些设计模式?](https://snailclimb.gitee.io/javaguide/#/docs/system-design/framework/spring/Spring-Design-Patterns)
- [SpringMVC 工作原理详解](https://snailclimb.gitee.io/javaguide/#/docs/system-design/framework/spring/SpringMVC-Principle)
- [Spring中 Bean 的作用域与生命周期](https://snailclimb.gitee.io/javaguide/#/docs/system-design/framework/spring/SpringBean)
- **[Spring事务总结](https://snailclimb.gitee.io/javaguide/#/docs/system-design/framework/spring/spring-transaction)**
- **[Spring 常见问题总结](https://snailclimb.gitee.io/javaguide/#/docs/system-design/framework/spring/SpringInterviewQuestions)**
- [Spring IoC 和 AOP详解](https://mp.weixin.qq.com/s?__biz=Mzg2OTA0Njk0OA==&mid=2247486938&idx=1&sn=c99ef0233f39a5ffc1b98c81e02dfcd4&chksm=cea24211f9d5cb07fa901183ba4d96187820713a72387788408040822ffb2ed575d28e953ce7&token=1666190828&lang=zh_CN#rd)

### SpringBoot

- [常用注解](https://snailclimb.gitee.io/javaguide/#/./docs/system-design/framework/spring/spring-annotations)
- [SpringBoot统一日志记录]()
- [SpringBoot统一错误处理]()

### MyBatis

- [MyBatis常见面试题总结](https://snailclimb.gitee.io/javaguide/#/docs/system-design/framework/mybatis/mybatis-interview)

## 数据结构与算法

### 数据结构

- [红黑树基础]()
- [不了解布隆过滤器？一文给你整的明明白白！](https://snailclimb.gitee.io/javaguide/#/docs/dataStructures-algorithms/data-structure/bloom-filter)
- [数据结构知识学习与面试](https://snailclimb.gitee.io/javaguide/#/docs/dataStructures-algorithms/数据结构)

### 算法

- [硬核的算法学习书籍+资源推荐](https://snailclimb.gitee.io/javaguide/#/docs/dataStructures-algorithms/算法学习资源推荐)
- 常见算法问题总结：
  - [几道常见的字符串算法题总结](https://snailclimb.gitee.io/javaguide/#/docs/dataStructures-algorithms/几道常见的子符串算法题)
  - [几道常见的链表算法题总结](https://snailclimb.gitee.io/javaguide/#/docs/dataStructures-algorithms/几道常见的链表算法题)
  - [剑指offer部分编程题](https://snailclimb.gitee.io/javaguide/#/docs/dataStructures-algorithms/剑指offer部分编程题)
  - [公司真题](https://snailclimb.gitee.io/javaguide/#/docs/dataStructures-algorithms/公司真题)
  - [回溯算法经典案例之N皇后问题](https://snailclimb.gitee.io/javaguide/#/docs/dataStructures-algorithms/Backtracking-NQueens)

## 全文搜索引擎

### Elascticsearch



## 消息队列

消息队列在分布式系统中主要是为了解耦和削峰。相关阅读： **[消息队列总结](https://snailclimb.gitee.io/javaguide/#/docs/system-design/data-communication/message-queue)** 。

### RabbitMQ

- [RabbitMQ 入门](https://snailclimb.gitee.io/javaguide/#/docs/system-design/data-communication/rabbitmq)





## 系统设计

### 必备知识

**[RestFul API 简明教程](https://snailclimb.gitee.io/javaguide/#/docs/system-design/restful-api)**

**[命名](https://snailclimb.gitee.io/javaguide/#/docs/system-design/naming)**

### 认证授权

**[认证授权基础:搞清Authentication,Authorization以及Cookie、Session、Token、OAuth 2、SSO](https://snailclimb.gitee.io/javaguide/#/docs/system-design/authority-certification/basis-of-authority-certification)**

**jwt**

- **[JWT 优缺点分析以及常见问题解决方案](https://snailclimb.gitee.io/javaguide/#/docs/system-design/authority-certification/JWT-advantages-and-disadvantages)**
- **[适合初学者入门 Spring Security With JWT 的 Demo](https://github.com/Snailclimb/spring-security-jwt-guide)**

**SSO(单点登录)**

SSO(Single Sign On)即单点登录说的是用户登陆多个子系统的其中一个就有权访问与其相关的其他系统。举个例子我们在登陆了京东金融之后，我们同时也成功登陆京东的京东超市、京东家电等子系统。相关阅读：**[SSO 单点登录看这篇就够了！](https://snailclimb.gitee.io/javaguide/#/docs/system-design/authority-certification/sso)**

### 大型网站架构

- [8 张图读懂大型网站技术架构](https://snailclimb.gitee.io/javaguide/#/docs/system-design/website-architecture/8 张图读懂大型网站技术架构)

- [关于大型网站系统架构你不得不懂的10个问题](https://snailclimb.gitee.io/javaguide/#/docs/system-design/website-architecture/关于大型网站系统架构你不得不懂的10个问题)

#### 性能测试

#### 高并发

#### 高可用

高可用描述的是一个系统在大部分时间都是可用的，可以为我们提供服务的。高可用代表系统即使在发生硬件故障或者系统升级的时候，服务仍然是可用的 。相关阅读： **《[如何设计一个高可用系统？要考虑哪些地方？](https://snailclimb.gitee.io/javaguide/#/docs/system-design/website-architecture/如何设计一个高可用系统？要考虑哪些地方？)》** 。





## 脚本语言

### Python

### JavaScript



## 必会工具

### Git

- [Git入门](https://snailclimb.gitee.io/javaguide/#/docs/tools/Git)

### Docker

- [Docker 基本概念解读](https://snailclimb.gitee.io/javaguide/#/docs/tools/Docker)
- [一文搞懂 Docker 镜像的常用操作！](https://snailclimb.gitee.io/javaguide/#/docs/tools/Docker-Image)

## 网络

1. [计算机网络常见面试题](https://snailclimb.gitee.io/javaguide/#/docs/network/计算机网络)
2. [计算机网络基础知识总结](https://snailclimb.gitee.io/javaguide/#/docs/network/干货：计算机网络知识总结)

## 操作系统

[最硬核的操作系统常见问题总结！](https://snailclimb.gitee.io/javaguide/#/docs/operating-system/basis)

### Linux

1. [后端程序员必备的 Linux 基础知识](https://snailclimb.gitee.io/javaguide/#/docs/operating-system/linux)
2. [Shell 编程入门](https://snailclimb.gitee.io/javaguide/#/docs/operating-system/Shell)
3. [完全使用GNU_Linux学习](https://snailclimb.gitee.io/javaguide/#/docs/operating-system/完全使用GNU_Linux学习)
4. [Linux 性能分析工具合集](https://snailclimb.gitee.io/javaguide/#/docs/operating-system/Linux性能分析工具合集)

## 学习资源

### 学习方法

### 书籍

### 优质博客

- [JavaGuide](https://snailclimb.gitee.io/javaguide/#/?id=基础) 也是看了这个项目才决定自己整理一个

- [mall-learning](http://www.macrozheng.com/#/) 不仅有实战，也有理论

- [SpringAll](https://github.com/wuyouzhuguli/SpringAll) SpringBoot的教程

- [hello-algorithm](https://github.com/geekxh/hello-algorithm) 算法

- [bestJavaer](https://github.com/crisxuan/bestJavaer) 人气不高，文章计算机基础 理论知识偏多

- [interviewGuide](https://github.com/NotFound9/interviewGuide) 后端技术总结

- [Java工程师技术指南](https://github.com/h2pl/Java-Tutorial) 

- [Java工程师成神之路](https://github.com/hollischuang/toBeTopJavaer) 现在内容还挺少的

- [互联网 Java 工程师进阶知识完全扫盲](https://github.com/doocs/advanced-java) 进阶知识

  

### 实战项目

### 视频课程



## 待办

- jvm相关
- 偏向业务的文章

## 说明

资源来源自网络。主要参考项目：[JavaGuide](https://snailclimb.gitee.io/javaguide/#/)

只会收集目前正在学习内容的相关资源

Markdown格式参考：[Github Markdown格式](https://guides.github.com/features/mastering-markdown/)

搭建类似文档类型网站：[《Guide哥手把手教你搭建一个文档类型的网站!免费且高速！》](https://mp.weixin.qq.com/s?__biz=Mzg2OTA0Njk0OA==&mid=2247486555&idx=2&sn=8486026ee9f9ba645ff0363df6036184&chksm=cea24390f9d5ca86ff4177c0aca5e719de17dc89e918212513ee661dd56f17ca8269f4a6e303&token=298703358&lang=zh_CN#rd) 

### 关于我

一个起步较晚，起点较低，但是一直在努力的程序员。