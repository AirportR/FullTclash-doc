# /test & /testurl

### 解释

发起一次连通性测试（通俗叫法为流媒体解锁测试），等到bot后台测试完成后将发送一张测试结果图片， 测试期间bot会发送测试进度。testurl是 test的派生指令。

### 参数

/test 的第一个参数是一个订阅名，而 /testurl 的第一个参数是一个订阅地址(URL形式)，除此之外其他参数均一致

* /testurl 的指令参数：

```
/testurl <订阅URL> <包含过滤器> <排除过滤器>
```

* /test 的指令参数：

```
/test <订阅名> <包含过滤器> <排除过滤器>
```

* <包含过滤器>

> 该参数接受一些字符串，用以选择只测试哪些节点。支持正则表达式(Python re模块正则)

* <排除过滤器>

> 该参数接受一些字符串，用以选择不要测试哪些节点。支持正则表达式(Python re模块正则）

### 使用

> 例子1：
>
> ```
> /testurl https://www.google.com
> ```
>
> 例子2：
>
> ```
> /test coffee
> ```
>
> 例子3：
>
> 仅测试一个订阅



### 效果

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>
