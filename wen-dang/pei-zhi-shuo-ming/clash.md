# clash

### path

此项在3.5.3版本之前（包含3.5.3），表示一个clash二进制文件。对于此文件，可以从[这里](https://github.com/Dreamacro/clash/releases)下载对应系统架构的二进制文件。

3.5.8 以上：

由于动态库加载用在python会产生奇怪的bug，所以重写成了专用的代理客户端，即&#x20;

[FullTCore](https://github.com/AirportR/FullTCore)

此项为其二进制文件的路径。

示例:

```yaml
clash:
 path: ./bin/FullTCore
```

### branch

3.6.0 加入。用于指定FullTCore代理客户端上游为meta分支，仅有两个有效值： \["origin", "meta"]。

如果不指定为meta分支，那么bot会自动过滤meta支持的新协议。



注意：指定为meta分支并不意味着你可以测vless等新协议了。你还需要前往FullTCore项目主页获取meta分支编译好的二进制。并且配置好路径

> 示例1:
>
> ```yaml
> clash:
>  branch: meta # 指定为meta分支
> ```

### cache-time

✨Premium专属配置

允许在内存中缓存测试过程产生的订阅的存活时间，若为0或者负数，则不允许缓存订阅。若为正数，则该值的单位为秒，默认60秒。

> ```yaml
> 示例:
> clash:
>  cache-time: 60
> ```

### allow-caching (3.6.0起已弃用)

3.6.0改动：已去除本地缓存功能。

是否允许缓存订阅到本地。如果是，则测试过程中的所有订阅将会保存在 ./clash/ 目录下。此项默认为否。

> 示例1：
>
> ```yaml
> clash:
>  allow-caching: true #开启状态
> ```
>
> 示例2：
>
> ```yaml
> clash:
>  allow-caching: false #关闭状态
> ```



### core

核心数。此项的值为整数，表示在测试过程将占用多少个测试端口，数字越大，测试速度越快。默认值为1,最大为64。超过64该配置无效。

打个比方，有一百个节点，此时的核心数为2，那么程序在测试时将分为100/2=50个批次，每批次测试2个节点。

如果将核心数修改为10，那么将会把测试节点分成 100/10=10个批次，每批次测试10个节点。

在同一批次中，这些节点是 **并发** 进行测试的，所以测试速度会得到极大的改善。如果你想核心数设置为1，那个测试速度是非常难受的。

⚠️ 注意 速度测试对于此项不适用。

> 示例：
>
> ```yaml
> clash:
>  core: 4
> ```

### auto-start (3.6.0起已弃用)

自动开启测试监听端口，如果核心数为4，则开启4个监听端口。

bot启动时顺带启动，若为false则需要在 bot上输入 /clash start 手动启动，默认false。

⚠️ 注意。启动后将无法使用 ctrl+c 退出程序。如果强行退出，则绑定的监听端口将无法释放，将会一直占用。这种情况需要读者自行杀死残留进程。

> 示例：
>
> ```yaml
> clash:
>  auto-start: true #自动开启监听。
> ```

### startup (3.6.0起已弃用)

3.6.0开始将自动寻找端口，无需自己指定。

启动的监听端口的起始端口。默认为 1122 。

表示从此端口开始往下数占用数量，比如核心数为4，就会占用\[1124,1126,1128,1130]共4个端口，有时候，系统的其他进程会占用端口。遇到端口占用时可配置此项。推荐10000以上作为初始端口。

> 示例：
>
> ```yaml
> clash:
>  startup: 11240
> ```

