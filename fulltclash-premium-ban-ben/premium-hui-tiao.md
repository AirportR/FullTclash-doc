---
description: 此页介绍Premium回调高级功能
---

# Premium回调

Premium的回调功能相比社区版进行更好的优化，更容易地被编写和优化。

以下是编写Premium回调的教程，如果你不是开发者，现在就可以关闭此文章了。



其实和社区版相差不大，回调编写可以直接参阅：

{% content-ref url="../hui-tiao-gong-neng-gao-ji.md" %}
[hui-tiao-gong-neng-gao-ji.md](../hui-tiao-gong-neng-gao-ji.md)
{% endcontent-ref %}



本页面仅介绍差异之处。

我们给Premium加了一个约定，可以导入以下装饰器:&#x20;

```python
from botmodule.util import on_callback
```

on\_callback是一个类装饰器，它的定义源码如下：

```python
class OnCallback:
    def __init__(self, name: str = None, filters: "Filter" = None, description: str = "", rank: int = 0,
                 enable: bool = True, hook: Any = None,
                 stop_propagation: bool = False):
        """
        回调函数实例装饰器

        name: str # 需要指定一个名字作为该回调名字
        filter: "Filter" = None # pyrogram原生过滤器，来自 pyrogram.filters.Filter() 类
        description: str = "" # 描述和介绍该回调
        rank: int = 0  # 回调执行顺序优先级，数字越小，执行优先度越高
        enable: bool = True  # 是否启用该回调
        hook: Callable  # 一个预处理函数，用于在回调执行前调用，做预备工作。
        stop_propagation: bool = False  # 停止传播，立即返回，执行到此回调后立即返回，不管后续是否还有回调未执行。
        """
        self.name = name or "callback-" + create_name()
        self.filters = filters
        self.description = description
        self.rank = rank
        self.enable = enable
        self.hook = hook
        self.stop_propagation = stop_propagation
        self._call = None

    def __call__(self, func):
        self._call = func

        async def handler(client: "Client", message: "Message"):
            if self.enable is False:
                return True
            if self.filters and isinstance(self.filters, Filter):
                if iscoroutinefunction(self.filters.__call__):
                    checked = await self.filters(client, message)
                else:
                    checked = await client.loop.run_in_executor(
                        client.executor,
                        self.filters,
                        client, message
                    )
                if not checked:
                    return True
            if iscoroutinefunction(func):
                res = await func(client, message)
            else:
                res = await asyncio.get_running_loop().run_in_executor(client.executor, func, client, message)

            return res, self.stop_propagation

        return handler


on_callback = OnCallback
```

可以这样使用这个装饰器:&#x20;

```python
@on_callback(name="your callback name", description="描述这个回调", enable=True, stop_propagation=False, rank=1, hook=hookfunc)
async def callback(bot: Client, message: Message) -> bool:
    try:
        pass # 在这里写你的回调逻辑
    except Exception as e:
        print(e)
        
```

你可能注意到了，上面有一个hook=hookfunc参数

这个hook函数是调用callback函数之前被调用的，它可以用来做准备工作，比如配置加载，资源申请，注册更多的按钮响应函数等。hook函数本质上也是一个回调函数，它的第一个参数是 OnCallback类，即"callback"函数的装饰器。

hook函数调用的时机是在BOT /setting命令 --> 回调插件管理 页面的打开的一瞬间调用的。

比如下面这个hook函数，它的作用是让/seting命令里面能够呼出面板:

```python
from pyrogram.types import Message, CallbackQuery, InlineKeyboardButton as IKB, InlineKeyboardMarkup as IKM
from pyrogram.handlers import CallbackQueryHandler as CQHandler, MessageHandler
from pyrogram.handlers.handler import Handler
from pyrogram.errors import UserNotParticipant, RPCError
from pyrogram import Client, filters
from pyrogram.enums import ChatType

from glovar import app # bot的客户端实例
from utils import handler_delete_queue # pyrogram handler定时删除队列，我们不希望太多的handler出现，因为一旦使用 app.add_handler(cq_handler, 3),除非主动移除，否则会越来越多。造成资源浪费。
from botmodule.cfilter import dynamic_data_filter as dyn_flt, admin_filter # 这个在社区版源码上有具体实现
CALLBACK_HOME_PREFIX: str = "/api/addons/home?name="
def hookfunc(c: "OnCallback"):
    async def callback_homepage(bot: Client, call2: Union["CallbackQuery", "Message"]):
        enable_text = "✅已启用" if c.enable else "❌已禁用"
        text = (f"名称: `{c.name}`\n"
                f"描述: `{c.description}`\n"
                f"状态: {enable_text}\n"
                f"优先级: {c.rank}\n"
                f"过滤器: {type(c.filters).__name__}\n\n")
        await call.answer("hook回调已被执行~")

        if isinstance(call2, CallbackQuery):
            await call2.message.edit_text(text, reply_markup=IKM(content_keyboard))
        else:
            await call2.reply(text, quote=True, reply_markup=IKM(content_keyboard))

    cq_handler = CQHandler(callback_homepage, filters=dyn_flt(CALLBACK_HOME_PREFIX + c.name) & admin_filter())
    app.add_handler(cq_handler, 3)
    handler_delete_queue.put(cq_handler, 3, 15) # 你可以不使用这个，手动在合适的时机移除。
```
