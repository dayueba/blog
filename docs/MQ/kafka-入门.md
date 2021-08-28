## 简介
Kafka 是一个分布式流式处理平台。

流平台具有三个关键功能：

1. 消息队列：发布和订阅消息流，这个功能类似于消息队列，这也是 Kafka 也被归类为消息队列的原因。
2. 容错的持久方式存储记录消息流： Kafka 会把消息持久化到磁盘，有效避免了消息丢失的风险·。
3. 流式处理平台： 在消息发布的时候进行处理，Kafka 提供了一个完整的流式处理类库。

Kafka 主要有两大应用场景：

1. 消息队列 ：建立实时流数据管道，以可靠地在系统或应用程序之间获取数据。
2. 数据处理： 构建实时的流数据处理程序来转换或处理数据流。

关于 Kafka 几个非常重要的概念：

1. Kafka 将记录流（流数据）存储在 topic 中。
2. 每个记录由一个键、一个值、一个时间戳组成。

## 特点
- 同时为发布和订阅提供高吞吐量。据了解，Kafka每秒可以生产约25万消息（50 MB），每秒处理55万消息（110 MB）。
- 可进行持久化操作。将消息持久化到磁盘，因此可用于批量消费，例如ETL，以及实时应用程序。
- 分布式系统，易于向外扩展。所有的producer、broker和consumer都会有多个，均为分布式的。无需停机即可扩展机器。
- 消息被处理的状态是在consumer端维护，而不是由server端维护。当失败时能自动平衡。
- 支持在线和离线的场景。

## 优秀设计
- 内存访问：直接使用 linux 文件系统的cache，来高效缓存数据，对数据进行读取和写入。
- 数据磁盘持久化：消息不在内存中cache，直接写入到磁盘，充分利用磁盘的顺序读写性能。
- zero-copy：减少IO操作步骤
    - 采用linux Zero-Copy提高发送性能。传统的数据发送需要发送4次上下文切换，采用sendfile系统调用之后，数据直接在内核统上下文切换减少为2次。根据测试结果，可以提高60%的数据发送性能。Zero-Copy详细的技术细节可以参考：
- 对消息的处理：
    - 支持数据批量发送

## 基本概念

## Broker
可以看作是一个独立的 Kafka 实例。多个 Kafka Broker 组成一个 Kafka Cluster。

### Topic & Partition
- Topic：特指Kafka处理的消息源（feeds of messages）的不同分类。Kafka 将生产者发布的消息发送到 Topic（主题） 中(类似RabbitMQ发送消息到交换机)，需要这些消息的消费者可以订阅这些 Topic（主题）
- Partition：Topic物理上的分组，一个topic可以分为多个partition，每个partition是一个有序的队列，并且同一 Topic 下的 Partition 可以分布在不同的 Broker 上，这也就表明一个 Topic 可以横跨多个 Broker 。partition中的每条消息都会被分序的id（offset）。

另外，还有一点我觉得比较重要的是 Kafka 为分区（Partition）引入了多副本（Replica）机制。分区（Partition）中的多个副本之间会有一个叫做 leader 的家伙，其他副本称为 follower。我们发送的消息会被发送到 leader 副本，然后 follower 副本才能从 leader 副本中拉取消息进行同步。

生产者和消费者只与 leader 副本交互。你可以理解为其他副本只是 leader 副本的拷贝，它们的存在只是为了保证消息存储的安全性。当 leader 副本发生故障时会从 follower 中选举出一个 leader,但是 follower 中如果有和 leader 同步程度达不到要求的参加不了 leader 的竞选。

**Kafka 的多分区（Partition）以及多副本（Replica）机制有什么好处呢？**
1. Kafka 通过给特定 Topic 指定多个 Partition, 而各个 Partition 可以分布在不同的 Broker 上, 这样便能提供比较好的并发能力（负载均衡）。
2. Partition 可以指定对应的 Replica 数, 这也极大地提高了消息存储的安全性, 提高了容灾能力，不过也相应的增加了所需要的存储空间。

- Message：消息，是通信的基本单位，每个producer可以向一个topic（主题）发布一些消息。
- Producers：消息和数据生产者，向Kafka的一个topic发布消息的过程叫做producers。
- Consumers：消息和数据消费者，订阅topics并处理其发布的消息的过程叫做consumers。
- Broker：缓存代理，Kafka集群中的一台或多台服务器统称为broker。

## Zookeeper 在 Kafka 中的作用
ZooKeeper 主要为 Kafka 提供元数据的管理的功能。

1. Broker 注册 ：在 Zookeeper 上会有一个专门用来进行 Broker 服务器列表记录的节点。每个 Broker 在启动时，都会到 Zookeeper 上进行注册，即到/brokers/ids 下创建属于自己的节点。每个 Broker 就会将自己的 IP 地址和端口等信息记录到该节点中去
2. Topic 注册 ： 在 Kafka 中，同一个Topic 的消息会被分成多个分区并将其分布在多个 Broker 上，这些分区信息及与 Broker 的对应关系也都是由 Zookeeper 在维护。比如我创建了一个名字为 my-topic 的主题并且它有两个分区，对应到 zookeeper 中会创建这些文件夹：/brokers/topics/my-topic/Partitions/0、/brokers/topics/my-topic/Partitions/1
3. 负载均衡 ：上面也说过了 Kafka 通过给特定 Topic 指定多个 Partition, 而各个 Partition 可以分布在不同的 Broker 上, 这样便能提供比较好的并发能力。 对于同一个 Topic 的不同 Partition，Kafka 会尽力将这些 Partition 分布到不同的 Broker 服务器上。当生产者产生消息后也会尽量投递到不同 Broker 的 Partition 里面。当 Consumer 消费的时候，Zookeeper 可以根据当前的 Partition 数量以及 Consumer 数量来实现动态负载均衡。

## 发送消息的流程
- Producer根据指定的partition方法（round-robin、hash等），将消息发布到指定topic的partition里面
- kafka集群接收到Producer发过来的消息后，将其持久化到硬盘，并保留消息指定时长（可配置），而不关注消息是否被消费。
- Consumer从kafka集群pull数据，并控制获取消息的offset

## 消息模型
### 队列模型
与Rabbit的简单模式一样，由一个生产者，一个消费者，一个队列组成。

### 发布订阅
与Rabbit的fanout模式一样，只不过消费者订阅的是Topic