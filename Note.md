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

```shell
./zkServer.sh start &  #启动
./zkServer.sh status #查看状态
```



## 6月16日

1、**基础：**[函数调用过程中栈到底是怎么压入和弹出的？ - 一八七四的回答 - 知乎](https://www.zhihu.com/question/22444939/answer/22200552) 

（1）一个函数调用另一个函数，会压入原来ebp的值, 参数, 以及调用函数的下一个指令地址。

（2）在调用一个函数时, 编译器就计算好函数需要的空间, 然后esp = ebp-需要的空间, 通过ebp+偏移量来访问. 在函数里调用另外一个函数时, 原来fun的ebp值压栈。

（3）ESP：栈指针寄存器(extended stack pointer)，其内存放着一个指针，该指针永远指向系统栈最上面一个栈帧的栈顶。

（4）EBP：基址指针寄存器(extended base pointer)，其内存放着一个指针，该指针永远指向系统栈最上面一个栈帧的底部。

（5）函数栈帧：ESP和EBP之间的内存空间为当前栈帧，EBP标识了当前栈帧的底部，ESP标识了当前栈帧的顶部。

（6）EIP：指令寄存器(extended instruction pointer)， 其内存放着一个指针，该指针永远指向下一条待执行的指令地址（返回地址）。

（7）函数调用步骤

压入前栈帧的EBP；

栈帧调整：ESP值装入EBP，更新栈帧底部，然后将ESP减去所需空间大小，抬高栈顶；

压入调用函数的局部变量；

压入调用函数的参数（从右往左顺序压入）；

压入返回地址（调用函数后下一条待执行的指令地址）；

代码区跳转：处理器从当前代码区跳转到被调用函数的入口处；

2、**ffmpeg：**[ffmpeg开发播放器学习笔记 - Hello FFmpeg (juejin.cn)](https://juejin.cn/post/6917170943676645390#heading-9)

ffmpeg初始化流程

（1）打开文件/数据流：AVFormatContext,保存了音视频文件信息

```
int ret = avformat_open_input(&formatContext, url, NULL, NULL);
```

（2）找到音、视频流信息：AVFormatContext，读取少量的数据包方便找到精确的音视频流信息,这些包会被缓存起来,解码的时候不会重复读取。

```
ret = avformat_find_stream_info(formatContext, NULL);
```

（3）遍历流信息：从已经读取到的流信息中遍历查找到音频与视频的流信息

（4）初始化音视频解码器：从AVStream中可以读取到解码器的参数信息,这个结构体里包括了视频的宽高、FPS、视频长度等信息；如果是音频它包括了采样率、声道、音频数据包、音频格式、解码器等信息。

```c
AVCodecParameters *codecParameters = stream->codecpar; // AVCodec定义了解码器的功能,首先找到解码对应流信息的解码器
AVCodecContext *codecContext = avcodec_alloc_context3(codec); // 找到解码器之后,需要实例化一个解码器上下文
```

AVCodec定义了功能,AVCodecContext结构表示程序运行的当前 AVCodec 使用的上下文，着重于所有 AVCodec 共有的属性(并且是在程序运行时才能确定其值)和关联其他结构的字段。AVCodecContext可以看作是AVCodec的一个具体实体表现，后续的解码操作都使用AVCodecContext。AVCodecContext不仅包含了AVCodec定义的功能,还需要通过特定的参数来完成功能的调用，这些参数存储在AVCodecParameters中。

```c
avcodec_parameters_to_context(codecContext, codecParameters); // 初始化完成之后还需要将流信息参数填充到AVCodecContext。
avcodec_open2(codecContext, codec, NULL); // AVCodecContext默认是关闭的,在解码使用前需要先打开
```

3、**ffmpeg：**[给初学者的 20 多个 FFmpeg 命令示例 (juejin.cn)](https://juejin.cn/post/6844903859236651022#heading-8)

FFmpeg典型语法：

```c
ffmpeg [全局选项] {[输入文件选项] -i 输入_url_地址} ...
 {[输出文件选项] 输出_url_地址} ...
```

（1）获取音频/视频文件信息

```
ffmpeg -i video.mp4
```

（2）转换视频文件到不同的格式

```
ffmpeg -i video.mp4 video.avi
```

（3）转换视频文件到音频文件

```c
ffmpeg -i input.mp4 -vn output.mp3  //-vn – 表明我们已经在输出文件中禁用视频录制。
```

（4）更改视频文件的分辨率

```
ffmpeg -i input.mp4 -s 1280x720 -c:a copy output.mp4
```

（5）压缩视频文件

```
ffmpeg -i input.mp4 -vf scale=1280:-1 -c:v libx264 -preset veryslow -crf 24 output.mp4
```

-c 后面需要跟 :v或者:a 用于说明是音频编码还是视频编码

（6）ffmpeg命令行很多，不需要全部记住，记住语法特点和几个常用的即可

4、**ffmpeg：**[FFmpeg 视频处理入门教程 - 阮一峰的网络日志 (ruanyifeng.com)](http://www.ruanyifeng.com/blog/2020/01/ffmpeg.html)

常用命令行参数

（1）-c：指定编码器

（2）-c copy：直接复制，不经过重新编码（这样比较快）

（3）-c:v：指定视频编码器

（4）-c:a：指定音频编码器

（5）-i：指定输入文件

（6）-an：去除音频流

（7）-vn： 去除视频流

（8）-preset：指定输出的视频质量，会影响文件的生成速度，有以下几个可用的值 ultrafast, superfast, veryfast, faster, fast, medium, slow, slower, veryslow。

（9）-y：不经过确认，输出时直接覆盖同名文件。

## 6月21日

1、**HTTP：**[Http协议报文格式 - 星朝 - 博客园 (cnblogs.com)](https://www.cnblogs.com/jpfss/p/10984966.html)

（1）总结了HTTP的请求方式

（2）总结HTTP请求头和响应头信息

（3）总结了响应码

2、**cookie：**[什么是cookie,token和session?它们之间有什么关系？ - 心谭的回答 - 知乎](https://www.zhihu.com/question/353373715/answer/974583248)

（1）HTTP 协议是无状态的。但是随着 web 应用的发展，越来越多的场景需要标识用户身份。例如：单点登陆、购物车等等。而 cookie、session 与 token，就是为了实现带有状态的“会话控制”。

（2）Cookie

cookie 是以 K-V 形式，存储在浏览器中一种数据。它可以在服务端设置，也可以在浏览器端用 js 代码设置。

它拥有 maxAge、domain、path 等属性，借助这些属性，可以实现父子域名之间的数据传递。

浏览器端：通过 js 代码来设置，例如 `document.cookie = "firstName=dongyuanxin; path=/`

服务器端：通过给 Http Response Headers 中的`Set-Cookie`字段赋值，来设置 cookie。客户端接收到`Set-Cookie`字段后，将其存储在浏览器中。

整体流程（购买商品）：监测到浏览器客户端没有标识用户的 cookie，跳转到登陆界面；用户账号密码登陆，后端验证，成功后，在Set-cookie中设置标识用户的 cookie；登陆成功，保存用户标识的 cookie；购买商品，自动携带用户身份的 cookie，后端验证无误后，购买成功；（服务端不保存cookie，cookie中已经保存了用户信息了，比如用户名密码）

（3）Session

Session 机制准确来说，也是通过 K-V 数据格式来保存状态。其中：Key：也称 SessionID，保存在客户端浏览器。Value：也称“Session”，保存在服务端（服务端保存了SessionID以及Session）。

客户端只需要存储 SessionID。具体映射的数据结构放在了服务端，因此跳出了仅仅浏览器 cookie 只可以存储 string 类型的限制。

客户端存储 SessionID，还是需要借助 cookie 来实现。

客户端发送请求携带SessionID，后端检验后返回Session中信息。

session 传输数据少，数据结构灵活：相较于 cookie 来说，session 存储在服务端，客户端仅保留换取 session 的用户凭证。因此传输数据量小，速度快。

session 更安全：检验、生成、验证都是在服务端按照指定规则完成，而 cookie 可能被客户端通过 js 代码篡改。

session 的不足：服务器是有状态的。多台后端服务器无法共享 session。解决方法是，专门准备一台 session 服务器，关于 session 的所有操作都交给它来调用。而服务器之间的调用，可以走内网 ip，走 RPC 调用（不走 http）。

（4）Token

对于 session 来说，服务器是有状态的。这个事情就很麻烦，尤其是在分布式部署服务的时候，需要共享服务器之间的状态。总不能让用户不停重复登陆吧？虽然专门准备一个服务器用来处理状态是可行的，但是能不能让服务器变成无状态的，还不能像单纯 cookie 那么蹩脚？

整体流程：用户尝试登陆；登陆成功后，后端依靠加密算法，将凭证生成 token，返回给客户端；客户端保存 token，每次发送请求时，携带 token；后端再接收到带有 token 的请求时，验证 token 的有效性；

生成：token 的组成为：${user}.${HS256(user, secret)}。其中，secret 是加密需要的密钥，保存在服务端，不能泄漏。HS256 是加密算法，使用 RS256、HS512 也可以。

验证：将请求中携带的 token 按照.分开，得到payload和sig。用服务器密钥对payload进行加密，将加密结果和sig比较，如果相同，那么通过验证。

服务器变成无状态了，实现分布式 web 应用授权。

安全性更高，密钥保存在服务器。若密钥被窃取，可以统一重新下发密钥。

## 6月23日

1、**Java：**[新手ubuntu安装Java环境 (juejin.cn)](https://juejin.cn/post/6844904121439354894)

（1）下载JDK

JDK网址：[Java SE - Downloads | Oracle Technology Network | Oracle Hong Kong SAR, PRC](https://www.oracle.com/hk/java/technologies/javase-downloads.html)

linux下载对应版本压缩包

（2）Linux中创建java目录

在/usr/目录下创建java目录

（3）解压Java安装包

将jdk文件移动到/usr/java

解压jdk文件

（4）配置环境

使用vim打开profile文件/etc/profile

在文件添加如下内容并保存

```shell
set java environment
JAVA_HOME=/usr/java/jdk1.8.0_241        
JRE_HOME=/usr/java/jdk1.8.0_241/jre     
CLASS_PATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar:$JRE_HOME/lib
PATH=$PATH:$JAVA_HOME/bin:$JRE_HOME/bin
export JAVA_HOME JRE_HOME CLASS_PATH PATH
```

让修改生效

```shell
source /etc/profile
```

（5）测试是否成功

```shell
java -version
```

## 6月28日

1、**Javascipt：**[require 和 import 详解 (juejin.cn)](https://juejin.cn/post/6844903735554998280)

（1）require

在CommonJS中，有一个全局性方法require()，用于加载模块。

模块写法分exports和module.exports。

（2）import

## 6月29日

1、**Docker：**[非root用户加入docker用户组省去sudo (juejin.cn)](https://juejin.cn/post/6974592882908872735)

（1）查看是否有docker组

```shell
sudo cat /etc/group | grep docker
```

（2）添加docker分组并将当前用户加入该用户组中

```shell
sudo groupadd docker
sudo usermod -aG docker $USER
```

（3）重启Docker并重新登录

## 7月1日

1、[MySQL 安装 | 菜鸟教程 (runoob.com)](https://www.runoob.com/mysql/mysql-install.html)

（1）apt或者rpm安装mysql

```shell
apt install mysql-server
```

（2）权限设置

```shell
chown mysql:mysql -R /var/lib/mysql
```

（3）初始化MySQL

```shell
mysqld --initialize
```

（4）启动MySQL

```shell
systemctl start mysqld
```

（5）查看MySQL运行状态

```shell
systemctl status mysqld
```

（6）验证MySQL安装

```shell
mysqladmin --version
```

（7）设置root用户密码

```shell
mysqladmin -u root password "new_password"
```

（8）连接到mysql服务器

```shell
mysql -u root -p
```

## 7月7日

1、[鸟哥的 Linux 私房菜 -- Linux 账号管理 (vbird.org)](http://cn.linux.vbird.org/linux_basic/0410accountmanager_5.php)

（1）PAM的目的：使某个用户可以使用系统资源，但不能登录linux主机。

（2）让只使用资源不登录的用户使用/sbin/nologin作为他们的shell。

如果我想要让某个具有 /sbin/nologin 的使用者知道，他们不能登陆主机时， 其实我可以创建『 /etc/nologin.txt 』这个文件， 并且在这个文件内说明不能登陆的原因，那么下次当这个用户想要登陆系统时， 屏幕上出现的就会是 /etc/nologin.txt 这个文件的内容，而不是默认的内容了！

（3）PAM 可以说是一套应用程序编程接口 (Application Programming Interface, API)，他提供了一连串的验证机制，只要使用者将验证阶段的需求告知 PAM 后， PAM 就能够回报使用者验证的结果 (成功或失败)。



## 待学习

**工具使用**

1、zookeeper

2、Hadoop

3、HBase

4、Solr

5、redis

[面试前必须要知道的Redis面试题 (qq.com)](https://mp.weixin.qq.com/s?__biz=MzI4Njg5MDA5NA==&mid=2247484609&idx=1&sn=4c053236699fde3c2db1241ab497487b&chksm=ebd745c0dca0ccd682e91938fc30fa947df1385b06d6ae9bb52514967b0736c66684db2f1ac9&token=177635168&lang=zh_CN#rd)

[美团二面：Redis与MySQL双写一致性如何保证？ (qq.com)](https://mp.weixin.qq.com/s?__biz=MzkwMDE1MzkwNQ==&mid=2247499396&idx=1&sn=87fbb610b56969c333b8f352330a30ae&chksm=c04ae9daf73d60cce50aa317229f808fc84566f2e21ef995350020d2b779ec21aa17ab106753&scene=132#wechat_redirect)

6、dubbo

7、nginx和keep-alive

8、gdb

9、ffmpeg

将ffmpeg一百行播放器的内容看熟

[leandromoreira/ffmpeg-libav-tutorial: FFmpeg libav tutorial - learn how media works from basic to transmuxing, transcoding and more (github.com)](https://github.com/leandromoreira/ffmpeg-libav-tutorial#chapter-3---transcoding)

[FFmpeg Encoding and Editing Course (slhck.info)](http://slhck.info/ffmpeg-encoding-course/#/)

[Lei Xiaohua's learning resource about video/audio technics (leixiaohua1020.github.io)](http://leixiaohua1020.github.io/#ffmpeg-development-examples)

[从零开始仿写一个抖音App——基于FFmpeg的极简视频播放器 (juejin.cn)](https://juejin.cn/post/6844903734238003208#heading-7)

10、websocket

如何使用websocket实现聊天功能

**原理**

1、消息队列

[什么是消息队列？ (juejin.cn)](https://juejin.cn/post/6844903817348136968)

2、零拷贝原理

3、中间件

[不会还有人不知道中间件吧？ (juejin.cn)](https://juejin.cn/post/6882932453674057735)

4、分布式锁

5、函数调用

[介绍 · 函数调用原理 (coder.cat)](https://gitbook.coder.cat/function-call-principle/)

6、fopen和open区别

7、awk和grep的使用、格式化输出

8、单点登录

[session多端登陆，共享怎么做的啊？ - SegmentFault 思否](https://segmentfault.com/q/1010000005788476)

9、虚拟内存的寻址空间

10、AB测试

## 总结类文章

### Javascript

1、[14万字 | 400 多道 JavaScript 面试题 🎓 有答案 🌠(第一部分 1-100题) (juejin.cn)](https://juejin.cn/post/6978348663286267912#no50)