## V1、WebRTC架构
### 1.1 整体架构
从下往上理解：

1、OS第三方适配：硬件设备库和第三方库Wrapper层；包括网络、操作系统API的跨平台封装，音频设备、视频设备封装，音频、视频解码器，DTLS第三方库的实现；

2、网络传输层：包括candidate收集，stun/turn协议的实现，dtls、rtp网络的建立，sctp连接的建立；

3、通道层：包括传输通道BaseChannel和媒体通道MediaChannel，传输通道是peerconnection和传输层的桥梁，媒体通道是传输通道和音视频引擎的桥梁

4、RTP_RTCP：流控；

5、Audio Engine和Video Engine：音视频引擎层，音视频处理；

6、音视频编解码器：webrtc自己的抽象，真正的编解码的实现为第三方库；

7、Peerconnection和Mediastream：对jsep协议的实现；

8、PeerconnectionInterface：对外抽象接口类的实现。

### 1.2 目录结构

重点是pc和module目录；

pc目录主要实现PeerConnection；

webrtc的js接口：RTCPeerConnection、RTCDataChannel、getUserMedia、setLocalDescription、setRemoteDescription、createOffer、createAnswer；

webrtc终端通信采用ice协议和sdp协议；

webrtc将逻辑功能独立、内聚性、复用性强的部分单独抽象为模块，放在modules目录下，包括流控、音视频设备，音视频解码器等。

### 1.3 源码分析
#### 1.3.1 编译系统

1、gn简介

gn用来生成ninja，gn和ninja的关系类似于cmake和makefile；

2、gn语法

gn help可以查看详细的语法，主要分为五类：命令、目标声明、构建文件函数、内置预定义变量和目标中设置的变量；

gn的语法很多用到了类似无返回值的C函数；

其中函数名表示目标声明，如executable表示生成可执行文件，group表示一组目标的集合，shared_library表示生成动态库，static_library表示生成静态库；

函数参数表示用户命名的目标的名字；

函数体内一般是类似python列表的变量，进行具体的设置，表示目标中设置的变量。如sources表示源文件，deps表示依赖文件（其中:开头表示依赖当前gn中的目标，//开头表示包含子文件夹中的目标）；列表可以通过+号进行扩展；

gn文件中可以使用类似C语言的条件语句。

3、构建过程

首先寻找.gn文件，该文件为“源根”，其中设置了“构建配置文件”的位置；

执行“构建配置文件”（在“源根”中设置，一般名字为BUILDCONFIG.gn），该文件配置了全局使用的参数和变量；

加载根目录中的BUILD.gn文件，然后递归加载其他目录中的BUILD.gn文件；

目标依赖解析完后，生成.ninja文件；所有目标解析完后，生成build.ninja文件。

**资料**

