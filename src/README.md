# GatewayWorker2.0 手册
本手册适用于最新版本GatewayWorker2.0(发布时间2015-11-11)。

GatewayWorker1.0手册参见[http://www.workerman.net/gatewaydoc-1.0/](http://www.workerman.net/gatewaydoc-1.0/)

## 1.0与2.0的差异
参见附录 1.0升级到2.0注意事项 一节

## GatewayWorker 手册
GatewayWorker基于Workerman开发的一个项目框架，用于快速开发TCP长连接应用，例如app推送服务端、即时IM服务端、游戏服务端、物联网、智能家居等等

GatewayWorker使用经典的Gateway和Worker进程模型。Gateway进程负责维持客户端连接，并转发客户端的数据给Worker进程处理；Worker进程负责处理实际的业务逻辑，并将结果推送给对应的客户端。Gateway服务和Worker服务可以分开部署在不同的服务器上，实现分布式集群。

GatewayWorker提供非常方便的API，可以全局广播数据、可以向某个群体广播数据、也可以向某个特定客户端推送数据。配合Workerman的定时器，也可以定时推送数据。

## GatewayWorker 与 Workerman的关系
Workerman可以看做是一个纯粹的socket类库，可以开发几乎所有的网络应用，不管是TCP的还是UDP的，长连接的还是短连接的。Workerman代码精简，功能强大，使用灵活，能够快速开发出各种网络应用。

因为绝大多数开发者的目标是基于Workerman开发TCP长连接应用，而长连接应用服务端有很多共同之处，例如它们有相同的进程模型以及单发、群发、广播等接口需求。所以才有了GatewayWorker框架，GatewayWorker是基于Workerman开发的一个TCP长连接框架，实现了单发、群送、广播等长连接必用的接口，并且内置了MySql类库。GatewayWorker框架实现了Gateway Worker进程模型，天然支持分布式部署，扩容缩容非常方便，能够应对海量并发连接。可以说GatewayWorker是基于Workerman实现的一个更完善的专门用于实现TCP长连接的项目框架。

## GatewayWorker 源码地址

https://github.com/walkor/GatewayWorker

## Applications\YourApp测试方法

##启动
以debug方式启动

```php start.php start```

或者以daemon方式启动

```php start.php start -d```

## 测试
使用telnet命令测试（不要使用windows自带的telnet测试）
```shell
 telnet 127.0.0.1 8282
Trying 127.0.0.1...
Connected to 127.0.0.1.
Escape character is '^]'.
Hello 3
3 login
haha
3 said haha
```

## 使用GatewayWorker开发的项目

## [tadpole](http://kedou.workerman.net/)
[Live demo](http://kedou.workerman.net/)

[Source code](https://github.com/walkor/workerman)

![workerman todpole](http://www.workerman.net/img/workerman-todpole.png)

## [chat room](http://chat.workerman.net/)
[Live demo](http://chat.workerman.net/)

[Source code](https://github.com/walkor/workerman-chat)

![workerman-chat](http://www.workerman.net/img/workerman-chat.png)






