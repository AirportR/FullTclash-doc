# 杂项

### proxy

http代理端口(非socks5)，用于下载获取订阅链接，订阅链接在中国大陆打不开可尝试开启。

格式为： host:端口

本机提供的代理可以这样填:&#x20;

> ```yaml
> proxy:  '127.0.0.1:7890'
> ```

如果有验证，配置格式为: proxy: "用户名:密码@host:端口"

> 示例：
>
> ```yaml
> proxy: "user1:112233@127.0.0.1:7890"
> ```

### geoip-api

GEOIP 测试api，取二级域名,目前支持 ip-api.com ip.sb ipleak.net ipdata.co ipapi.co 五种，其中 ipdata 需要配置key

> 示例：
>
> ```yaml
> geoip-api: ip.sb
> ```

### geoip-key

有些geoip的api需要配置token/key。比如 ipdata.co

> 示例：
>
> ```yaml
> geoip-key: 123456abcdefg123456
> ```

### pingurl

延迟测试的URL，亦可称为URLtest。计算HTTP数据包的往返时间。

> 默认值：
>
> ```yaml
> pingurl: http://www.gstatic.com/generate_204
> ```
>
> HTTP，极容易被劫持，造成数据造假。因此可以改成HTTPS(虽然还是有可能被劫持)：
>
> ```yaml
> pingurl: https://www.gstatic.com/generate_204
> ```
>
> 以及，所谓的GooglePing：
>
> ```yaml
> pingurl: https://www.google.com
> ```

### netflixurl

奈飞流媒体非自制影片解锁的检测URL。此项配置需要一个奈飞非自制剧网页。

> 示例（默认值）：
>
> ```yaml
> netflixurl: "https://www.netflix.com/title/80113701"
> ```

### speednodes

单次速度测试的节点数量限制，默认为300。

### speedthread

速度测试的线程，默认为4

> 示例：
>
> ```yaml
> speednodes: 100 #很少有超过100节点的订阅。
> speedthread: 1 #设置为1为单线程
> ```

### speedfile

自定义测速文件。测试时将请求这里配置的测速文件URL。默认值为：[https://dl.google.com/dl/android/studio/install/3.4.1.0/android-studio-ide-183.5522156-windows.exe](https://dl.google.com/dl/android/studio/install/3.4.1.0/android-studio-ide-183.5522156-windows.exe)

可以单个URL，也可以设置多个URL。

🔍为什么需要多个测速文件的URL？

因为部分使用者，可能测速的带宽很大，几秒钟就把文件下完了。如果只有一份文件，这时单个节点的测速时长还没走完，就会呈现无数据的下载的情况，因此多个测速文件可以保证进行完整测速。

当然，想要出现这种情况，要在单线程的情况下的测速带宽至少为 1Gbps 一般人达不到这个标准。多线程测速几乎不会出现这种情况。&#x20;

> 示例1（单个URL）：
>
> ```yaml
> speedfile: "https://dl.google.com/dl/android/studio/install/3.4.1.0/android-studio-ide-183.5522156-windows.exe"
> ```
>
> 示例2（多个URL）：
>
> ```yaml
> speedfile:
> - "https://dl.google.com/dl/android/studio/install/3.4.1.0/android-studio-ide-183.5522156-windows.exe"
> - "https://dl.google.com/dl/android/studio/install/3.4.1.0/android-studio-ide-183.5522156-windows.exe"
> - "https://dl.google.com/dl/android/studio/install/3.4.1.0/android-studio-ide-183.5522156-windows.exe"
> ```

### speedconfig

#### interval

单个节点测速的时长，默认为10 ，单位秒（s）。

> 示例：
>
> ```yaml
> speedconfig:
>  interval: 10
> ```

### nospeed

禁用速度测试，默认false。设置为true后，bot将拒绝所有的测速服务。

> 示例：（禁用测速）
>
> ```yaml
> nospeed: true
> ```

### entrance

节点拓扑测试的入口显示项配置。仅有两个有效值：ip、cluster。

设置为ip将显示入口ip段，设置为cluster将显示簇，默认设置为ip，这里的簇为入口域名绑定的ip地址数量。

> 示例1（显示为入口ip段）：
>
> ```yaml
> entrance: ip
> ```
>
> 示例2（显示为簇）：
>
> ```yaml
> entrance: cluster
> ```

### user

用户列表。最好不要在配置里设置。推荐用bot的 /grant 指令进行授权，经过授权的用户ID会保存在这里，ID为Telegram的用户ID。

> 示例：
>
> ```yaml
> user: 
> - 12345677 #第一个授权ID
> - 23456779 #第二个授权ID
> ```

### emoji

用于结果绘图时提供emoji表情支持。

#### enable

是否启用，默认启用（true）。若否（false），则在输出图片时emoji将无法正常显示。关闭该项可解决部分图片生成失败的问题。

#### emoji-source

emoji表情源。默认值为TwitterPediaSource。分为web源与本地源。可配置的值参考 ./libs/emoji\_custom/\_\_**all\_\_** 里面的成员变量。目前本地源仅支持: TwemojiLocalSource&#x20;

> 示例：
>
> ```yaml
> emoji: #emoji可选配置
>  enable: true #是否启用,默认启用。若否，则在输出图片时emoji将无法正常显示。关闭该项可解决部分图片生成失败的问题。（可选配置）
>  emoji-source: 'TwemojiLocalSource' #开启本地源，bot启动时会自动下载emoji资源。
> ```

### font

自定义字体。此配置的值为字体文件的路径（绝对路径和相对路径均可），默认值为 ./resources/alibaba-Regular.ttf

> 示例：
>
> ```yaml
> font: "./resources/alibaba-Regular.ttf"
> ```

### subinfo

bot通过 /new 指令添加的订阅会保存在这。不推荐读者自己配置该项。
