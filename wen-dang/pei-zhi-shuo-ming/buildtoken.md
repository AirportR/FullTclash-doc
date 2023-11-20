---
description: FullTClash代理后端的编译token
---

# buildtoken

## 描述

如果你自己编译了代理客户端FullTCore，并且编译token为自己制定的而非默认的，那么你应该在此处配置你自己指定编译token，bot会读取这里的token替换默认的token，否则代理客户端数据交互时将无法解密。

## 示例

```yaml
buildtoken: 1234567890abcdefgh
```

