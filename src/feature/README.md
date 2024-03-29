# GatewayWorker特性

### 1、基于Workerman开发
GatewayWorker是基于Workerman开发的

### 2、基于Gateway、Worker进程模型
GatewayWorker使用经典的Gateway和Worker进程模型。Gateway进程负责维持客户端连接，并转发客户端的数据给Worker进程处理；Worker进程负责处理实际的业务逻辑，并将结果推送给对应的客户端。Gateway服务和Worker服务可以分开部署在不同的服务器上，实现分布式集群。

### 3、支持分布式部署
GatewayWorker可以非常方便实现分布式部署，Gateway服务和Worker服务都可以分开部署在不同的服务器集群上。并且操作简单、容易扩容、上下线用户无感知。

### 4、支持高并发
Gateway进程只负责网络IO，Worker进程负责业务逻辑。其中每个Gateway进程可以维持上万的并发连接，多个Gateway进程可以维持数十万甚至百万的并发连接，Gateway集群则可以维持千万级别的并发连接。

### 5、支持全局广播或者向任意客户端推送数据
GatewayWorker提供非常方便的API，可以全局广播数据、可以向某个群体广播数据、也可以向某个特定客户端推送数据。配合Workerman的定时器，也可以定时推送数据。

### 6、支持各种应用层协议
WorkerMan接口上支持各种应用层协议，包括自定义协议。同样GatewayWorker也支持各种应用层协议。

### 7、多协议支持
有时应用客户端所使用的协议不止一种，例如PC网页客户端使用的是WebSocket协议，而手机App使用的是其它协议。GatewayWorker可以非常方便的支持多协议，只需要以不同的协议开不同的端口即可，业务代码无需改动。

### 8、支持对象或者资源永久保持
WorkerMan在运行过程中只会载入解析一次PHP文件，然后便常驻内存，这使得类及函数声明、PHP执行环境、符号表等不会重复创建销毁，这与Web容器下运行的PHP机制是完全不同的。在WorkerMan中，一个进程生命周期内静态成员或者全局变量在不主动销毁的情况下是永久保持的，也就是将对象或者链接等资源放到全局变量或者类静态成员中则整个进程生命周期内的所有请求都可以复用。例如只要单个进程内初始化一次数据库连接，则以后这个进程的所有请求都可以复用这个数据库连接，避免了频繁连接数据库过程中TCP三次握手、 数据库权限验证、断开连接时TCP四次握手的过程，极大的提高了应用程序效率。

### 9、高性能
由于php文件从磁盘读取解析一次后便会常驻内存，下次使用时直接使用内存中的opcode， 极大的减少了磁盘IO及PHP中请求初始化、创建执行环境、词法解析、语法解析、编译opcode、请求关闭等诸多耗时过程， 并且不依赖nginx、apache等容器，少了nginx等容器与PHP通信的开销，最主要的是资源可以永久保持，不必每次初始化数据库连接等等， 所以使用WorkerMan开发应用程序，性能非常高。

### 10、支持HHVM
支持在HHVM虚拟机上运行，可成倍提升PHP性能。尤其是在cpu密集运算业务中，性能非常优异，是PHP Zend虚拟机8倍左右。通过实际压力测试对比，在没有负载业务的情况下，WorkerMan在HHVM下运行比在Zend PHP5.6运行网络吞吐量提高了30-80%左右

### 11、方便与其它项目集成
针对其它项目，GatewayWorker提供推送非常简单方便的API，可以在任何项目中使用这个API向所有客户端或者特定客户端推送数据，比如在普通Web项目中推送数据。

### 12、支持代码热更新
可以reload Worker进程实现业务代码更新升级，而不必担心客户端连接会断开，因为客户端连接都由Gateway进程维持。

### 13、支持长连接
GatewayWorker主要用于长连接即时通讯应用。如游戏服务器、物联网无服务、IM、移动应用等。



