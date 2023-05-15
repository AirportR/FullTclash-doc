# /topo & /topourl

### 解释

发起一次拓扑测试（通俗叫法为节点出入口分析），等到bot后台测试完成后将发送一张测试结果图片， 测试期间bot会发送测试进度。topourl是 topo 的派生指令。

### 别名

该指令有其他的触发文本，效果等同：

* analyze & analyzeurl

### 参数

/topo 的第一个参数是一个订阅名，而 /topourl 的第一个参数是一个订阅地址(URL形式)，除此之外其他参数均一致

* /topourl 的指令参数：

```
/topourl <订阅URL> <包含过滤器> <排除过滤器>
```

* /topo 的指令参数：

```
/topo <订阅名> <包含过滤器> <排除过滤器>
```

* <包含过滤器> 和 <排除过滤器> 的使用与 /test 一致，使用方法移步 /test 指令中的说明。

### 使用

> 例子1：
>
> ```
> /topourl https://www.google.com
> ```
>
> 例子2：
>
> ```
> /topo coffee
> ```



## 特殊派生指令

* /inbound
* /outbound&#x20;
* /inboundurl
* /outboundurl

它们的参数均与 /topo 和 /topourl 对齐

区别是

/inbound & /inbound 仅仅作入口分析，如果只想测试入口数据，可以选用此派生指令。

/outbound & /outboundurl 仅仅作出口分析，如果只想测试出口数据，可以选用此派生指令。

### 效果

效果几乎等同/test，读者自行尝试
