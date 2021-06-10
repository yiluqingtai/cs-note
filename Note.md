## 6月3日

1、**可伸缩性**：[可伸缩性/可扩展性(Scalable/scalability) - 解道Jdon](https://www.jdon.com/scalable.html)

（1）可伸缩性(可扩展性)是一种对软件系统计算处理能力的设计指标，高可伸缩性代表一种弹性，在系统扩展成长过程中，软件能够保证旺盛的生命力，通过很少的改动甚至只是硬件设备的添置，就能实现整个系统处理能力的线性增长，实现高吞吐量和低延迟高性能。

（2）无论采取什么技术，如果应用系统内部是铁板一块，例如严重依赖数据库，系统达到一定访问规模，负载都集中到一两台数据库服务器上，这时进行分区扩展伸缩就比较困难，正如[Hibernate框架](https://www.jdon.com/dl/best/hibernate.htm)创建人Gavin King所说：关系数据库是最不可扩展的。

（3）什么是性能问题？ 如果你的系统对于一个用户访问还很慢，那就是性能问题；什么是扩展性问题？ 如果你的系统对一个用户来说是快的，但是在用户不断增长的高访问量下就慢了。

（4）延迟和吞吐量是衡量可扩展性的一对指标，我们希望获得低延迟和高吞吐量的系统架构。

低延迟：用户能感受到的系统响应时间，比如一个网页在几秒内打开，越短表示延迟越低。

吞吐量：表示同时有多少用户能够享受到这种低延迟，如果并发用户量很大时，用户感觉网页的打开速度很慢，这意味着系统架构的吞吐量有待提高。

扩展性：其目标是用可接受的延迟获得最大的吞吐量。

可靠性(可用性)：用可接受的延迟获得数据更新的一致性。

## 6月4日

1、**边缘计算**：[边缘计算成为下一个爆发点，云计算巨头和CDN巨头谁会赢？_百科TA说 (baidu.com)](https://baike.baidu.com/tashuo/browse/content?id=60005a46c676726713e12e07&lemmaId=9044985&fromLemmaModule=pcBottom)

（1）云计算最大的三重价值是：成本低、扩展性和可靠性，它适合没有实时性要求、有较长周期（从采集到处理到计算到存储再到多次挖掘）的计算需求，而边缘计算本身是分散的云计算，除了有云计算的优势外，还具有低延时、高使用和更安全，更加适合实时性和短周期的计算。

（2）云计算不能满足一些新兴的计算场景，特别是IoT。云计算的做法是，数据被终端采集后传输汇集到集中式云计算中心，通过集群计算后再返回结果，因为有网络延迟，这需要一定的时间，特别是在基于4G网络的移动互联网中。比如实时语音翻译，再比如无人车，对响应时间都有极高要求，依赖云计算并不现实。

（3）边缘计算的核心理念就是将数据的存储、传输、计算和安全交给边缘节点来处理，当然与云计算出现前的终端计算不同，边缘计算并不是说要让终端自己负责所有计算，而是在离终端更近的地方部署边缘平台，终端与之通信可以有多种形式，这样可以避免集中式云计算中心的网络延迟问题。大量实时的需要交互的计算将在边缘节点完成，一些需要集中式处理的计算则继续交由大型云计算中心，如大数据挖掘、大规模学习则要集中式云计算中心才能完成，边缘计算与云计算分工协作，来满足IoT时代爆发式的计算需求。

（4）CDN的核心价值是将数字内容智能分发到离用户更近的节点，进而提升整体分发效率，降低网络延时、节省带宽资源，其与生俱来的边缘节点属性，低延时和低带宽，令其在边缘计算市场具备先发优势，CDN本身就是边缘计算的雏形。CDN玩家凭借着此前在边缘节点和边缘技术上的积累，也成为边缘计算的核心玩家。一方面，CDN玩家利用边缘计算可以进一步降低成本和智能分发，另一方面，CDN玩家在数据分发基础上，开放计算存储安全等一系列服务。

## 6月9日

1、**ZooKeeper**：[可能是把 ZooKeeper 概念讲的最清楚的一篇文章 (juejin.cn)](https://juejin.cn/post/6844903677367418893)

（1）Zookeeper概览

ZooKeeper 是一个开源的分布式协调服务。

ZooKeeper 的设计目标是将那些复杂且容易出错的分布式一致性服务封装起来，构成一个高效可靠的原语集，并以一系列简单易用的接口提供给用户使用。

ZooKeeper 是一个典型的分布式数据一致性解决方案，分布式应用程序可以基于 ZooKeeper 实现诸如数据发布/订阅、负载均衡、命名服务、分布式协调/通知、集群管理、Master 选举、分布式锁和分布式队列等功能。

Zookeeper 一个最常用的使用场景就是用于担任服务生产者和服务消费者的注册中心。 

Zookeeper一般采用集群服务，集群机器数量为奇数台。

ZooKeeper两大作用：集群管理和注册中心。

（2）Zookeeper重要概念

ZooKeeper  本身就是一个分布式程序（只要半数以上节点存活，ZooKeeper  就能正常服务）。

为了保证高可用，最好是以集群形态来部署 ZooKeeper。

ZooKeeper  将数据保存在内存中，这也就保证了高吞吐量和低延迟。

ZooKeeper 是高性能的。 在“读”多于“写”的应用程序中尤其地高性能，因为“写”会导致所有的服务器间同步状态。

ZooKeeper有临时节点的概念。 当创建临时节点的客户端会话一直保持活动，瞬时节点就一直存在。而当会话终结时，瞬时节点被删除。持久节点是指一旦这个ZNode被创建了，除非主动进行ZNode的移除操作，否则这个ZNode将一直保存在Zookeeper上。

ZooKeeper 底层其实只提供了两个功能：①管理（存储、读取）用户程序提交的数据；②为用户程序提交数据节点监听服务。

（3）ZooKeeper集群角色

Leader：负责进行投票的发起和决议，更新系统状态；

Follower：用于接收客户请求并向客户端返回结果，在选举过程中参与投票；

Observer：可以接受客户端连接，将写请求转发给Leader，但Observer不参加投票过程，只同步Leader的状态，Observer的目的是为了扩展系统，提高读取速度。

## 6月10日

1、[什么是TLS DTLS和SRTP？ - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/89028639)

（1）TLS 传输层安全性协议

安全套接层SSL的前身，利用非对称加密演算来对通信方做身份认证，之后交换对称密钥作为会谈密钥（Session key）。这个会谈密钥是用来将通信两方交换的数据做加密，保证两个应用间通信的保密性和可靠性，使客户与服务器应用之间的通信不被攻击者窃听。

（2）DTLS 数据报传输层安全性协议

它基于传输层安全性（TLS）协议，该协议为基于计算机的通信网络提供安全性。 DTSL和TLS之间的主要区别在于DTLS使用UDP，而TLS使用TCP。 它可用于Web浏览，邮件，即时消息传递和VoIP。 DTSL是与SRTP一起用于WebRTC技术的安全协议之一。

（3）SRTP 安全实时传输协议

SRTP是在实时传输协议(Real-time Transport Protocol)基础上所定义的一个协议，旨在为单播和多播应用程序中的实时传输协议的数据提供加密、消息认证、完整性保证和重放保护安全实时传输协议。

2、**ZooKeeper**：[运维部署-Zookeeper (juejin.cn)](https://juejin.cn/post/6844904024144085005#heading-10)

需求环境：jdk

（1）ZooKeeper下载

[Apache Download Mirrors](https://www.apache.org/dyn/closer.lua/zookeeper/zookeeper-3.6.3/apache-zookeeper-3.6.3-bin.tar.gz)

```shell
wget -c  https://mirror-hk.koddos.net/apache/zookeeper/zookeeper-3.6.3/apache-zookeeper-3.6.3-bin.tar.gz #下载
tar -zxv -f apache-zookeeper-3.6.3-bin.tar.gz #解压
```

（2）zookeeper目录

```shell
# zookeeper配置目录
conf
├── configuration.xsl
├── log4j.properties
└── zoo_sample.cfg 

# zookeeper脚本目录
bin
├── README.txt
├── zkCleanup.sh
├── zkCli.cmd
├── zkCli.sh
├── zkEnv.cmd
├── zkEnv.sh
├── zkServer.cmd
├── zkServer-initialize.sh
├── zkServer.sh
├── zkSnapShotToolkit.cmd
├── zkSnapShotToolkit.sh
├── zkTxnLogToolkit.cmd
└── zkTxnLogToolkit.sh
```

脚本功能

| 脚本      | 说明                                                  |
| --------- | ----------------------------------------------------- |
| zkCleanup | 清理Zookeeper历史数据, 包括事务日志文件和快照数据文件 |
| zkEnv     | 设置Zookeeper的环境变量                               |
| zkServer  | Zookeeper服务器的启动、停止、重启脚本                 |
| zkCli     | Zookeeper的命令行客户端                               |

（3）zookeeper单机环境搭建

创建服务器标识文件

```shell
mkdir data
echo 1 > data/myid # 标识当前实例的标识值为1
```

修改zoo.cfg文件并启动（修改dataDir目录和增加服务通讯标识）

```shell
# The number of milliseconds of each tick
tickTime=2000
# The number of ticks that the initial
# synchronization phase can take
initLimit=10
# The number of ticks that can pass between
# sending a request and getting an acknowledgement
syncLimit=5
# the directory where the snapshot is stored.
# do not use /tmp for storage, /tmp here is just
# example sakes.
dataDir=/home/wjy/Library/apache-zookeeper-3.6.3-bin/data
# the port at which the clients will connect
clientPort=2181
# 配置server节点
server.1 = 127.0.0.1:2888:3888
# the maximum number of client co
```

启动zookeeper



## 待学习

1、zookeeper

2、Hadoop

3、HBase

4、Solr

5、redis

[面试前必须要知道的Redis面试题 (qq.com)](https://mp.weixin.qq.com/s?__biz=MzI4Njg5MDA5NA==&mid=2247484609&idx=1&sn=4c053236699fde3c2db1241ab497487b&chksm=ebd745c0dca0ccd682e91938fc30fa947df1385b06d6ae9bb52514967b0736c66684db2f1ac9&token=177635168&lang=zh_CN#rd)

[美团二面：Redis与MySQL双写一致性如何保证？ (qq.com)](https://mp.weixin.qq.com/s?__biz=MzkwMDE1MzkwNQ==&mid=2247499396&idx=1&sn=87fbb610b56969c333b8f352330a30ae&chksm=c04ae9daf73d60cce50aa317229f808fc84566f2e21ef995350020d2b779ec21aa17ab106753&scene=132#wechat_redirect)

6、消息队列

[什么是消息队列？ (juejin.cn)](https://juejin.cn/post/6844903817348136968)

7、零拷贝原理

8、dubbo

9、nginx和keep-alive
10、中间件

[不会还有人不知道中间件吧？ (juejin.cn)](https://juejin.cn/post/6882932453674057735)

11、分布式锁

