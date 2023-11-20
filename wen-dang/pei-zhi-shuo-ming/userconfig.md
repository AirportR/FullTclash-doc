---
description: 用户使用过程的相关配置
---

# userconfig

### 描述

此项配置里包含bot使用过程中可以优化使用体验的配置



### 示例

```yaml
userconfig: #用户权限组相关配置
  rule: #测试时的默认规则,3.6.0加入。注意，强烈建议在bot里使用 /setting 查看规则面板添加规则，手动添加规则容易出错。
    "规则名":
      enable: true #是否启用激活该规则
      slaveid: local  #slaveid的有效值参照配置里的 slaveconfig下的所有键。
      script: ["Netflix", "Youtube", "Disney+", "维基百科"] #script的有效值参照连通性测试绘图结果中显示的名称（大小写敏感）。
      # 特殊值说明：由于script里面的值太多，你可以使用"全测" 或者 "all" 替代。这两个特殊值会自动帮你导入所有规则。
      #script: "全测"
      #script: "all"
      # 此外,script的值不一定是数组，以下是premium版本专属用法：
      # script可以设置为一个字符串，表示模糊匹配
      # 例如，当script值为 "hbo" ，导入的脚本名称含有 "hbo"时将命中匹配，
      # 例如有三个这样的脚本: "hbomax" "hbogo" "netflix" ，那么会匹配出两个符合条件脚本："hbomax", "hbogo"
      sort: "HTTP升序" #排序
```
