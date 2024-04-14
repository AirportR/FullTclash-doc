---
description: 订阅转换的部分配置
---

# subconverter

⚠️ 此项已经无人维护！

但仍然可用，可以将其他订阅格式转换成clash配置格式，因为bot仅支持clash配置格式。

### enable

是否启用，默认否（false）

### host

后端服务地址，格式为： host:端口

### remoteconfig

启用远程配置。默认遵循订阅转换后端的默认配置。此配置的值为一个URL地址

> 示例：
>
> ```yaml
> subconverter:
>  enable: true #启用订阅转换
>  host: "127.0.0.1:25500"
>  tls: True # 告诉bot启用HTTPS安全连接请求
>  remoteconfig: "https://raw.githubusercontent.com/ACL4SSR/ACL4SSR/master/Clash/config/ACL4SSR_Online.ini"
> ```

### include

节点包含过滤器的预处理。全局配置

### exclude

节点排除过滤器的预处理。全局配置

🔍从3.5.4版本开始，以上两项脱离subconvertor。意味着即使 enable 设为 false仍然生效。

这项配置存在的意义在于，可以预先过滤一些节点名称中包含广告、官网、套餐、流量等信息。

> 示例：
>
> ```yaml
> subconverter:
>  include: '' #设置为空。表示不启用。
>  exclude: '官网|套餐到期|剩余流量'
> ```
