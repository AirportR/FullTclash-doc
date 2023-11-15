# WebSocket前后端模式说明



WebSocket协议是基于TCP的一种网络通信协议。 它实现了客户端与服务器全双工（full-duplex）通信，即允许服务器主动发送信息给客户端。 因此，在WebSocket中，浏览器和服务器只需要完成一次握手，两者之间就直接可以创建持久性的连接，并进行双向数据传输，客户端和服务器之间的数据交换变得更加简单。



在FullTclash中，它大概可以描述为这样子：

<figure><img src=".gitbook/assets/ws.png" alt="" width="563"><figcaption></figcaption></figure>

从主端（也就是从bot）那里接受到用户发起的测试请求时，bot会通过websocket主动连接到后端，给后端发送测试请求，返回等待后端回传结果。在此期间，双方保持长连接，直到其中有一方断开连接。



## 如何使用



**由于技术原因，目前支持ws对接的版本为Premium版本，即未开源的私人使用版本。**

如果您是忠实的开源的拥护者或者仅为个人使用，那么github仓库上的开源版本已经足够使用，它包含了premium版本的 %95 的特性。

如果您坚持要体验Premium版本，请继续往下阅读。

### 获取

你可以从FullTclash交流群（邀请链接在频道简介）中获取到premium版本



### 搭建



Premium版本为已经打包好的编译版本，意味着您不需要配置任何环境。首先需要解压，然后找到主程序二进制文件，通常是叫做 "FullTclash"。

然后同样需要一份配置文件（配置文件写法参见快速开始），接着跟其他二进制文件启动方式一样, ./FullTclash 启动即可，全程不需要安装python环境。



### websocket后端对接

首先您需要搭建一个后端，这个后端所在的机器需要有公网ip或者内网穿透。

接着您需要前往本项目的backend分支拉取纯后端的运行代码：

<div align="center" data-full-width="true">

<figure><img src=".gitbook/assets/backend.png" alt="" width="283"><figcaption></figcaption></figure>

</div>

或者使用git：

```bash
git clone https://github.com/AirportR/FullTclash.git -b backend
```

启动后端的教程前往backend查看。很容易配置

启动好后，后端已经就绪，等到主端连接，主端需要配置一下后端的连接信息。

分为主端配置和后端配置，后端可以直接命令行启动，基础使用无需配置。

以下是一个对接ws后端的配置示例：

```yaml
slaveconfig:
  "随便写": # 默认后端配置。
    comment: "ws测试后端" # 默认测试后端的备注。
    public-key: "12345678abcdefg" # 后端的通信Token，也叫做通信密钥。密钥不对无法解密信息。
    type: websocket  #此项指明后端连接类型。仅有两个有效值: ["websocket", "bot"]
    address: "127.0.0.1:8765" # 此项配置为websocket后端专属配置，当type为websocket时才有效，这里填 host:port 格式。
```

在主端写上以上配置后，就可以在测试选择新的后端了。



### 问题答疑

1、websocket通信是否为明文：

答：通信过程全程加密，除非通讯密钥泄露。

2、是否支持启用TLS？

答：暂时不支持。目前已经有一层加密，未来将会跟进TLS。

3、是否支持IPV6后端？

答：需要配置DNS，也就是将域名添加一个AAAA记录，address那一栏填 域名:端口。

4、未来是否会开源websocket对接部分源码？

答：可能会、也有可能不会。在技术尚且不够成熟的时候，随意造的轮子可能让后端陷入危险境地。在互联网中，对网络通信应保持谨慎态度。

5、是否支持赞助？

答：很高兴您能看到最后，如果真的需要支持我，那您应该先了解我是怎样的人，亦或者我是谁？

比起赞助，我更希望FullTclash您能给一个star，以及改进它。


