---
description: sub - subscription 的缩写
---

# /subinfo

### 解释

查询网络提供商的服务信息，也称为订阅信息。

### 别名

该指令有其他的触发文本，效果等同：

* traffic
* 流量查询
* 流量



### 参数

有一个必填参数，两种参数类型识别：

```
/subinfo <订阅链接的URL>
```

```
/subinfo <订阅名>
```

订阅名是bot之前通过 /new 指令添加的订阅名。

订阅链接URL为 http(s):// 开头的文本

### 使用

> 例子1：
>
> ```
> /subinfo https://www.google.com
> ```
>
> 例子2：
>
> ```
> /subinfo coffee
> ```

### 效果

<figure><img src="../.gitbook/assets/image (3) (1) (1).png" alt=""><figcaption></figcaption></figure>