1、[官网](https://gn.googlesource.com/gn/)

主要介绍了gn的二进制文件的获取和自带的例子的使用，内容较少。

2、[GN Quick Start guide](https://gn.googlesource.com/gn/+/master/docs/quick_start.md#gn-quick-start-guide)

gn概览，包括命令行使用和gn文件的语法，很好的入门材料。

3、[GN Language and Operation](https://chromium.googlesource.com/chromium/src/tools/gn/+/48062805e19b4697c5fbd926dc649c78b6aaa138/docs/language.md#GN-Language-and-Operation)

详细介绍了GN语法；

要了解GN语法和构建过程，看这一篇就够了，介绍得非常详细。

4、[The Ninja build system (Github)](https://github.com/ninja-build/ninja/blob/master/doc/manual.asciidoc)

ninja官方文档。

#### 1.3.2 代码

1、Server

使用了WinSock网络编程规范；

服务端例子并没有使用WebRTC主要模块的API，而客户端例子用到了。

2、Client

## 2、WebRTC协议
### 2.1 NAT

NAT的出现原因：IPv4地址不够用，使用NAT私有地址缓解地址问题方案；

NAT基本思想：IP地址转换，私有地址和公有地址之间的转换；

NAT穿透：两台不同NAT设备后面的主机无法直接建立UDP或TCP连接，需要NAT穿透实现P2P通信；

终端所处NAT网络类型：开放式、完全圆锥型NAT、地址限制型圆锥型NAT、端口限制圆锥型NAT、对称型NAT、对称型UDP防火墙、封闭式；

客户端使用固定公网IP的STUN服务器探测自己所处的网络类型。

当我们检测到一端是端口受限锥型一端是对称型或者两端都是对称型，那肯定是不可以打通的。

**资料**
1、[RFC 3022 - Traditional IP Network Address Translator (Traditional NAT) (ietf.org)](https://tools.ietf.org/html/rfc3022)

RFC文档，最全面的资料。

2、《WebRTC Native开发指南》第20章 NAT穿透

3、[WebRTC网络基础 九、第二节 NAT打洞原理 - 程序员大本营 (pianshen.com)](https://www.pianshen.com/article/30941591646/)

NAT类型介绍以及哪些NAT类型之间可以打通。

### 2.2 STUN
[RFC 8489: Session Traversal Utilities for NAT (STUN) (rfc-editor.org)](https://www.rfc-editor.org/rfc/rfc8489)
### 2.3 TURN
1、[RFC 8656 - Traversal Using Relays around NAT (TURN): Relay Extensions to Session Traversal Utilities for NAT (STUN) (ietf.org)](https://tools.ietf.org/html/rfc8656)

2、[What is WebRTC and How to Setup STUN/TURN Server for WebRTC Communication?](https://medium.com/av-transcode/what-is-webrtc-and-how-to-setup-stun-turn-server-for-webrtc-communication-63314728b9d0)

搭建coturn指南

### 2.4 ICE
1、[RFC 8445 - Interactive Connectivity Establishment (ICE): A Protocol for Network Address Translator (NAT) Traversal (ietf.org)](https://tools.ietf.org/html/rfc8445)

2、[WebRTC samples Trickle ICE](https://webrtc.github.io/samples/src/content/peerconnection/trickle-ice/)

该网页可以收集并显示本机的ICE candidate。

### 2.5 SDP

媒体能力协商：双方都支持哪些编码方式，支持哪些分辨率等；

setLocalDescription和setRemoteDescription分别是保存本地SDP和远程SDP的接口；

SDP通过offer/answer机制进行协商；

SDP一般分为会话行和媒体行，WebRTC分为五个部分：会话基本信息、网络传输信息、媒体数据流信息、数据加密身份认证信息和服务质量传输层复用信息；

会话基本信息：v, o, s, t；

网络传输信息：c, a=candidate；

媒体数据流信息： m, a=rtpmap, a=fmtp, a=sendrecv；

数据加密和身份认证信息：a=crypto, a=ice-frag, a=ice-pwd, a=fingerprint；

服务质量和传输层复用：a=rtcp-fb, a=group, a=rtcpmux；

最重要的媒体数据流信息，包括m行和a行，m行之间的a行描述媒体数据的数据格式、网络传输等信息；

a=candidate描述要使用的ice candidate，a=recvonly描述媒体会话的方向为只接收；

a=rtpmap描述媒体会话支持的格式；

SDP主要用来描述会话、协商媒体信息，为什么要协商？因为会话的各个成员的能力是不对等的；

a=ice-frag和a=ice-pwd的作用：描述ice连接过程中使用的用户名和密码，这两个信息是为了防止ICE连接过程被攻击，例如第三方尝试非法建立ICE连接。WebRTC通过ICE收集的整个网络地址和连通性检测，最终选出一个最有效的路径来，那么选出这个最有效的路径怎么知道这两台机子的会话是合法的呢？那就是通过这个a=ice-frag和a=ice-pwd。通过这个ice-frag和ice-pwd对这个用户进行连通性检测的时候，对这个用户进行判断，也就是如果我通过SDP将这个信息将这个对方的frag和pwd传给你，那当真正建立连接性检测的时候，它就通过这个密码去验证，跟你连通的时候我将这个ice-frag和这个ice-pwd传给你，传给你之后如果你验证通过了，那说明咱们确实是应该建立连接的，那如果你是一个第三方，你想和我进行偷偷的连接，我传给你的用户名和密码，然后你在给我发回来，发出来的用户名和密码与我真正放出去的用户名和密码是不一致的，那说明你是一个非法用户。通过这种方式来保证整个链路的连接是安全的。

a=fingerprint的作用：fingerprint中保存的是sha-256的值，是DTLS协商时使用的证书的sha-256哈希值。指纹就是用来我们进行数据加密的时候，来验证这个证书的。那它首先通过信令层将SDP中的证书的指纹下发给对方，那么下次对数据加密的时候跟之前的它进行一下数据证书的交换，交换证书的时候通过的是DTLS，通过这个指纹去验证你这个证书的有效性，那如果这个证书验证是有效性的，然后后面你才能进行数据加密然后进行传输。如果通过指纹这个证书不匹配，那说明你这个连接也是有问题的。那这个时候就不能进行传输。
a=ice-frag和a=ice-pwd在连通性检测时使用，a=fingerprint在数据传输时使用，两者都是用来验证连接的合法性。

**资料**

1、《WebRTC native 开发实战》的3.4节-SDP初探和第5章-SDP详解；

### 2.6 SIP

## 3、WebRTC信令

信令服务器的作用：交换SDP和ICE Candidate；房间和用户管理；媒体数据连接管理（SFU和MCU情况下）；

信令交互基本流程：发起端和接收端分别与websocket服务器建立连接并注册，发起端依次发送offer消息和candidate消息给接收端，接收端返回answer消息和candidate消息；

ICE server：下发STUN/TURN Server的url、用户名和密码等；

TURN server：供客户端获取公网IP，也能提供媒体数据中转服务；

流程：发起端加入房间->设置本地SDP并上传offer->应答端加入房间->收到offer，设置本地SDP和远程SDP并上传answer->设置远程SDP->两端收集ICE Candidate，通过信令服务器交换->建立p2p的socket，收发音视频数据；

ICE：ICE在SDP中增加传输地址记录值（IP+port+协议），然后对其进行连通性测试，测试通过后就能传输媒体数据了；

ICE Candidate：四种。客户端从本机网络接口上获取的地址；STUN Server看到的该客户端的地址；TURN Server为该客户端分配的中继地址；连通性测试过程中，从对方报文中看到的地址；

STUN：NAT穿透的一套工具，它提供了获取一个内网连接对应的公网连接映射关系的机制；

TURN：STUN协议的一个扩展，TURN服务器为每个peer分配一个中继地址，TURN服务器进行数据转发。

SFU流程：发起端加入房间->设置本地SDP并上传offer到信令服务器（该SDP记录媒体信息）->信令通过rpc将offer发送给流媒体服务器->流媒体服务器收到offer，设置本地SDP和远程SDP并上传answer->客户端设置远程SDP->收集ICE Candidate（客户端发送请求到ICE server，ICE server下发STUN/TURN的url、用户名和密码，客户端发送请求到TURN server，获取候选地址），通过信令服务器交换->通过DTLS进行连通性检测->建立p2p的socket，通过srtp收发音视频数据。

服务器的操作：流媒体服务器根据接入的客户端的ssrc（或者是session id？）新建一个transport，该transport中包含一个代表客户端的producer以及为每个同房间用户生成一个consumer，同房间其他用户也生成新加入客户端的consumer。客户端上传一路流到producer时，将转发该路流到它的所有订阅者（同房间其他客户端在服务器中生成的consumer）。

**资料**

1、《WebRTC native开发指南》

这本书的信令解释集中在交换SDP和ICE Candidate上，对房间管理和媒体数据连接管理基本没有介绍。

2、[WebRTC Signaling Servers: Everything You Need to Know](https://www.wowza.com/blog/webrtc-signaling-servers)

对信令服务器做了简单的介绍，webrtc应用需要四种服务器。

3、[WebRTC Server: What is it exactly?](https://bloggeek.me/webrtc-server/)

四种服务器分别是：信令服务器、流媒体服务器、STUN/TURN服务器、应用服务器；

流媒体服务器是一种表现为webrtc客户端但运行在服务端的服务器。

4、[Do you still need TURN server if your media server has a public IP address?](https://bloggeek.me/turn-public-ip-address/)

如果使用了流媒体服务器，可以不需要STUN服务器，但还必须使用TURN服务器。

5、[WebRTC TURN: Why you NEED it and when you DON’T need it](https://bloggeek.me/webrtc-turn/)

客户端和媒体服务器通信的协议选择：直接UDP->TURN/UDP->TURN/TCP->TURN/TLS；

有些时候防火墙阻止UDP报文，所以需要配置TURN服务器支持TCP连接和TLS连接。

6、《WebRTC权威指南》

这本书的第4章专门介绍信令，但有很多看不懂的地方。（总得来说，这本书不容易读懂，有可能是翻译问题，也有可能是内容比较陈旧）

7、[WebRTC for New Users: Terminology and How It Works](https://www.wowza.com/blog/webrtc-terminology-and-how-it-works)

8、[WebRTC 入门教程（一）| 搭建WebRTC信令服务器](https://rtcdeveloper.com/t/topic/13341)

socket.io库可以实现WebRTC信令服务器，其内置了房间的概念；

9、[WebRTC 入门教程（二）|WebRTC信令控制与STUN/TURN服务器搭建](https://rtcdeveloper.com/t/topic/13742)

会话控制消息：房间的创建和销毁、加入房间、离开房间、开启音频/关闭音频、开启视频/关闭视频、获取房间人数、静音、切换主讲人；

网络信息消息：创建好RTCPeerConnection对象，且调用了setLocalDescription方法后，就开始收集ICE candidate；

ICE候选者分为主机候选者、反射候选者和中继候选者。

## 4、WebRTC流媒体

流媒体服务器，就是用来转发音视频流的服务器。WebRTC主要规范了客户端的标准，缺乏服务端的统一标准，所以服务端可以有多种实现。服务端的主要工作为信令交换和媒体流转发，由于多人通讯一般使用SFU架构，所以必须使用流媒体服务器。

### 4.1 WebRTC流媒体服务器
以下列出的几种服务器都可以作为WebRTC音视频会议的流媒体服务器。

#### 4.1.1 Janus
仓库地址：https://github.com/meetecho/janus-gateway

**要点**

Janus由Janus CORE、Janus Plugin以及信令接口三部分组成；

Janus支持多种信令协议，如websocket，http和RabbitMQ等；

Janus的业务管理是按照插件的方式，如videoroom插件可以实现多人音视频互动；

#### 4.1.2 MediaSoup
仓库地址：https://github.com/versatica/mediasoup/

官方文档：https://mediasoup.org/documentation/

官方Demo：https://github.com/versatica/mediasoup-demo

课程：百万级高并发WebRTC流媒体服务器设计与开发[专门以mediasoup为例子]

**要点**

采用了SFU架构；

nodejs负责信令接收和业务管理

C++负责媒体数据的处理；

底层C++使用libuv处理I/O事件；

demo分析：app, server, C++ mediasoup；

app为客户端代码，server为服务端代码；

server.js为主程序，config.js为配置文件，room.js为房间管理与信令处理；

mediasoup C++部分分析：Worker, Router, Transport；

Worker代表一个运行在单核CPU上并处理Router实例的mediasoup C++子进程；

Router用于注入、选择和转发通过Transport实例创建的媒体流；

Transport将终端与MediaSoup Router连接起来，并通过在其上创建的Producer和Consumer实例实现双向媒体传输；

每个Worker里有多个Router；

每个Worker里都有一个Channel(管道) 通过其与C++进行通讯；

每个用户的Transport可能会有多个Producer或者 Consumer；

mediasoup js起到管理作用，是上层应用与C++层的一个桥梁，生成json字符串传给C++；

C++部分负责流的流转，数据的流转，带宽的评估，丢包通知重传等工作；

nodejs部分和C++部分通过管道进行通信；

管道处理都交给了Channel类处理；

mediasoup使用了protoo实现websocket，protoo是一个面向实时通信应用的最小可扩展node.js信令框架。

**mediasoup流程**

客户端发起websocket请求，并携带房间号；

根据房间号查找房间，如果房间不存在，轮询挑选一个worker，产生一个router，通过router产生一个DirectTransport；

客户端执行加入房间的命令join；

客户端为每个同房间的用户产生一个Consumer，自己产生一个Producer；

新用户加入到房间后为当前房间已经存在的每个Producer各产生一个Consumer，将此Consumer的信息通过newConsumer指令发送给客户端，建立客户端和服务端的consumer的通道；

新用户每创建一个Producer也会为当前房间已经存在的用户创键一个对应的Consumer，并发送到已存在用户的客户端上；

用户的音视频数据通过Producer分发到同房间的Consumer上。

**资料**
1、[mediasoup-demo 实践](https://blog.csdn.net/aggresss/article/details/104858479)

mediasoup demo 搭建记录。

2、[Mediasoup 杂谈](https://www.liangzl.com/get-article-detail-223550.html)

分析了源码结构。

3、[【流媒体服务器Mediasoup】多人音视频架构、流媒体的比较、mediasoup介绍 (一)](https://blog.csdn.net/gjy_it/article/details/104414037?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522161424846216780271597490%2522%252C%2522scm%2522%253A%252220140713.130102334.pc%255Fblog.%2522%257D&request_id=161424846216780271597490&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~blog~first_rank_v2~rank_v29-2-104414037.pc_v2_rank_blog_default&utm_term=mediasoup)

mediasoup课程的总结笔记，系列文章，值得一看。

4、[Mediasoup库的架构（C++部分）](https://www.pianshen.com/article/97851523061/)

5、[mediasoup架构分析](https://www.pianshen.com/article/59951724122/)

#### 4.1.3 Medooze

仓库地址：https://github.com/medooze/media-server

#### 4.1.4 Licode

仓库地址：https://github.com/lynckia/licode

#### 4.1.5 Jitsi

### 4.2 其他流媒体服务器

以下服务器一般在直播中使用

#### 4.2.1 SRS

#### 4.2.2 EasyDarwin

### 4.3 多人视频通讯架构

#### 4.3.1 mesh

端对端通讯；

弊端：链接过多，占带宽。

#### 4.3.2 MCU

MultiPoint Control Unit；

服务器中继并进行音视频混合；

优点：带宽降低，每端收发一路；

弊端：CPU负载较高；客户端难以调整参数。

#### 4.3.3 SFU

Selective Forwarding Unit；

纯粹的数据转发；

一路发，多路收；

弊端：接收端占带宽高。

### 4.4 参考文献
1、 [多人实时互动之各WebRTC流媒体服务器比较 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/91040064)

这篇文章主要分析对比了Mediasoup、Janus和Medooze三种流媒体服务器，配上的插图很好地描述了三者的架构。

2、[webrtc笔记(3): 多人视频通讯常用架构Mesh/MCU/SFU](https://www.cnblogs.com/yjmyzz/p/webrtc-multiparty-call-architecture.html)

简要介绍了Mesh、MCU和SFU三种架构的异同以及应用场景。

3、[史上最全的WebRTC服务器技术选型分析 - 死磕音视频的个人空间 - OSCHINA - 中文开源技术交流社区](https://my.oschina.net/u/3937935/blog/4331261)

和第一篇文章的内容差不多，但介绍的开源流媒体服务器种类更多，分析也更全面。

4、[【流媒体服务器Mediasoup】多人音视频架构、流媒体的比较、mediasoup介绍 (一)](https://blog.csdn.net/gjy_it/article/details/104414037?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522161424846216780271597490%2522%252C%2522scm%2522%253A%252220140713.130102334.pc%255Fblog.%2522%257D&request_id=161424846216780271597490&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~blog~first_rank_v2~rank_v29-2-104414037.pc_v2_rank_blog_default&utm_term=mediasoup)

对音视频架构和流媒体服务器开源软件做了分析比较。

5、[是支持计划添加WEBRTC到RTMP服务器 · Issue #357 · xia-chu/ZLMediaKit (github.com)](https://github.com/xia-chu/ZLMediaKit/issues/357)

6、[coturn/coturn: coturn TURN server project (github.com)](https://github.com/coturn/coturn)

turn/stun 服务器例子，可以参考学习。

## 5、WebRTC APIs 官方示例

**参考**

[WebRTC samples](https://webrtc.github.io/samples/)

### 5.1 getUserMedia

1、基本的getUserMedia样例

使用getUserMedia() API在一个视频元素中显示视频流；

效果：点击Open camera按钮后显示摄像头抓取的视频。

```html
<!--html核心代码：视频窗口和按钮-->
<video id="gum-local" autoplay playsinline></video>
<button id="showVideo">Open camera</button>
```

```javascript
// 1、添加按钮点击事件
document.querySelector("#showVideo").addEventListener('click', e => init(e));
// 2、音频和视频选择
const constraints = window.constraints = {
	audio: false;
    video: true;
};
// 3、获取流并处理
async function init(e) {
    try {
		const stream = await navigator.mediaDevices.getUserMedia(constraints);   
        handleSuccess(stream);
        e.target.disabled = true;
    } catch(e) {
        handleError(e);
    }
}
// 4、处理并显示视频流
function handleSuccess(stream) {
    const video = document.querySelector('video');
    window.stream = stream;
    video.srcObject = stream;
}
```

## 6、WebRTC源码

### 6.1 p2p

主要是实现 candidate 收集，NAT 穿越。

#### 6.1.1 turn_server

1、TurnServer类：turn服务器打开两个端口，一个对内部客户端，一个对外部转发；AddInternalServerSocket监听内部连接请求，AddInternalSocket监听内部客户端发送的包，setExternalSocketFactory使用工厂方式创建对外转发端口；

**参考**

1、[WebRTC TURN协议初识及turnserver实践 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/71025431)

turn server的原理详细解释。

2、[(1条消息) WebRTC源码中turnserver的使用方法_安晓辉生涯——聚焦程序员的职业规划与成长-CSDN博客](https://blog.csdn.net/foruok/article/details/60769621)

webrtc的turn server实例的使用方法。

3、[TURN服务器  | WebRTC](https://webrtc.org/getting-started/turn-server)

一份官方说明。搭建好turn服务器后，在浏览器代码中配置iceConfiguration，设置turn服务器的url，用户名和密码，就可以根据此配置来建立RTCPeerConnection。

4、[How to set up and configure your own TURN server using Coturn (gabrieltanner.org)](https://gabrieltanner.org/blog/turn-server)

如何使用coturn搭建turn服务器并检测。

5、[node.js - How do I configure WebRTC to connect to my TURN server? - Stack Overflow](https://stackoverflow.com/questions/61822108/how-do-i-configure-webrtc-to-connect-to-my-turn-server)

一个有趣的问题，提问者配置了iceConfiguration，但是忘记了在建立RTCPeerConnection里加入这个配置了。

## 7、WebRTC相关问题及解答

1、TURN协议的工作原理以及阶段

分配：客户端需要在中继服务器上申请中继地址和端口；

转发：STUN服务器将UDP数据封装为STUN数据；

信道：建立信道后传输，减少包头长度。

2、ICE的概念

交互式连接建立，是整合了TURN和STUN协议的框架。

3、ICE服务器提供什么功能？

下发stun和turn服务器的地址；

ICE的用户名和证书。

4、收集ICE候选者的时机

WebRTC创建RTCPeerConnection对象后，调用setLocalDescription方法，收集ICE候选者。

5、ICE候选者的类型

本地候选者、反射候选者和中继候选者。

6、如何搭建turn服务器以及检测其是否正常工作

coturn开源项目以及trickle-ice网页。

7、为什么使用了流媒体服务器还需要turn和stun服务器？

WebRTC通过UDP发送数据，有时候客户端防火墙阻止UDP报文，所以需要配置TURN服务器支持TCP连接和TLS连接。

8、介绍SDP的各个部分

会话层：整个会话的基本信息 vost

网络传输层：网络传输的信息 a=candidate

媒体层：媒体数据流的信息 m= a=rtpmap a=sendrecv

安全层：数据加密和身份认证的信息 a=ice-frag

QoS层：服务质量和传输层复用的信息 a=rtcp-fb

9、介绍几个常见SDP行

m行：媒体行，m行之间都是描述媒体信息的

a=candidate：描述ICE Candidate

a=recvonly：描述媒体流的方向

a=rtpmap：描述媒体流支持的格式

a=ice-frag, a=ice-pwd：描述ICE连接过程中使用的用户名和密码，防止ICE连接过程被攻击

## 8、WebRTC参考资料
### 8.1 博客资料

1、[[WebRTC架构分析]源码目录结构介绍](https://zhuanlan.zhihu.com/p/81361664)

webrtc源码目录结构的介绍。

2、[互动直播之WebRTC服务开源技术选型](https://juejin.cn/post/6844904167341817869)

3、[WebRTC 入门教程（二）|WebRTC信令控制与STUN/TURN服务器搭建](https://juejin.cn/post/6844903844904697864)

4、[WebRTC TURN协议初识及turnserver实践](https://juejin.cn/post/6844903875598614536)

5、[WebRTC源码研究（3）webrtc运行机制](https://juejin.cn/post/6850418115856039949)

6、[WebRTC入门与提高-WebRTC原理(STUN/TURN/SDP)](https://zhuanlan.zhihu.com/p/79489847)

零声学院的那幅图对理解webrtc p2p的流程有帮助；

另外还包含了webrtc的架构图。

7、[WebRTC 之ICE浅谈 | 内有干货免费下载](https://zhuanlan.zhihu.com/p/60684464)

对ICE的介绍比较深入。

8、[WebRTC SDP 详解和剖析](https://juejin.cn/post/6898652794899660807)

可能是最全面的SDP分析。

9、[WebRTC信令服务器实现 八、第二节 WebRTC信令服务器原理 - 程序员大本营 (pianshen.com)](https://www.pianshen.com/article/58311584594/)

介绍了信令服务器的作用，SDP的内容以及socket.io。

10、[WebRTC网络基础 九、第二节 NAT打洞原理 - 程序员大本营 (pianshen.com)](https://www.pianshen.com/article/30941591646/)

介绍了NAT类型，哪些NAT类型之间可以打通。

11、[Webrtc服务器架构 - 程序员大本营 (pianshen.com)](https://www.pianshen.com/article/9533714907/)

mesh、SFU和MCU三种服务器架构的介绍。

12、[二、第二节 WebRTC源码目录结构 - 程序员大本营 (pianshen.com)](https://www.pianshen.com/article/89141400459/)

13、[WebRTC for New Users: Terminology and How It Works](https://www.wowza.com/blog/webrtc-terminology-and-how-it-works)

该文对WebRTC的工作过程做了总结性的介绍，很有参考价值。。

14、[WebRTC源码研究（1）WebRTC架构](https://juejin.cn/post/6844904199684096007)

### 8.2 WebRTC源码

WebRTC核心代码30多M，但包含的第三方库10G左右；需要重点研读的是WebRTC核心代码；

Examples文件夹包含了浏览器和各个客户端平台的Demo，可以从其中熟悉WebRTC的API的使用；

Modules文件夹中的内容最多也最重要；

Api文件夹中封装了很多供浏览器Js使用的API，也是一个学习的起点；

其他的文件夹在学习examples和api的途中再分别研读；

### 8.3 书籍

1、 WebRTC native 开发实战

前两章介绍webrtc的安装和部署，有帮助，但限于网络环境，在实践仍然有层层困难，至今没有将完整的webrtc代码下载下来（声网的镜像修复好后，可以从声网拉代码下来）。

后面章节大部分篇幅是比较硬核的源码导读，其中剖析客户端的代码比较多，如果不结合源码看这些章节基本看不懂，深入挖掘也费时费力，所以目前应该将后面章节快速过一遍，建立一个整体的框架和概念即可。

这本书简略得过了一遍，源码分析太多，没法深入看。代码这东西只有自己亲自调试才能看懂，这本书只能在自己阅读代码时辅助使用，里面介绍的概念可以着重熟悉一下。

2、WebRTC音视频开发：React+Flutter+Go

这本书从目录来看内容很不错，有助于了解webrtc的API，但是其web端使用React，移动端使用Flutter，后台使用Go，这些都是我不熟悉的技术，所以目前还无法看下去。

### 8.4 视频课程

1、李超课程《WebRTC入门》

重点剖析WebRTC的使用，特别是浏览器端的使用；对熟悉WebRTC原理和API调用有帮助。

2、李超课程《百万级高并发WebRTC流媒体服务器设计与开发》

专注于流媒体服务器的分析，特别是异步处理IO和mediasoup分析，可以好好看看。

流媒体服务器的种类很多，首先根据这个课程和一些文章了解流媒体服务器的异同，再重点学习mediasoup，包括其部署和源码。

### 8.5 WebRTC官方文档

1、[external/webrtc - Git at Google (googlesource.com)](https://chromium.googlesource.com/external/webrtc)

webrtc本地代码的官方仓库，C++底层库，用来开发native应用

2、[WebRTC 1.0: Real-Time Communication Between Browsers (w3c.github.io)](https://w3c.github.io/webrtc-pc/)

webrtc javascript api，用来开发web应用

3、[WebRTC development (googlesource.com)](https://webrtc.googlesource.com/src/+/refs/heads/master/docs/native-code/development/index.md#example-applications)

webrtc开发指南

4、[WebRTC samples](https://webrtc.github.io/samples/)

WebRTC的JS API使用示例