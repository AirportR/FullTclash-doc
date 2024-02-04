---
description: 后端对接的相关配置
---

# slaveconfig

### 描述

FullTClash有两种对接后端的方式，具体解释详见：

{% content-ref url="../../fulltclash-qian-hou-duan-mo-shi-she-ji-si-xiang-ji-yu-userbot.md" %}
[fulltclash-qian-hou-duan-mo-shi-she-ji-si-xiang-ji-yu-userbot.md](../../fulltclash-qian-hou-duan-mo-shi-she-ji-si-xiang-ji-yu-userbot.md)
{% endcontent-ref %}

以及 Premium 专属的 websocket对接方式：

{% content-ref url="../../websocket-qian-hou-duan-mo-shi-shuo-ming.md" %}
[websocket-qian-hou-duan-mo-shi-shuo-ming.md](../../websocket-qian-hou-duan-mo-shi-shuo-ming.md)
{% endcontent-ref %}

正常情况下，读者无需手动配置该项，应当使用在bot里使用 /connect 和 /sconnect 配置对接。

但有个特殊情况，本地后端像改动某个配置：

### 示例

本地后端（特殊键）

```yaml
slaveconfig:
  default-slave: #这个值是固定给本地后端用的，你可以理解为它就是本地后端的配置。
    comment: "本地后端 [meta]" #备注，绘图那里后端显示的值，可以在这里更改
    hidden: false # 3.6.5新增。是否隐藏后端，默认不隐藏，即 false ，想隐藏可以改为 true
```

以下为Premium专属的websocket后端类型配置写法：

```yaml
slaveconfig:
  "slave1": #第一个后端，注意这里的名字是随便填的，是为了方便你该配置所标记的。
    address: 127.0.0.1:8765 #此项配置为websocket后端专属配置，当type为websocket时才有效。后端地址格式为 ip:port ，也可以是 域名:port。
    comment: "ws后端 [ws] [meta]" #后端备注，在测试图显示的。
    public-key: "12345678" #后端解密的通讯token，也叫做通信密钥，密钥不对无法对接成功。
    path: "/don't set a simple path"  #后端ws连接路径，默认为/ ，这里填配置里显示的路径。
    type: "websocket" #此项指明后端连接类型。仅有三个有效值：["websocket", "bot", "miaospeed"] 这里websocket后端。
```

以及Premium专属的Miaospeed后端配置写法：

```yaml
slaveconfig:
  "slave2": #后端id，即slaveid
    address: 127.0.0.1:8765
    comment: "miao后端" #后端备注，在测试图显示的。
    public-key: "12345678" # 如果为miaospeed后端类型，则此项对应miaospeed里的启动token
    skip-cert-verify: true #如果你的miaospeed的证书是自签证书，请设置为true，否则无法连接miaospeed。默认值为false，即默认验证证书有效性。
    tls: true # 连接miaospeed启用了tls，即运（传）输层安全
    invoker: "1234567890" # miaospeed白名单的botid伪装，不填默认为主端的botid。默认即可
    type: "miaospeed"
    branch: "fulltclash" # miaospeed仓库分支，以便内部兼容优化。仅有两个有效值: ["fulltclash", "origin"]，如果你不是用的本项目组的分支fulltclash，请设置为origin
    buildtoken: "11111|22222|33333|44444" #仅当type为miaospeed可用,可以单独给该后端设置buildtoken，这样配置里的默认miaospeed-buildtoken就不会生效。默认不用填
    miaospeedConfig: #仅当type为miaospeed可用
      downloadURL: "https://dl.google.com/dl/android/studio/install/3.4.1.0/android-studio-ide-183.5522156-windows.exe" # 自定义测速文件地址
      stunURL: "udp://stun.ideasip.com:3478" # 自定义UDP类型测试地址
      downloadDuration: 8 # 测速时长，单位为秒
      downloadThreading: 4 # 测速线程
      pingAverageOver: 3 # ping的次数，取平均值
      pingAddress: "https://cp.cloudflare.com/generate_204" # 自定义URLtest 延迟测试地址（强烈建议写HTTPS前缀）
      taskRetry: 3 # 任务重试次数

```
