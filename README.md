---
description: 🤖 节点质量检测的Telegram机器人
---

# FullTClash

## 基本介绍

FullTClash名字来源于 Full Test base on Clash 。

后端部分使用[Clash项目](https://github.com/Dreamacro/clash)(现在亦可称之为[mihomo](https://github.com/MetaCubeX/mihomo))相关代码作为出站代理，前端部分使用Telegram API作为交互界面，需配合Telegram使用，即为一个Telegram机器人(bot)， FullTClash bot 是承载其测试任务的Telegram 机器人（以下简称bot）。\
目前支持以Clash配置文件为载体的**批量**连通性测试，支持以下测试条目:

1. Netflix
2. Youtube
3. DisneyPlus
4. Bilibili解锁
5. OpenAI(ChatGPT)
6. 落地IP风险(IP欺诈度)
7. 维基百科
8. 微软Copilot
9. Claude
10. 落地DNS区域检测
11. Spotify
12. SSH 22端口封禁检测
13. Tiktok

此外还有：

1. HTTP请求延迟测试
2. 链路拓扑测试（节点出入口分析）。
3. 下行速度测试

## 主要功能

* asyncio异步支持
* 订阅管理
* 测试结果绘图
* 权限控制
* 文档支持
* 基于Pyrogram框架
* 规则系统
* 支持Docker
* 命令行支持
* 日志输出
* 插件扩展
* 自由定制化配置

## 如何开始?

你可以在这里阅读快速搭建指南：

{% content-ref url="kuai-su-kai-shi.md" %}
[kuai-su-kai-shi.md](kuai-su-kai-shi.md)
{% endcontent-ref %}

## 更多文档

你可以在这里找到关于本项目的配置说明:

{% content-ref url="wen-dang/pei-zhi-shuo-ming/" %}
[pei-zhi-shuo-ming](wen-dang/pei-zhi-shuo-ming/)
{% endcontent-ref %}
