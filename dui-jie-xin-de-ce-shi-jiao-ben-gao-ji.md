# 对接新的测试脚本（高级）

## 前言

此指南目的在于给想要自己添加测试项的开发者一个快速入门的机会。如果你是一个使用者，而非开发者，那么看到这里你可以关掉本文章了。 本文章仅作抛砖引玉，有更好的外接脚本方法可以进行讨论。

## 基础要求

想要新增流媒体测试项，首先需要一定的python基础知识。学会核心基础模块，异步库： aiohttp [官方文档](https://docs.aiohttp.org/en/stable/)

## 开始编写

可以看看项目中的netflix，tvb是咋写的，做到触类旁通就好。 首先分为，三个部分：采集数据函数，后续清洗数据函数、以及创建协程任务，以下为模板。

* 在addons文件夹下新建一个py文件,如 XXX.py ,xxx是随便取的名字，一般对应流媒体的名字即可。然后在这个文件里编写相关函数。
* 模块导入

基本的模块导入

```
import asyncio # 异步io模块
import aiohttp # 爬取网页要用
from aiohttp import ClientConnectorError # 错误处理
from loguru import logger # 日志
```

* 采集函数

```python
async def fetch_XXX(Collector, session: aiohttp.ClientSession, proxy=None, reconnection=2):
    """
    XXX检测, XXX是流媒体的名字
    :param Collector: 采集器，来自 libs.collector.Collector() 类
    :param session: session，来自 aiohttp.ClientSession() 类
    :param proxy: 默认None即可，采集器会设置代理，这里不用设代理。
    :param reconnection: 重连次数，如果网络不稳定可能会造成请求失败，所以会有重新发送请求机制，默认为2
    :return: 不返回数据，所有数据维护在 Collector.info 属性中，它是一个字典。
    """
    try:
        # 这里写下你的测试逻辑
        async with session.get(_url, proxy=proxy, timeout=5) as reqs:
            Collector.info['XXX'] = "解锁" # 将数据放入字典中
    # 强烈建议包含以下两个异常处理，可应对大部分情况。
    except ClientConnectorError as c:
        logger.warning("XXX请求发生错误:" + str(c))
        if reconnection != 0:
            await fetch_XXX(Collector, session=session, proxy=proxy, reconnection=reconnection - 1)
            
    except asyncio.exceptions.TimeoutError:
        logger.warning("XXX请求超时，正在重新发送请求......")
        if reconnection != 0:
            await fetch_XXX(Collector, session=session, proxy=proxy, reconnection=reconnection - 1)
```

采集函数是测试核心，怎样设计就看你python的功底了。

* 数据清洗

如果你在采集阶段就得到了测试的结果，那么这步就比较简单。这一步主要是为了获取干净的测试数据

提示：设计数据清洗的目的是为了区分功能，让采集器和清洗器各司其职，而不是让采集器干清洗数据的活。举个例子，假设拿到指定数据需要用到正则匹配，并且操作繁琐，那么应该写成以下这样的函数。采集器需要快速将请求内容输入完毕，这种可能增加时间的活应该先“放着”一边，之后交给清洗器处理。

```
def get_XXX_info(ReCleaner):
    """
    获得XXX解锁信息
    :param ReCleaner: 来自 libs.cleaner.ReClener() 类
    :return: str: 解锁信息: [解锁(地区代码)、失败、N/A等等]
    """
    try:
        if 'XXX' not in ReCleaner.data:
            logger.warning("采集器内无数据")
            return "N/A"
        else:
            logger.info("XXX解锁情况：" + str(ReCleaner.data.get('netflix_new', "N/A")))
            return ReCleaner.data.get('netflix_new', "N/A")
    except Exception as e:
        logger.error(e)
        return "N/A"
```

* 创建协程任务 创建了协程任务，以方便让协程并发工作。

```
def task(Collector, session, proxy):
    return asyncio.create_task(fetch_XXX(Collector, session, proxy=proxy))
```

* 最后的工作

在该脚本的**末尾**，新增一个全局变量 SCRIPT （必须大写）,它是python字典类型。 该变量需要有三个键： "MYNAME": 流媒体名字， "TASK": 协程任务函数名，不加括号 "GET": 获取解锁信息的函数名，不加括号

正确范例：

```python
SCRIPT = {
    "MYNAME": "Netflix",
    "TASK": task,
    "GET": get_xxx_info
}
```

至此，已完成全部工作，可以开始测试是否正常了。
