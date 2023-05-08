---
description: bot配置相关说明，以下配置全部隶属于'bot'这一父项。
---

# bot

### api\_hash

从telegram获取的api\_hash

### api\_id

从telegram获取的api\_id

### bot\_token

从 @BotFather 创建一个机器人后，而得到的控制机器人的唯一令牌。

> 示例：
>
> ```yaml
> bot:
>  api_hash: "ABCDEFG"
>  api_id: "123456"
>  bot_token: "123456:ABCDEFG"
> ```

### proxy

bot需要与telegram官方进行网络通讯。在面对某些国家地区（如中国大陆）可能会受阻。这时候我们就需要通过代理帮助bot连接。此代理必须为**socks5**代理类型。

> 1、无身份验证形式。格式为 host:端口
>
> 示例：
>
> ```yaml
> bot:
>  proxy: 127.0.0.1:7890
> ```
>
> 2、需要身份验证。格式为 host:端口:用户名:密码
>
> 示例：
>
> ```yaml
> bot:
>  proxy: 127.0.0.1:7890:username:123456789
> ```

### scripttext

连通性测试过程中出现的提示文本，默认值为如下图所示。

<figure><img src="../../.gitbook/assets/屏幕截图 2023-04-23 141543.png" alt=""><figcaption></figcaption></figure>

> 示例
>
> ```yaml
> bot:
>  scripttext: "⏳联通性测试进行中..."
> ```

### analyzetext

节点拓扑测试过程中出现的提示文本，默认值为如下图所示。

<figure><img src="../../.gitbook/assets/屏幕截图 2023-04-23 141859.png" alt=""><figcaption></figcaption></figure>

> 示例
>
> ```
> bot:
>  analyzetext: "⏳节点拓扑测试进行中..."
> ```



### speedtext

速度测试过程中出现的提示文本，默认值为如下图所示。

<figure><img src="../../.gitbook/assets/屏幕截图 2023-04-23 142104.png" alt=""><figcaption></figcaption></figure>

> 示例:
>
> ```yaml
> bot:
>  speedtext: "⏳速度测试进行中..."
> ```

### bar

已完成的测试进度条，默认值为 "="

<figure><img src="../../.gitbook/assets/屏幕截图 2023-04-23 144040.png" alt=""><figcaption></figcaption></figure>

如上图中的猫猫头像为已完成的部分。

### bleft

左边边界框条，默认值为 \`\[&#x20;

### bright

右边边界框条，默认值为 ]\`

### bspace

未完成的测试进度条，默认值为 "  "  （双引号里面为两个空格）

> 以上四个配置的完整示例：
>
> ```yaml
> bot:
>  bar: "="
>  bleft: "["
>  bright: "]"
>  bspace: "  "
> ```

### command

高级用法。用于权限回调，此配置为一个数组。每一个数组成员为一个字符串。

此配置的作用是在bot注册一个指令。举个例子：

bot原生支持的指令有 /test /testurl /speed /analyze /new 等等，这些都是需要用代码去“注册”，让bot能“听到”这些声音。比如你给bot发一个不存在未注册的指令 /mycommand 它是不会回应你的。但是现在我们可以在这里配置要注册的指令。如下这个例子：

> 示例：
>
> 多行形式：
>
> ```yaml
> bot:
>  command: 
>  - "command1"
>  - "command2"
>  - "command3"
> ```
>
> 当然单行形式也是可以的：
>
> ```yaml
> bot:
>  command: ["command1", "command2", "command3"]
> ```

以上两种形式没有区别，看个人写法喜好。写下这些配置，就可以写权限回调脚本的时候，接收到相应的指令。这个配置只是辅助，想让bot多一点功能还得写相应的代码。

注意：这个特性是本项目的限制，并非上游api的限制。
