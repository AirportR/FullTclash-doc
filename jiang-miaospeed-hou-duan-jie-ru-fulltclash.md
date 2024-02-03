# 将MiaoSpeed后端接入FullTclash

### 介绍

MiaoSpeed是一个开源的连通性测试工具，采用Go语言编写，内部代理出站实现基于Clash项目。

您可以前往MiaoSpeed项目地址进一步了解：

{% embed url="https://github.com/miaokobot/miaospeed" %}

针对原始仓库，FullTclash项目组有它的fork仓库，该仓库的miaospeed将保持最大的兼容性：

{% embed url="https://github.com/AirportR/miaospeed" %}

接下来将如何对接miaospeed作详细说明。

### 编译成二进制并启动



首先你需要一个拥有公网IP地址的后端机器，或者让处于NAT下的后端机器进行内网穿透等。

自行编译二进制文件，或者用仓库、群里面提供的。

关于如何编译，项目仓库介绍得比较详细了，在此不多赘述。

* 启动你的miaospeed二进制，开启websocket服务：

```bash
./miaospeed server -bind <ip>:<端口> -token <你的启动token> -mtls

# 例子
./miaospeed server -bind 0.0.0.0:8765 -token SbbieN2e{Q?W -mtls
```

```
-mtls 参数的意思是，miaospeed会使用内部的根证书集进行TLS RTT测试，防止系统根证书劫持造成数据造假，开不开都无所谓，一般建议开。
更多参数可通过 ./miaospeed server 查看
```

* 主端配置文件修改

以下是一个对接的配置案例，你也可以在 ./resources/config.yaml.example 找到样例。

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

做好以上，就可以启动你的主端bot进行测试了。

### javascript脚本接入

&#x20;miaospeed如果想要测Netflix、youtube等流媒体，则需要编写相应的js脚本。关于如何编写，篇幅有限以后再说。现在假设你有了若干写好的js脚本，只需要把所有脚本放到 ./addons/js/ 文件夹下即可。

⚠️注意！

由于技术原因，js脚本的名字有一定限制，需要与python的测试脚本的名字对应，大小写均可，有中文的名字则也需要改成中文。

举个例子：

假设你有一个python测试脚本为netflix.py ，然后在里面的 SCRIPT 全局变量中的 "MYNAME" 为 "奈飞"

即：

netflix.py

```python
SCRIPT = {
    "MYNAME": "奈飞",
    "TASK": "",
    "GET": "",
}
```

那么你对应js脚本名字就得是 "奈飞.js" ，关于项目内置的9个检测项，同理，为绘图出现的项的名字。

### 兼容性

由于技术以及架构原因，目前并非完美兼容，尤其是与原版的miaospeed的兼容。

如果你使用的是原版miaospeed（即官方编译的版本），那么javascript脚本将不可用，原版miaospeed接入FullTclash仅支持：ping延迟检测、速度测试、拓扑测试(即将支持)。

如果你用的是本项目组的fork仓库编译而来的二进制，那么不会有以上问题。
