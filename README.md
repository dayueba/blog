# blog
这里是我的个人博客，与大多数程序员写博客的目的一样，总结自己所学的知识和记录一下学习过程中遇到的问题，提高自己的能力，卷起来！

## 目录
- [博客说明(重要！！！)](#说明)
- [changelog](#changelog)
- [学习方法](#学习方法)
- [编程语言](#编程语言)
  - [JavaScript & Node](#JavaScript)
  - [Go](#Go)
- [数据库](#数据库)
  - [MySQL](#MySQL)
  - [Redis](#Redis)
  - [Elasticsearch](#Elasticsearch)
- [消息队列](#消息队列)
  - [RabbitMQ](#RabbitMQ)
  - [Kafka](#Kafka)
- [系统设计](#系统设计)
- [微服务](#微服务)
- [计算机基础](#计算机基础)
- [面试指南](#面试指南)
- [学习资源](#学习资源)
- [关于我](#关于我)
- [放松一下](#放松一下)

<!-- - [计算机基础](#计算机基础)
  - [数据结构](#数据结构)
  - [算法](#算法)
  - [网络](#网络) -->
<!-- - [设计模式](#设计模式) -->
<!-- - [必会工具](#必会工具) -->
  <!-- - [MongoDB](#MongoDB) -->
  <!-- - [云原生](#云原生)
  - [Docker](#Docker)
  - [etcd](#etcd) -->
<!-- - [Python](#Python) -->

## 学习方法

- [总结的一些学习方法以及一些好的习惯](https://xjip3se76o.feishu.cn/mindnotes/bmncniLbhid2PubMtdOEIwon2Jc)

## 编程语言

### JavaScript
- js
  - [数据类型](docs/js/数据类型.md)
  - [深拷贝与浅拷贝](docs/js/深拷贝与浅拷贝.md)
  - [闭包](docs/js/闭包.md)
  - [JS 内存管理机制](docs/js/JS内存管理机制.md)
  - [promise详解](docs/js/promise.md)
- ts: TypeScript不是一门新的编程语言，而是JavaScript的超集。提供了强大的类型系统，可以解决一大堆问题。TypeScript 是一门中间语言，最终它还需要转译为纯 JavaScript，再交给各种终端解释、执行。
  - [TypeScript](docs/js/typescript.md)
  - [类型](docs/js/ts/类型.md)
- Node.js
  - [Nodejs入门](docs/js/nodejs/node.md)
  - [Node事件循环机制](docs/js/事件循环机制.md)

### Go

- 数据结构
  - [切片和数组](https://xjip3se76o.feishu.cn/wiki/wikcnFg1jzo0hRVon704K8TdBYc)
  - [channel](https://xjip3se76o.feishu.cn/wiki/wikcnJvxiKIojsPmj6yagSkEJ6d)
  - [map](https://xjip3se76o.feishu.cn/wiki/wikcn2iP5uc5pvexhSq35JjU6ed)
- runtime
  - [GMP](https://xjip3se76o.feishu.cn/wiki/wikcnsb57fiHgpYySiaW5XVAmgb)
  - [GC](https://xjip3se76o.feishu.cn/wiki/wikcnTosMFf6NSUxT5MOng29rad)
- 并发
  - [goroutine](https://xjip3se76o.feishu.cn/wiki/wikcnAAPUirTrjeiDDRhCPLHOGc)
  - [SingleFlight](https://xjip3se76o.feishu.cn/wiki/wikcn1FHGexi9CTLPDpAFaNc76d)

<!-- ### Python

- todo: [装饰器]()

新特性
- [海象运算符 & 类型注解](https://xjip3se76o.feishu.cn/docs/doccnXgd4NaLIMMZLHF2S8IoHZf) -->


## 数据库

### MySQL

基础：
- [MySQL8.0新特性](https://xjip3se76o.feishu.cn/docs/doccnEzv7JuedymQlUyo1w9D6Xd#lCIfAG)


mysql的提高包括：SQL 语句优化、索引原理、MySQL 锁、事务、MySQL 安全、分库分表、读写分离、MySQL 操作规范等

<!-- - [我的MySQL文章合集](https://www.yuque.com/u1169619/bgwsg4#%20%E3%80%8AMySQL%E3%80%8B) -->
- [自己整理的几道容易出错的面试题](docs/database/MySQL/mysql面试题.md)
- [聊聊主键](docs/database/MySQL/mysql-primary-key.md)
- [MySQL 那些常见的错误设计规范](https://mp.weixin.qq.com/s?__biz=MjM5ODc5ODgyMw==&mid=2653585806&idx=1&sn=5e00837028440d41bea2e35dcee2d215&chksm=bd1b15068a6c9c101e1d3d1e8a74219fa696a475017b91cc4b5f8388b90596c0663f13fa1ae4&mpshare=1&scene=2&srcid=0709WZNZPqskWXlsHZJ3T5uX&sharer_sharetime=1625827270022&sharer_shareid=a9f162b83d3be451174be9ec97298b2b#rd)

**设计与使用**
- [MySQL 中存储时间的最佳实践](https://www.upyun.com/tech/article/652/MySQL%20%E4%B8%AD%E5%AD%98%E5%82%A8%E6%97%B6%E9%97%B4%E7%9A%84%E6%9C%80%E4%BD%B3%E5%AE%9E%E8%B7%B5.html)
- [开发与设计规范](docs/database/MySQL/开发与设计规范.md)
- [一些错误的设计规范](https://xjip3se76o.feishu.cn/docs/doccn6NpsRQDvzmcXb2oEqV3vee)
- [把mysql当成nosql使用](https://xjip3se76o.feishu.cn/docs/doccnn15sICaevRBvy99h21fVBc)

**总结：**

- [事务](https://xjip3se76o.feishu.cn/docs/doccne4DKKKmA0Tpad2SPhjEnPe), [mvcc](docs/database/MySQL/mvcc.md)
- [存储引擎](https://xjip3se76o.feishu.cn/docs/doccnDM66eaPlUOzaPo5SVptJLf)
- [一条SQL语句在MySQL中如何执行的](docs/database/MySQL/一条sql语句在mysql中如何执行的.md)
- 索引：[索引实战](docs/database/MySQL/索引实战.md)，[索引总结2](https://xjip3se76o.feishu.cn/docs/doccnmlh4wJR7RlNN8QsmIk8IVr)
- 锁: [全局锁&表锁&行锁](docs/database/MySQL/lock.md), [死锁](docs/database/MySQL/dead-lock.md), [意向锁、排它锁以及共享锁]()

**日志文件**
- [binlog](https://xjip3se76o.feishu.cn/docs/doccnoG4mp3cGrEDKHSGbI7e3dg)
- [redo log](https://xjip3se76o.feishu.cn/docs/doccn4C4wL63WUsSdnPSxYik3We)
- [undo log](https://xjip3se76o.feishu.cn/docs/doccnUL36FWaKgni0yUE5e8jJxf)

**InnoDB 数据存储**
- [行格式](https://xjip3se76o.feishu.cn/docs/doccn8V3i3yekKBJlao9KiKJKye)
- [数据页结构](docs/database/MySQL/innodb-page.md)
- [内存结构](https://xjip3se76o.feishu.cn/docs/doccnFVu43rXnFyjFiYD2j7A66d)
- [磁盘结构](https://xjip3se76o.feishu.cn/docs/doccnL3r6wkI24PNEgIop1BNZAg)

**sql优化**


**高可用：**

- [主从同步/读写分离](https://xjip3se76o.feishu.cn/docs/doccnmplRlj38wtL5V9hrIc7q4l)

**设计与实现**
- [为什么MySQL使用B+Tree](docs/database/MySQL/为什么MySQL使用B+Tree.md)
- [InnoDB WAL](docs/database/MySQL/innodb-wal.md)
- [InnoDB group commit](docs/database/MySQL/innodb-group-commit.md)
- [InnoDB undo log 与 mvcc](docs/database/MySQL/innodb-undo-log-and-mvcc.md)
- [MySQL Cost-Based Optimizer](docs/database/MySQL/MySQL为什么有时候会选错索引.md)

### Redis

**缓存**
- [关于缓存的一些重要概念](https://xjip3se76o.feishu.cn/docs/doccn5aY5nPi3ylnspqwPaooOR1)
<!-- - [缓存数据一致性](docs/database/Redis/缓存更新策略.md) -->
- [缓存数据一致性](https://xjip3se76o.feishu.cn/docx/doxcnRafKPJ1lYFtm5iiGDfWVRc)
- [7大缓存经典问题](https://xjip3se76o.feishu.cn/docs/doccnnQ3isgYklfKQqSvxaFWmAh)

--

- [学习资料推荐](https://www.yuque.com/docs/share/2f391f98-d9b0-461d-83a5-5300aab8c633)，[学习资料推荐](https://xjip3se76o.feishu.cn/docs/doccnPKZHMNHqnychGUCrwS6fXc)
- [Redis的单线程&多线程&IO模型](docs/database/Redis/单线程&多线程&IO模型.md)
- [缓存过期策略/内存淘汰机制](https://xjip3se76o.feishu.cn/docs/doccnDzvoXSW5m2NaB7TrIzBAjl)
- [零碎知识点](docs/database/Redis/零碎知识点.md)
- [Redis单线程与多线程](https://xjip3se76o.feishu.cn/docs/doccn8OCWaPKKv6Wx2xJHxriXtd)
- [Resp](https://xjip3se76o.feishu.cn/docs/doccncKmo98UNh0PKnCHvHVpBkf)

**数据结构**
<!-- - [五种基础数据结构](https://lrita.github.io/2019/03/13/the-internal-of-file-syscall/#fsyncfdatasync) -->
- [五种基础数据结构](https://xjip3se76o.feishu.cn/docs/doccnYVIAWxerOZDyCH5aG36psd)
- [Redis3种高级数据结构](https://xjip3se76o.feishu.cn/docs/doccnxRkiOQlg0NRdCP610tqSsf)
- [底层数据结构](https://xjip3se76o.feishu.cn/docs/doccnIWqCK1fau5qvMTJS5rbYfO)

**持久化**

记住：持久化的目的是为了重启时快速恢复数据
- [持久化简介](https://xjip3se76o.feishu.cn/docs/doccnMeJBkpmpabnlyModXbJHcg)
- [AOF](https://xjip3se76o.feishu.cn/docs/doccnW6NiitQBCw2bVahUo48wnb)，[AOF重写](https://xjip3se76o.feishu.cn/docs/doccn1yGrTMNSgA5FDqqBkt4iih)
- [RDB](https://xjip3se76o.feishu.cn/docs/doccndeuPUjLL44q0xr56i9yGXb)
- [混合持久化](https://xjip3se76o.feishu.cn/docs/doccnY9oQTBEJHy07bZYIusAJIf)

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

<!-- ### 其它缓存
- todo: [pika](#) -->

<!-- ### memcached -->
<!-- - todo: [简介](#) -->

### Elasticsearch

- [es入门](docs/es/es简介.md)
- [安装与配置](docs/es/es-install-config.md)
- [索引基本操作](docs/es/索引基本操作.md)
- [文档基本操作](https://xjip3se76o.feishu.cn/docs/doccn9LvZ8QYW45mF76GYrFPAwb)
- [mapping](docs/es/mapping.md)

**搜索**
- [全文检索](https://xjip3se76o.feishu.cn/docs/doccnLWrq8ZCaE2Hous06b5wAuc)
- [term精确搜索](https://xjip3se76o.feishu.cn/docs/doccnrIWBqaG1y1HpLNo9NDLX2Y)

--
- [我的es学习笔记](https://xjip3se76o.feishu.cn/mindnotes/bmncnIGWaqUckdRIIlKvfh4ezBh)


<!-- ### MongoDB

**基础知识：**

todo
- [高可用]() -->

## 消息队列

消息队列在分布式系统中主要是为了解耦和削峰（也可以拿来与其它系统通信以及分布式事务）。相关阅读： **[消息队列总结](https://xjip3se76o.feishu.cn/docs/doccnBD85O83ONNtjOLkHinML5g)** 。

- [消息队列入门](docs/MQ/mq-intro.md)
- [主流消息中间件及选型](docs/MQ/mq-select.md)
- [消息队列常见问题总结](https://xjip3se76o.feishu.cn/docs/doccnSm6eNc0XqaIuZBveCMGqWg)


### RabbitMQ
- [AMQP协议](docs/MQ/amqp.md)
- [RabbitMQ 入门](https://xjip3se76o.feishu.cn/docs/doccn725GpfoylHyz4ZXjkVx0jd)
- [RabbitMQ存储机制](https://xjip3se76o.feishu.cn/docs/doccnW3NCL6iAhgsHIEQJmVEZ8c)
- [ttl机制](https://xjip3se76o.feishu.cn/docs/doccntQ6Lr9wvDepytGvDqfcPdc)
- [配置文件](https://upyun.feishu.cn/docs/doccnXFypkaCHSjhyiZQOHSTCUh)
- [connection和channel的关系](https://xjip3se76o.feishu.cn/docs/doccnleNUhJqsUN2KUtSU9Zv3he)
- [rabbitmq可靠性](https://xjip3se76o.feishu.cn/docs/doccnQ798zyK4xw393BJ8kMO2oc)
- [RabbitMQ集群与运维](https://xjip3se76o.feishu.cn/docs/doccnSRSj6G14onkVvi6ng9Z1lh)
- [一些QA](https://xjip3se76o.feishu.cn/docs/doccnviQTmErPxNlTM8GEvIMEtg)

### Kafka

- [Kafka入门](docs/MQ/kafka-入门.md)
- [基本概念](docs/MQ/kafka/基本概念.md)
- [常用配置](https://xjip3se76o.feishu.cn/docs/doccn0BcJhDA0fFtkuAJ5GRhVke)
- [基本操作](docs/MQ/kafka/基本操作.md)

<!-- ## 计算机基础

### 数据结构
我的[github代码仓库](https://github.com/dayueba/DA)，用GO和JS实现常见的数据结构与算法，并有相应的笔记

- [二叉树](docs/DA/tree.md)
- [跳表](#)
- [红黑树基础](#)
- [布隆过滤器](docs/dataStructures-algorithms/dataStructures/RedisBloom.md)

### 算法

常见算法问题总结：
- [常见排序算法](docs/DA/sort.md)
- todo [常见的字符串算法题](#)
- todo [常见的链表算法题](#)

### 网络

- [在浏览器输入了一个 URL 后发生了什么](docs/network/a-request.md)

<!-- ### 操作系统 -->

<!-- ### 计算机组成原理

### 概率论

### 统计学 --> -->

<!-- ## 设计模式
- [20条改善代码质量的编码规范.md](docs/design-patterns/20条改善代码质量的编码规范.md)
- [函数式编程](docs/FunctionalProgramming/FunctionalProgramming.md) -->

## 系统设计
工程能力

- [常见的web攻击技术](docs/system_design/攻击技术.md)
- [如何设计一个秒杀系统](docs/miaosha.md)
- [电商存储中的高频问题解决方案](docs/电商存储中的24个高频问题解决方案.md)
- [实现一个短网址系统](https://xjip3se76o.feishu.cn/docs/doccnGJcry3GVgHIHRtZoHw3AdO)
- [Timeline Feed系统设计](https://xjip3se76o.feishu.cn/wiki/wikcno6bBPVTm3xDeoWp5z6FLYg)
<!-- - [重构](https://xjip3se76o.feishu.cn/docx/doxcnISkL1wbh4dtAOue2Wfgs6b) -->

## 微服务

- 微服务治理
  - [服务注册与发现](https://xjip3se76o.feishu.cn/docs/doccna6XCw1IcnwiqFMB37QCaCd)
  - [zookeeper入门](https://xjip3se76o.feishu.cn/docs/doccnzDT13vhdwntLesvvVDF4Cd)
  - [配置中心](https://xjip3se76o.feishu.cn/docs/doccnp7KjzUeyUIrl9ARj2aKXC9)
  - [过载保护/限流/熔断](https://xjip3se76o.feishu.cn/wiki/wikcnRaVLjH67npX4rB9ZWrsZnh)
- RPC
  - [rpc简介](docs/rpc/intro.md)
  - [消息协议](docs/rpc/message.md)
  - [protobuf与grpc](docs/rpc/protobuf&grpc.md)
- 云原生
  - [Docker入门](docs/Docker/docker.md)
  - [etcd简介](https://xjip3se76o.feishu.cn/docs/doccnzyWADqitACeRpDPRxxE4Kc)

<!-- ## 必会工具

- git
  - [Git入门以及常用操作](https://xjip3se76o.feishu.cn/docs/doccnyUVnidyYanZCKe8BXUIBxb) -->

## 计算机基础
- [网络IO模型](https://xjip3se76o.feishu.cn/docx/doxcnp7jIh58xLsadhkNHKWpMOh)

## 面试指南

1. [简历编写](docs/essential-content-for-interview/简历编写.md)
2. [个人面试经验](docs/essential-content-for-interview/interview.md)
3. [毛老师教你如何搞定面试](https://xjip3se76o.feishu.cn/docx/doxcndCat0MkUtJKUq5V5SQ6N6C)

## 学习资源
- [学习资料推荐](https://xjip3se76o.feishu.cn/mindnotes/bmncnh1mneKcbqrx45SuUDow0af)
- [有趣的网站推荐](https://xjip3se76o.feishu.cn/docs/doccn0xk8QwCAKqNnqj63C6lk9c)
- [互联网 Java 工程师进阶知识完全扫盲](https://doocs.gitee.io/advanced-java/)
- [Psyduck](https://github.com/SmartKeyerror/Psyduck)

<!-- ## 待学习
- 操作系统
- 计算机组成原理
- 概率论
- 统计学 -->

## 说明
- 想法来源于此项目：[JavaGuide](https://snailclimb.gitee.io/javaguide/#/) 。可以参考这篇文章搭建类似的网站：[《Guide哥手把手教你搭建一个文档类型的网站!免费且高速！》](https://mp.weixin.qq.com/s?__biz=Mzg2OTA0Njk0OA==&mid=2247486555&idx=2&sn=8486026ee9f9ba645ff0363df6036184&chksm=cea24390f9d5ca86ff4177c0aca5e719de17dc89e918212513ee661dd56f17ca8269f4a6e303&token=298703358&lang=zh_CN#rd) 。
- 为什么没有这样像其他大佬一样，买服务器，买域名，单独部署呢？
  - 目前这样最大的好处就是免费！刚开始我们写博客主要目的只是为了总结一下自己学到的知识，大概率是没什么人看的，所以前期花费金钱去买服务器显得没有那么划算。
- 为什么大部分文章都是用飞书文档写的？
  - 虽然 docsify 框架渲染的文章更好看，比飞书文档好看多了，虽然飞书文档功能很多，但是是真的丑。
  - 但是使用飞书文档的一个重要好处就是可以评论文档，写博客最好还是支持一下评论，不然万一别人有问题，人家需要加你微信才能问你，除非你文章写的特别好，不然大部分人是不会加你的。没有评论区，写博客会有点自嗨的感觉。
  - 类似的还有语雀，但是由于工作使用的办公软件是飞书，所以就用飞书文档了
  - 直接md文档还有一个问题，部署的时候容易审核过不去（用github部署应该没问题，但是国内访问慢），重点是只告诉你哪个文档有问题，没有更详细的信息，修改起来很麻烦
  - 学习过程中可能有想补充的可以立马写到飞书文档里，如果直接写MD，还需要推送到仓库，再重新部署，麻烦
- 可能的侵权问题
  - 总结的博客里，会放上一些自己参考的资料，如果侵权了，可以加我微信（p320jun），联系后删除

## changelog
- 2022-09-08
  - 增加go相关文章
- 2022-09-07
  - 增加几篇飞书文档中的文章
- 2022-09-06
  - 修改主页描述，删除大量低质量文章
- 2022-08-23
  - 增加go数据结构map文章
- 2022-08-22
  - 删除一些认为质量较低的博客
  - 修改主页，修改一些描述，删除一些失效连接
  - 增加go_数据结构 文章

## 关于我

这是我看的一些和编程无关，但是对自身发展有用的书，并总结了相应的笔记，推荐大家看看：[地址](https://xjip3se76o.feishu.cn/docs/doccnctBNWVnDHBhSP1ShlQxDHc)

Go+Node.js后端开发 对存储和架构比较感兴趣 联系方式：微信号（p320jun）

## 放松一下
推荐一些个人觉得好看的书，好玩的游戏以及各种有趣的东西
