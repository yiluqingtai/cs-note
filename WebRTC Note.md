## 5月28日

1、[webRTC的标准与发展 (juejin.cn)](https://juejin.cn/post/6967159163633795103)

（1）浏览器将音视频处理和传输的复杂性的大部分从三个主要API中抽象出来：

`MediaStream`：获取音频和视频流

`RTCPeerConnection`：音频和视频数据的通信

`RTCDataChannel`：任意应用程序数据的通信

（2）WebRTC通过UDP传输其数据。但是，UDP只是一个起点。要使浏览器中的实时通信成为现实，它需要花费比原始UDP多得多的费用。

（3）WebRTC体系结构由十几种不同的标准组成，涵盖了应用程序和浏览器API，以及使其工作所需的许多不同的协议和数据格式：

Web实时通信（WEBRTC）W3C工作组负责定义浏览器API。

Web浏览器中的实时通信（RTCWEB）是IETF工作组，负责定义协议，数据格式，安全性和所有其他必要方面，以实现浏览器中的对等通信。

（4）实现低延迟，对等传输是一项不平凡的工程挑战：NAT遍历和连接性检查，信令，安全性，拥塞控制以及无数其他细节需要处理。

2、[硬货专栏 ｜深入浅出 WebRTC AEC（声学回声消除） (qq.com)](https://mp.weixin.qq.com/s/iq6EWCQHoYTtAwZBzs8tYA)

（1）音频方面熟知的 3A 算法（AGC: Automatic gain control; ANS: Adaptive noise suppression; AEC: Acoustic echo cancellation）。

（2）文章结构：回声的形成，回声消除的本质，信号处理流程，线性滤波，非线性滤波，延时调整策略，总结与优化方向。

（3）回声如何形成和回声消除的本质的讲得比较详细，配合图观看。

（4）后面滤波部分较复杂，还没来得及仔细看。