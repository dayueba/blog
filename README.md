# blog
这是我的个人博客主页

记录自己写的博客以及推荐一些学习资料，希望大家都能成为优秀的程序员。

## 目录
- [学习方法](#学习方法)
- [编程语言](#编程语言)
  - [Python](#Python)
  - [JavaScript](#JavaScript)
  - [Go](#Go)
- [数据库](#数据库)
  - [MySQL](#MySQL)
  - [Redis](#Redis)
  - [Elasticsearch](#Elasticsearch)
  <!-- - [MongoDB](#MongoDB) -->
- [消息队列](#消息队列)
  - [RabbitMQ](#RabbitMQ)
  - [Kafka](#Kafka)
- [计算机基础](#计算机基础)
  - [数据结构](#数据结构)
  - [算法](#算法)
  - [网络](#网络)
  - [操作系统](#操作系统)
  - [计算机组成原理](#计算机组成原理)
  - [概率论](#概率论)
  - [统计学](#统计学)
- [设计模式](#设计模式)
- [云原生](#云原生)
  - [Docker](#Docker)
  - [etcd](#etcd)
  <!-- - [Kubernetes](#Kubernetes) -->
- [系统设计](#系统设计)
  - [认证授权](#认证授权)
- [分布式](#分布式)
  - [RPC](#RPC)
  - [分布式限流](#分布式限流)
- [必会工具](#必会工具)
  - [Git](#Git)
- [实战文章](#实战文章)
- [面试指南](#面试指南)
- [学习资源](#学习资源)
- [待办](#待办)
- [说明](#说明)

## 学习方法

- [总结的一些学习方法以及一些好的习惯](https://xjip3se76o.feishu.cn/mindnotes/bmncniLbhid2PubMtdOEIwon2Jc)

## 编程语言

### Python

<!-- - [我的Python文章合集](https://www.yuque.com/u1169619/kb2a00#%20%E3%80%8APython%E3%80%8B) -->
- todo: [装饰器]()

新特性
- [海象运算符 & 类型注解](https://xjip3se76o.feishu.cn/docs/doccnXgd4NaLIMMZLHF2S8IoHZf)

### JavaScript

- [数据类型](docs/js/数据类型.md)
- [深拷贝与浅拷贝](docs/js/深拷贝与浅拷贝.md)
- [闭包](docs/js/闭包.md)
- [JS 内存管理机制](docs/js/JS内存管理机制.md)
- [promise详解](docs/js/promise.md)

**TypeScript**: TypeScript不是一门新的编程语言，而是JavaScript的超集。提供了强大的类型系统，可以解决一大堆问题。TypeScript 是一门中间语言，最终它还需要转译为纯 JavaScript，再交给各种终端解释、执行。
- [TypeScript](docs/js/typescript.md)
- [类型](docs/js/ts/类型.md)

**Nodejs**

- [Nodejs入门](docs/js/nodejs/node.md)
- [Node事件循环机制](docs/js/事件循环机制.md)
- todo: [Buffer和stream模块]()

### Go

- [注意的点](https://xjip3se76o.feishu.cn/docs/doccnJPTeCDiI01jvDMAoYDWqSe)
- [error](https://xjip3se76o.feishu.cn/docs/doccnxU4HTdnOq33vaBdxqHfDPd)

## 数据库

### MySQL
mysql的提高包括：SQL 语句优化、索引原理、MySQL 锁、事务、MySQL 安全、分库分表、读写分离、MySQL 操作规范等

- [学习资料推荐](https://www.yuque.com/docs/share/533eeaef-1f2c-4518-ba00-e33fc9df286a)
<!-- - [我的MySQL文章合集](https://www.yuque.com/u1169619/bgwsg4#%20%E3%80%8AMySQL%E3%80%8B) -->
- [自己整理的几道容易出错的面试题](docs/database/MySQL/mysql面试题.md)
- [聊聊主键](docs/database/MySQL/聊聊主键.md)
- [MySQL 那些常见的错误设计规范](https://mp.weixin.qq.com/s?__biz=MjM5ODc5ODgyMw==&mid=2653585806&idx=1&sn=5e00837028440d41bea2e35dcee2d215&chksm=bd1b15068a6c9c101e1d3d1e8a74219fa696a475017b91cc4b5f8388b90596c0663f13fa1ae4&mpshare=1&scene=2&srcid=0709WZNZPqskWXlsHZJ3T5uX&sharer_sharetime=1625827270022&sharer_shareid=a9f162b83d3be451174be9ec97298b2b#rd)

**总结：**

- [开发与设计规范](docs/database/MySQL/开发与设计规范.md)
- [事务](https://xjip3se76o.feishu.cn/docs/doccne4DKKKmA0Tpad2SPhjEnPe), [mvcc](docs/database/MySQL/mvcc.md)
- [存储引擎](https://xjip3se76o.feishu.cn/docs/doccnDM66eaPlUOzaPo5SVptJLf)
- [一条SQL语句在MySQL中如何执行的](docs/database/MySQL/一条sql语句在mysql中如何执行的.md)
- [MySQL 中存储时间的最佳实践](https://www.upyun.com/tech/article/652/MySQL%20%E4%B8%AD%E5%AD%98%E5%82%A8%E6%97%B6%E9%97%B4%E7%9A%84%E6%9C%80%E4%BD%B3%E5%AE%9E%E8%B7%B5.html)
- 索引：[数据库索引总结](docs/database/MySQL/index.md), [索引实战](docs/database/MySQL/索引实战.md)
- 锁: [全局锁&表锁&行锁](docs/database/MySQL/lock.md), [死锁](docs/database/MySQL/dead-lock.md)

**sql优化**

- [分析SQL执行效率](https://www.yuque.com/docs/share/52941483-0e31-4665-a371-2b52e2febe66), [执行效率分析](docs/database/MySQL/执行效率分析.md)
- [优化count](docs/database/MySQL/优化count.md)
- [优化分页查询](docs/database/MySQL/优化分页查询.md)
- [优化join](https://www.yuque.com/docs/share/214278dd-1a07-425e-8796-5d7b58a47a7f)
- [优化数据插入](https://www.yuque.com/docs/share/80d352c0-f621-4b8e-b419-966adb71d71b)
- [优化order by 与 group by](https://www.yuque.com/docs/share/e67300c8-a44b-487b-9e6a-62e14cd04190)
<!-- - [整体优化思路]() -->

**高可用：**

- [主从同步/读写分离](https://xjip3se76o.feishu.cn/docs/doccnmplRlj38wtL5V9hrIc7q4l)

**设计与实现**
 - [InnoDB WAL](docs/database/MySQL/innodb-wal.md)


### Redis

- [学习资料推荐](https://www.yuque.com/docs/share/2f391f98-d9b0-461d-83a5-5300aab8c633)
- 缓存: [关于缓存的一些重要概念](https://xjip3se76o.feishu.cn/docs/doccn5aY5nPi3ylnspqwPaooOR1), [缓存一致性](docs/database/Redis/缓存更新策略.md), [缓存击穿/穿透/雪崩](docs/database/Redis/击穿_穿透_雪崩.md)
- [Redis的单线程&多线程&IO模型](docs/database/Redis/单线程&多线程&IO模型.md)
- [Redis3种高级数据结构](https://xjip3se76o.feishu.cn/docs/doccnxRkiOQlg0NRdCP610tqSsf)
- 持久化: [AOF](https://www.yuque.com/docs/share/c0569ec3-7f9e-4173-959c-399b3ad79847), [RDB](https://www.yuque.com/docs/share/bc561448-6a86-4c44-b255-481def852ae0), [优化方案](https://www.yuque.com/docs/share/c44e4f7e-c4d4-4522-a597-48e6cea4d9cb)
- [底层数据结构](https://xjip3se76o.feishu.cn/docs/doccnIWqCK1fau5qvMTJS5rbYfO)
- [缓存过期策略/内存淘汰机制](https://xjip3se76o.feishu.cn/docs/doccnDzvoXSW5m2NaB7TrIzBAjl)
- [零碎知识点](docs/database/Redis/零碎知识点.md)

高可用
- [主从同步](docs/database/Redis/主从同步.md)
- [Redis Sentinel](https://xjip3se76o.feishu.cn/docs/doccnmpYlkFkKX3kg4shaD4qVSg)
- todo: [Redis Cluster](#)

实战
- [分布式锁](docs/database/Redis/redis-lock.md)
- [限流](docs/database/Redis/限流.md)
- [Redis存储对象信息是用Hash还是String](https://www.upyun.com/tech/article/638/Redis%20%E5%AD%98%E5%82%A8%E5%AF%B9%E8%B1%A1%E4%BF%A1%E6%81%AF%E6%98%AF%E7%94%A8%20Hash%20%E8%BF%98%E6%98%AF%20String.html)
- [Redis实现消息队列](https://xjip3se76o.feishu.cn/docs/doccnkIoycOLEXU9CXO2dXFW4Xf)
- [使用Redis实现防止超卖的方法](docs/database/Redis/使用Redis实现防止超卖的方法.md)

### Elasticsearch

- [es入门](docs/es/es入门.md)
- [我的es学习笔记](https://xjip3se76o.feishu.cn/mindnotes/bmncnIGWaqUckdRIIlKvfh4ezBh)

<!-- ### MongoDB

**基础知识：**

- [快速入门](http://www.macrozheng.com/#/reference/mongodb_start) -->

## 消息队列

消息队列在分布式系统中主要是为了解耦和削峰（也可以拿来与其它系统通信以及分布式事务）。相关阅读： **[消息队列总结](https://xjip3se76o.feishu.cn/docs/doccnBD85O83ONNtjOLkHinML5g)** 。

- [消息队列常见问题总结](https://xjip3se76o.feishu.cn/docs/doccnSm6eNc0XqaIuZBveCMGqWg)


### RabbitMQ

- [RabbitMQ 入门](https://xjip3se76o.feishu.cn/docs/doccn725GpfoylHyz4ZXjkVx0jd)
- [RabbitMQ 提高](https://xjip3se76o.feishu.cn/docs/doccna3dWgYO1wVOtuHwxsgtTYg)

### Kafka

- [Kafka入门](docs/MQ/kafka-入门.md)

## 计算机基础

### 数据结构
我的[github代码仓库](https://github.com/dayueba/DA)，用GO和JS实现常见的数据结构与算法，并有相应的笔记

- [二叉树](docs/DA/tree.md)
- [跳表](#)
- [红黑树基础](#)
- [布隆过滤器](docs/dataStructures-algorithms/dataStructures/RedisBloom.md)

### 算法

- [常见排序算法](docs/DA/sort.md)

- 常见算法问题总结：
  - [几道常见的字符串算法题总结](https://snailclimb.gitee.io/javaguide/#/docs/dataStructures-algorithms/几道常见的子符串算法题)
  - [几道常见的链表算法题总结](https://snailclimb.gitee.io/javaguide/#/docs/dataStructures-algorithms/几道常见的链表算法题)

### 网络

1. [计算机网络常见面试题](https://snailclimb.gitee.io/javaguide/#/docs/network/计算机网络)
2. [计算机网络基础知识总结](https://snailclimb.gitee.io/javaguide/#/docs/network/干货：计算机网络知识总结)
- [在浏览器输入了一个 URL 后发生了什么](docs/network/a-request.md)
- []

### 操作系统

[最硬核的操作系统常见问题总结！](https://snailclimb.gitee.io/javaguide/#/docs/operating-system/basis)


<!-- #### Linux -->

<!-- 1. [后端程序员必备的 Linux 基础知识](https://snailclimb.gitee.io/javaguide/#/docs/operating-system/linux) -->


### 计算机组成原理

### 概率论

### 统计学

## 设计模式
- [20条改善代码质量的编码规范.md](docs/design-patterns/20条改善代码质量的编码规范.md)
- [函数式编程](docs/FunctionalProgramming/FunctionalProgramming.md)

## 云原生

### Docker

- [Docker入门](docs/Docker/docker.md)

### etcd

- [etcd简介](docs/Docker/etcd.md)

<!-- ### Kubernetes -->



## 系统设计

### 攻击技术
- [常见的web攻击技术](docs/system_design/攻击技术.md)

### 认证授权

**[认证授权基础:搞清Authentication,Authorization以及Cookie、Session、Token、OAuth 2、SSO](https://snailclimb.gitee.io/javaguide/#/docs/system-design/authority-certification/basis-of-authority-certification)**

**jwt**

- **[JWT 优缺点分析以及常见问题解决方案](https://snailclimb.gitee.io/javaguide/#/docs/system-design/authority-certification/JWT-advantages-and-disadvantages)**

**SSO(单点登录)**

SSO(Single Sign On)即单点登录说的是用户登陆多个子系统的其中一个就有权访问与其相关的其他系统。举个例子我们在登陆了京东金融之后，我们同时也成功登陆京东的京东超市、京东家电等子系统。相关阅读：**[SSO 单点登录看这篇就够了！](https://snailclimb.gitee.io/javaguide/#/docs/system-design/authority-certification/sso)**

**OAuth2**

todo

## 分布式

- [服务注册与发现](https://xjip3se76o.feishu.cn/docs/doccna6XCw1IcnwiqFMB37QCaCd)
- [zookeeper入门](https://xjip3se76o.feishu.cn/docs/doccnzDT13vhdwntLesvvVDF4Cd)
- [配置中心](https://xjip3se76o.feishu.cn/docs/doccnp7KjzUeyUIrl9ARj2aKXC9)
<!-- - []() -->

### RPC

- [rpc简介](docs/rpc/intro.md)
- [消息协议](docs/rpc/message.md)
- [protobuf与grpc](docs/rpc/protobuf&grpc.md)

### 分布式限流

1. [限流算法有哪些?](https://snailclimb.gitee.io/javaguide/#/docs/system-design/micro-service/limit-request)



## 必会工具

### Git

- [Git入门以及常用操作](https://xjip3se76o.feishu.cn/docs/doccnyUVnidyYanZCKe8BXUIBxb)

## 实战文章
- [如何设计一个秒杀系统](docs/miaosha.md)
- [电商存储中的高频问题解决方案](docs/电商存储中的24个高频问题解决方案.md)
- [实现一个短网址系统](docs/practice/short-url.md)

## 面试指南

1. [简历编写](docs/essential-content-for-interview/简历编写.md)
2. [个人面试经验](docs/essential-content-for-interview/interview.md)

## 学习资源

- [我star的所有仓库](https://github.com/dayueba?tab=stars)
- [有趣的网站推荐](https://xjip3se76o.feishu.cn/docs/doccn0xk8QwCAKqNnqj63C6lk9c)

推荐的学习资源
- [互联网 Java 工程师进阶知识完全扫盲](https://doocs.gitee.io/advanced-java/)
- [Psyduck](https://github.com/SmartKeyerror/Psyduck)

## 待办

## 说明

想法来源于项目：[JavaGuide](https://snailclimb.gitee.io/javaguide/#/)

搭建类似文档类型网站：[《Guide哥手把手教你搭建一个文档类型的网站!免费且高速！》](https://mp.weixin.qq.com/s?__biz=Mzg2OTA0Njk0OA==&mid=2247486555&idx=2&sn=8486026ee9f9ba645ff0363df6036184&chksm=cea24390f9d5ca86ff4177c0aca5e719de17dc89e918212513ee661dd56f17ca8269f4a6e303&token=298703358&lang=zh_CN#rd) 

推荐写作网站：[语雀](https://www.yuque.com/)，飞书文档

### 关于我

这是我看的一些和编程无关，但是对自身发展有用的书，并总结了相应的笔记，推荐大家看看：[地址](https://xjip3se76o.feishu.cn/docs/doccnctBNWVnDHBhSP1ShlQxDHc)

GO+NODE后端开发 对存储和架构比较感兴趣 联系方式：微信号（p320jun）
