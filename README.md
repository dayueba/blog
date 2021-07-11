# blog
这是我的个人博客主页

记录自己写的博客以及推荐一些学习资料

## 目录
- [学习方法](#学习方法)
- [编程语言](#编程语言)
  - [Python](#Python)
  - [JavaScript](#JavaScript)
  - [Go](#Go)
- [数据库](#数据库)
  - [MySQL](#MySQL)
  - [Redis](#Redis)
  - [MongoDB](#MongoDB)
- [数据结构与算法](#数据结构和算法)
  - [数据结构](#数据结构)
  - [算法](#算法)
- [全文搜索引擎](#全文搜索引擎)
  - [Elasticsearch](#Elasticsearch)
- [消息队列](#消息队列)
  - [RabbitMQ](#RabbitMQ)
  - [Kafka](#Kafka)
- [设计模式](#设计模式)
- [系统设计](#系统设计)
  - [必备知识](#必备知识)
  - [认证授权](#认证授权)
  - [大型网站架构](#大型网站架构)
    - [性能测试](#性能测试)
    - [高并发](#高并发)
    - [高可用](#高可用)
- [分布式](#分布式)
  - [RPC](#RPC)
  - [分布式限流](#分布式限流)
- [必会工具](#必会工具)
  - [Git](#Git)
  - [Docker](#Docker)
- [网络](#网络)
- [操作系统](#操作系统)
  - [Linux](#Linux)
- [实战文章](#实战文章)
- [面试指南](#面试指南)
- [学习资源](#学习资源)
  - [学习方法](#学习方法)
  - [书籍](#书籍)
  - [优质博客](#优质博客)
  - [实战项目](#实战项目)
  - [优质课程](#优质课程)
- [待办](#待办)
- [说明](#说明)

## 学习方法
## 编程语言

### Python

- [我的Python文章合集](https://www.yuque.com/u1169619/kb2a00#%20%E3%80%8APython%E3%80%8B)

### JavaScript

### Go

## 数据库

### MySQL
mysql的提高包括：SQL 语句优化、索引原理、MySQL 锁、事务、MySQL 安全、分库分表、读写分离、MySQL 操作规范等

- [学习资料推荐](https://www.yuque.com/docs/share/533eeaef-1f2c-4518-ba00-e33fc9df286a)
- [我的MySQL文章合集](https://www.yuque.com/u1169619/bgwsg4#%20%E3%80%8AMySQL%E3%80%8B)
- [自己整理的几道面试题](docs/database/MySQL/mysql面试题.md)
- [MySQL 那些常见的错误设计规范](https://mp.weixin.qq.com/s?__biz=MjM5ODc5ODgyMw==&mid=2653585806&idx=1&sn=5e00837028440d41bea2e35dcee2d215&chksm=bd1b15068a6c9c101e1d3d1e8a74219fa696a475017b91cc4b5f8388b90596c0663f13fa1ae4&mpshare=1&scene=2&srcid=0709WZNZPqskWXlsHZJ3T5uX&sharer_sharetime=1625827270022&sharer_shareid=a9f162b83d3be451174be9ec97298b2b#rd)

**总结：**

1. **[【推荐】MySQL/数据库 知识点总结](https://snailclimb.gitee.io/javaguide/#/docs/database/MySQL)**
3. **[一千行MySQL学习笔记](https://snailclimb.gitee.io/javaguide/#/docs/database/一千行MySQL命令)**
4. [MySQL高性能优化规范建议](https://snailclimb.gitee.io/javaguide/#/docs/database/MySQL高性能优化规范建议)
5. [一条SQL语句在MySQL中如何执行的](https://snailclimb.gitee.io/javaguide/#/docs/database/一条sql语句在mysql中如何执行的)
6. **[MySQL 中存储时间的最佳实践](https://www.upyun.com/tech/article/652/MySQL%20%E4%B8%AD%E5%AD%98%E5%82%A8%E6%97%B6%E9%97%B4%E7%9A%84%E6%9C%80%E4%BD%B3%E5%AE%9E%E8%B7%B5.html)**
7. [聊聊主键](docs/database/MySQL/聊聊主键.md)

**面试必问：**

- 索引：[数据库索引总结](docs/database/MySQL/index.md)

### Redis

- [学习资料推荐](https://www.yuque.com/docs/share/2f391f98-d9b0-461d-83a5-5300aab8c633)
- [关于缓存的一些重要概念(Redis前置菜)](https://snailclimb.gitee.io/javaguide/#/docs/database/Redis/some-concepts-of-caching)
- [Redis存储对象信息是用Hash还是String](https://www.upyun.com/tech/article/638/Redis%20%E5%AD%98%E5%82%A8%E5%AF%B9%E8%B1%A1%E4%BF%A1%E6%81%AF%E6%98%AF%E7%94%A8%20Hash%20%E8%BF%98%E6%98%AF%20String.html)
- [redis常见知识点](docs/database/Redis/redis.md)
- [Redis 常见问题总结](https://snailclimb.gitee.io/javaguide/#/docs/database/Redis/redis-all)
- [Redis 缓存击穿，穿透，雪崩](docs/database/Redis/击穿_穿透_雪崩.md)
- [Redis面试题](docs/database/Redis/面试题.md)
- Redis系列文章合集：
  1. 数据结构和算法：[5种基本数据结构](https://snailclimb.gitee.io/javaguide/#/docs/database/Redis/redis-collection/Redis(1)——5种基本数据结构)，[跳跃表](https://snailclimb.gitee.io/javaguide/#/docs/database/Redis/redis-collection/Redis(2)——跳跃表)，[神奇的HyperLoglog解决统计问题](https://snailclimb.gitee.io/javaguide/#/docs/database/Redis/redis-collection/Reids(4)——神奇的HyperLoglog解决统计问题)，[亿级数据过滤和布隆过滤器](https://snailclimb.gitee.io/javaguide/#/docs/database/Redis/redis-collection/Redis(5)——亿级数据过滤和布隆过滤器)，[GeoHash查找附近的人](https://snailclimb.gitee.io/javaguide/#/docs/database/Redis/redis-collection/Redis(6)——GeoHash查找附近的人)
  2. [持久化](https://snailclimb.gitee.io/javaguide/#/docs/database/Redis/redis-collection/Redis(7)——持久化)
  3. [发布订阅与Stream](https://snailclimb.gitee.io/javaguide/#/docs/database/Redis/redis-collection/Redis(8)——发布订阅与Stream)
  4. [史上最强【集群】入门实践教程](https://snailclimb.gitee.io/javaguide/#/docs/database/Redis/redis-collection/Redis(9)——集群入门实践教程)
  5. [Redis数据类型、编码、底层数据结构的关系看这篇](https://snailclimb.gitee.io/javaguide/#/docs/database/Redis/redis-collection/Redis(10)——Redis数据类型、编码、数据结构的关系)

### MongoDB

**基础知识：**

- [快速入门](http://www.macrozheng.com/#/reference/mongodb_start)

## 数据结构与算法

### 数据结构

- [红黑树基础]()
- [不了解布隆过滤器？一文给你整的明明白白！](https://snailclimb.gitee.io/javaguide/#/docs/dataStructures-algorithms/data-structure/bloom-filter)
- [数据结构知识学习与面试](https://snailclimb.gitee.io/javaguide/#/docs/dataStructures-algorithms/数据结构)

### 算法

- 常见算法问题总结：
  - [几道常见的字符串算法题总结](https://snailclimb.gitee.io/javaguide/#/docs/dataStructures-algorithms/几道常见的子符串算法题)
  - [几道常见的链表算法题总结](https://snailclimb.gitee.io/javaguide/#/docs/dataStructures-algorithms/几道常见的链表算法题)

## 全文搜索引擎

### Elasticsearch

## 消息队列

消息队列在分布式系统中主要是为了解耦和削峰。相关阅读： **[消息队列总结](https://snailclimb.gitee.io/javaguide/#/docs/system-design/data-communication/message-queue)** 。

### RabbitMQ

- [RabbitMQ 入门](https://snailclimb.gitee.io/javaguide/#/docs/system-design/data-communication/rabbitmq)


### Kafka

- [Kafka入门+SpringBoot整合Kafka系列](https://github.com/Snailclimb/springboot-kafka)
- [Kafka常见面试题总结](https://snailclimb.gitee.io/javaguide/#/docs/system-design/data-communication/kafka-inverview)
- [【加餐】Kafka入门看这一篇就够了](https://snailclimb.gitee.io/javaguide/#/docs/system-design/data-communication/Kafka%E5%85%A5%E9%97%A8%E7%9C%8B%E8%BF%99%E4%B8%80%E7%AF%87%E5%B0%B1%E5%A4%9F%E4%BA%86)

## 设计模式
- [20条改善代码质量的编码规范.md](docs/design-patterns/20条改善代码质量的编码规范.md)

## 系统设计

### 必备知识

**[RestFul API 简明教程](https://snailclimb.gitee.io/javaguide/#/docs/system-design/restful-api)**

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

### 大型网站架构

- [8 张图读懂大型网站技术架构](https://www.yuque.com/docs/share/a8a6e551-5a3f-4348-8da8-7c8a1629837c?#%20《8张图读懂大型网站技术架构》)

- [关于大型网站系统架构你不得不懂的10个问题](https://snailclimb.gitee.io/javaguide/#/docs/system-design/website-architecture/关于大型网站系统架构你不得不懂的10个问题)

#### 性能测试

#### 高并发

#### 高可用

高可用描述的是一个系统在大部分时间都是可用的，可以为我们提供服务的。高可用代表系统即使在发生硬件故障或者系统升级的时候，服务仍然是可用的 。相关阅读： **《[如何设计一个高可用系统？要考虑哪些地方？](https://snailclimb.gitee.io/javaguide/#/docs/system-design/website-architecture/如何设计一个高可用系统？要考虑哪些地方？)》** 。

## 分布式

### RPC

让调用远程服务调用像调用本地方法那样简单。

- [服务之间的调用为啥不直接用 HTTP 而用 RPC？](https://snailclimb.gitee.io/javaguide/#/docs/system-design/data-communication/why-use-rpc)

### 分布式限流

1. [限流算法有哪些?](https://snailclimb.gitee.io/javaguide/#/docs/system-design/micro-service/limit-request)



## 必会工具

### Git

- [Git入门](https://snailclimb.gitee.io/javaguide/#/docs/tools/Git)
- [分支管理-Git flow](http://git-tower.com/learn/git/ebook/cn/command-line/advanced-topics/git-flow)
- [我的Git笔记合集](https://www.yuque.com/books/share/1205240a-67ff-484e-9f4c-1d63e2e34e2c?#%20%E3%80%8Agit%E3%80%8B)

### Docker

- [Docker 基本概念解读](https://snailclimb.gitee.io/javaguide/#/docs/tools/Docker)
- [一文搞懂 Docker 镜像的常用操作！](https://snailclimb.gitee.io/javaguide/#/docs/tools/Docker-Image)
- [我的Docker笔记合集](https://www.yuque.com/books/share/de30a6ba-5e79-4ec6-9748-ce42a56c2534?#%20%E3%80%8ADocker%E3%80%8B)

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

## 实战文章
- [如何设计一个秒杀系统](docs/mall/miaosha.md)
- [电商存储中的24个高频问题解决方案](docs/电商存储中的24个高频问题解决方案.md)

## 面试指南

1. [简历编写](docs/essential-content-for-interview/简历编写.md)
2. [个人面试经验](docs/essential-content-for-interview/interview.md)

## 学习资源

- [我star的所有仓库](https://github.com/dayueba?tab=stars)
- [有趣的网站推荐](https://xjip3se76o.feishu.cn/docs/doccn0xk8QwCAKqNnqj63C6lk9c)
## 待办

## 说明

资源来源自网络。主要参考项目：[JavaGuide](https://snailclimb.gitee.io/javaguide/#/)

只会收集和整理目前正在学习内容的相关资源

Markdown格式参考：[Github Markdown格式](https://guides.github.com/features/mastering-markdown/)

搭建类似文档类型网站：[《Guide哥手把手教你搭建一个文档类型的网站!免费且高速！》](https://mp.weixin.qq.com/s?__biz=Mzg2OTA0Njk0OA==&mid=2247486555&idx=2&sn=8486026ee9f9ba645ff0363df6036184&chksm=cea24390f9d5ca86ff4177c0aca5e719de17dc89e918212513ee661dd56f17ca8269f4a6e303&token=298703358&lang=zh_CN#rd) 

推荐另一个写作网站：[语雀](https://www.yuque.com/)

### 关于我

一个起步较晚，起点较低，但是一直在努力的程序员。
