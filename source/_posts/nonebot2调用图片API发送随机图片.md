---
title: nonebot2调用图片API发送随机图片
tags:
  - nonebot2
  - python
  - QQ机器人
swiper_index: 3
swiper_desc: nonebot2调用图片API发送随机图片插件编写指南
categories: 
  - nonebot2
abbrlink: 39795
date: 2022-08-13 12:00:00
description: nonebot2调用图片API发送随机图片插件编写指南

---

# 前言

我们经常可以看到能够发送随机图片的QQ机器人，接下来我们会学习到如何编写这种插件

# 效果展示

![](http://img.sevin.cn/i/2023/06/07/647ff05420517.png)

# 正文

##　图片ＡＰＩ选择

图片API可以按照其返回数据的方式分成几种，我这里使用的API的类型是直接返回图片的URL，就比如说访问我自己部署的一个二次元图API：[https://api.sevin.cn/api/ecy.php]（https://api.sevin.cn/api/ecy.php），他就会随机返回一张图片的URL，比如说：https://api.sevin.cn/api/img/ecy/ (17).jpg

![返回例子](http://img.sevin.cn/i/2023/06/07/647ff086dd636.png)

另一种返回json格式的API的使用方法请看这篇文章：[nonebot2调用json格式图片API发送随机图片](https://blog.csdn.net/m0_62568363/article/details/126539128)

至于这种图片API怎么制作，大家可以看我的这篇文章：[超简单随机图片API制作教程](https://blog.csdn.net/m0_62568363/article/details/126328130)。或者你直接去网上找现成的这种类型的现成图片API也可以

## 插件编写

### Step 1 定义命令

首先，我们需要定义插件命令，只有成功调用了命令，才能触发插件操作。在本插件中，我们使用 on_command 装饰器定义一个命令，当用户输入特定的命令时，机器人就会执行相应的操作。例如，我们定义命令为“二次元图”：

```python
from nonebot import on_command

ecyt = on_command('二次元图')
```

### Step 2 编写插件逻辑

接下来，我们可以在 on_command 修饰器下使用 handle 装饰器来编写插件逻辑，当用户触发命令时，机器人就会执行相应的逻辑。在本插件中，我们需要从图片 API 获取随机图片的 URL，并将其发送给用户。

```python
@ecyt.handle()
async def main():
    # 获取随机图片 URL
    msg = await get_data()

    # 发送图片给用户
    await ecyt.finish(MessageSegment.image(msg))

```

在上面的代码中，我们定义了一个名为 main 的异步函数，使用 await get_data() 来获取随机图片网址，然后使用 await ecyt.finish()发送随机图片URL。

### Step 3 调用图片 API

在 main 函数中，我们需要获取随机图片 URL，而我们可以使用 httpx 库中的异步函数异步获取图片 URL。在示例代码中，我们使用了一个图片 API，这个 API 它可以随机返回二次元图片的 URL。

```python
async def get_data():
    url = 'https://api.sevin.cn/api/ecy.php'
    async with httpx.AsyncClient() as client:
        resp = await client.get(url)
        data = resp.text.strip()
    return data

```

在上述代码中，我们使用 httpx 库中的 AsyncClient() 来实现异步请求，发出 GET 请求，从 API 获取随机图片 URL，并返回响应内容。

### Step 4 发送图片

在获得图片URL后，我们需要将其发送给用户。我们需要使用 nonebot.adapters.onebot.v11.message.MessageSegment 中的 image 函数。这个函数将 URL 转换成 Nonebot 内置的 image 消息段，使得机器人能够正确发送图片。

```python 
from nonebot.adapters.onebot.v11 import MessageSegment

await ecyt.finish(MessageSegment.image(msg))
```

在上述代码中，我们调用了 MessageSegment.image 函数，并将获取到的图片 URL 作为参数传递给了它。最后，我们调用了 ecyt.finish() 函数，将消息发送给了用户。

### Step 5 完整代码

将以上 Step 1 - Step 4 中的代码合并，便可得到本插件完整代码：

``` Python
from nonebot import on_command
from nonebot.adapters.onebot.v11 import MessageSegment
import httpx


ecyt = on_command('二次元图')


@ecyt.handle()
async def main():
    msg = await get_data()
    await ecyt.finish(MessageSegment.image(msg))


async def get_data():
    url = 'https://api.sevin.cn/api/ecy.php'
    async with httpx.AsyncClient() as client:
        resp = await client.get(url)
        data = resp.text.strip()
    return data

```

你需要把代码上面的“二次元图”改成你自己触发插件的命令，把代码上面的链接改成你要调用的API链接，然后如果你触发插件的命令是中文的，你可能需要把插件的编码改成utf-8（一般默认就是utf-8，但是你最好检查一下），不然会引发乱码

# 相关

[nonebot2调用文本API发送随机文本](https://blog.csdn.net/m0_62568363/article/details/126325208)