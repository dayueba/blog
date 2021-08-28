## 什么是RPC
RPC（Remote Procedure Call）—远程过程调用，它是一种通过网络从远程计算机程序上请求服务，而不需要了解底层网络技术的协议。比如两个不同的服务 A、B 部署在两台不同的机器上，那么服务 A 如果想要调用服务 B 中的某个方法该怎么办呢？使用 HTTP请求 当然可以，但是可能会比较慢而且一些优化做的并不好。 RPC 的出现就是为了解决这个问题。


## 如何设计一个RPC框架

## protobuf
一种轻量 高效的结构化数据存储格式，性能比json强很多

一个例子
```protobuf
syntax = "proto3";

option java_package=""; // 作用： 

// 定义方法
service Greeter {
  rpc SayHello (HelloRequest) returns (HelloReply) {}
  rpc sayHelloAgain (HelloRequest) returns (HelloReply) {}
  rpc sayHelloAsync(HelloRequest) returns (HelloReply) {}
}

// 定义请求参数格式
message HelloRequest {
  string name = 1;
}

// 定义返回参数格式
message HelloReply {
  string message = 1;
}
```
语法：
- 结尾需要分号
- [数据类型](https://developers.google.com/protocol-buffers/docs/proto3#scalar), 每个类型都有对应的默认值
- message字段中的修饰符 
    - singular: 表示成员有0个或者一个，一般省略不写
    - repeated: 可以包含多个


在proto文件中通过`import`引入其他proto文件，比如引入官方定义好的空消息。`import "geogle/protobuf/empty.proto"`

**嵌入消息类型**
 ```protobuf
message HelloReply {
  string message = 1;
  repeated User user = 2; 
}

message User {
  string name = 1;
}
```
可以直接写成
```protobuf 
message HelloReply {
  string message = 1;
  message User {
    string name = 1;
  }
  repeated User user = 2; 
}
```

枚举类型

- https://developers.google.com/protocol-buffers/docs/overview?hl=en#enum

Map

- https://developers.google.com/protocol-buffers/docs/overview?hl=en#maps

时间戳
```protobuf

```
 

## GRPC

geogle推出一个rpc框架，采用的通信协议是http/2，序列化协议是protobuf


## 需要注意的点

### protobuf文件修改了怎么办

比如我们原来是

```protobuf
message HelloReply {
  string message = 1;
  string name = 2;
}
```

我们修改成
```protobuf
message HelloReply {
  string name = 1;
  string message = 2;
}
```
只是把两个字段的返回值调换了一下位置。由于序列化的时候是按照编号映射，而不是字段名（json是按照字段名），所以此时会出现bug。
