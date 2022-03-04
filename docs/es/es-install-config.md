## 版本介绍

### 7.x 更新
1. ES数据存储结构变化：简化了Type 默认使用_doc。es6时，官方就提到了es7会逐渐删除索引type，并且es6时已经规定每一个index只能有一个type。在es7中使用默认的_doc作为type，官方说在8.x版本会彻底移除type。api请求方式也发送变化，如获得某索引的某ID的文档：GET index/_doc/id其中index和id为具体的值
2. ES程序包默认打包jdk：以至于7.x版本的程序包大小突然增大了200MB+, 对比6.x发现，包大了200MB+， 正是JDK的大小
3. 默认配置变化：默认节点名称为主机名，默认分片数改为1，不再是5。


### 6.x 更新


## 源代码目录
- modules：依赖模块目录
- lib：第三方依赖库
- logs: 输出日志目录
- plugins: 插件目录
- bin: 可执行文件目录
- config: 配置文件目录
- data: 数据目录 

## 配置文件
- cluster.name
- node.name
- path.log
- path.data

## 安装与运行

单个实例
```bash
./bin/elasticsearch -E cluster.name=es -E node.name=node1 -E path.data=node1 -d 
```

多个实例
```bash
./bin/elasticsearch -E node.name=node1  -E cluster.name=test -E path.data=node1_data -d
./bin/elasticsearch -E node.name=node2 -E cluster.name=test -E path.data=node2_data -d
./bin/elasticsearch -E node.name=node3 -E cluster.name=test -E path.data=node3_data -d
# 删除进程 ps -ef | grep elasticsearch / kill pid
```

## 开放端口
- 9200: 客户端访问接口，接收Http协议
- 9300: 集群节点间通讯接口，接收tcp协议
