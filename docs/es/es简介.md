> 文档地址：https://www.elastic.co/guide/en/elasticsearch/reference/current/index.html

## 功能
1. 分布式实时搜索引擎
    1. 使用场景：百度、谷歌，站内搜索
2. 大数据近实时分析引擎
3. 海量存储

## 特点
1. 

## 核心概念

### Near Realtime
近实时，有两层意思：

1. 从写入数据到数据可以被搜索到有一个小延迟（大概是 1s）
2. 基于 ES 执行搜索和分析可以达到秒级

### Cluster 集群

集群包含多个节点，每个节点属于哪个集群都是通过一个配置来决定的，对于中小型应用来说，刚开始一个集群就一个节点很正常。

### Node 节点
Node 是集群中的一个节点，节点也有一个名称，默认是随机分配的。默认节点会去加入一个名称为 elasticsearch 的集群。如果直接启动一堆节点，那么它们会自动组成一个 elasticsearch 集群，当然一个节点也可以组成 elasticsearch 集群。

### Document & field
一个 document 可以是一条客户数据、一条商品分类数据、一条订单数据，通常用 json 数据结构来表示。每个 index 下的 type，都可以存储多条 document。一个 document 里面有多个 field，每个 field 就是一个数据字段。

### Index
索引包含了一堆有相似结构的文档数据，比如商品索引。一个索引包含很多 document，一个索引就代表了一类相似或者相同的 ducument。

对应mysql中的数据库

### Type
对应mysql的表

注意ES每个大版本之间区别很大：
- ES 5.x中一个index可以有多种type。
- ES 6.x中一个index只能有一种type。
- ES 7.x中只有一个index:_doc。以后要逐渐移除type这个概念。

### mapping
mapping定义了每个字段的类型等信息。相当于关系型数据库中的表结构。

详细地址：https://www.elastic.co/guide/en/elasticsearch/reference/current/mapping-types.html#_multi_fields_2
