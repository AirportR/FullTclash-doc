# /share

### 解释

分享订阅的测试权限给其他用户。出于安全考虑，每个用户组内的用户之前的订阅是隔离的。意味着用户之间无法访问彼此的订阅。不是自己添加的订阅，正常情况下不能发起针对该订阅的测试，唯有通过这个指令，可以进行“分享”订阅的测试权限。

请注意！仅仅只是分享了测试权限，TA**依然无法**查看您的原始订阅信息。**不会**暴露订阅链接。

### 参数

```
/share <回复一个目标> <订阅名>
```

```
<回复一个目标>    该占位符的意思是需要将该指令回复给对应目标，对应目标会获得订阅名所对应的测试权限
<订阅名>    您在 /new 中添加的订阅名，订阅名可通过 /sub 指令列出。
```

### 使用

> ```
> /share 谷歌云
> ```

### 特性

* 若用户输入的订阅名不是该用户所添加的，说明不是该用户不是这个订阅的所有者，分享失败。
* 若用户输入的订阅名不存在，分享失败

### 效果

* 未回复一个目标时：

<figure><img src="../.gitbook/assets/image (3) (1) (1).png" alt=""><figcaption></figcaption></figure>

* 不是订阅所有者时：

<figure><img src="../.gitbook/assets/image (4) (1).png" alt=""><figcaption></figcaption></figure>

* 分享成功时：

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>
