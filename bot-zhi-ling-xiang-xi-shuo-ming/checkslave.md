# /checkslave

### 解释

🟢Premium专属指令

检查websocket后端的在线情况。

### 参数

无参数

### 使用

```
/checkslave
```

### 特性

* 互斥锁机制，在本次检查结束前，其他用户使用该命令会拒绝服务，直到结束后锁释放。
* 结果缓存。检查结束会保存这次结果在内存中。覆盖上一个缓存结果。
* 用户权限只能查看缓存结果（除非没有缓存，这种情况为刚启动bot），管理权限可以刷新缓存结果。
* 有30秒冷却时间，也就是管理员最多每隔30秒检查一次，缓存结果展示没有限制。

### 效果

有其他用户检查时：

<figure><img src="../.gitbook/assets/image (8).png" alt=""><figcaption><p>互斥机制</p></figcaption></figure>

检查结果：

<figure><img src="../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>
