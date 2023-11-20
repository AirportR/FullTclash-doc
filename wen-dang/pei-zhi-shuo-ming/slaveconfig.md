---
description: 后端对接的相关配置
---

# slaveconfig

### 描述

FullTClash有两种对接后端的方式，具体解释详见：

{% content-ref url="../../fulltclash-qian-hou-duan-mo-shi-she-ji-si-xiang.md" %}
[fulltclash-qian-hou-duan-mo-shi-she-ji-si-xiang.md](../../fulltclash-qian-hou-duan-mo-shi-she-ji-si-xiang.md)
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
```

以下为websocket专属配置写法：

```yaml
slaveconfig:
  "slave1": #第一个后端，注意这里的名字是随便填的，是为了方便你该配置所标记的。
    address: 127.0.0.1:8765 #后端地址，格式为 ip:port ，也可以是 域名:port
    comment: "ws后端 [ws] [meta]" #后端备注，在测试图显示的。
    public-key: "12345678" #后端解密的通讯token，也叫做通信密钥，密钥不对无法对接成功。
    type: "websocket" #仅有两个有效值：["websocket", "bot"] 这里websocket后端。
```
