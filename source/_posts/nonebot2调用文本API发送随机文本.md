---
title: nonebot2调用文本API发送随机图片
tags:
  - nonebot2
  - python
  - QQ机器人
swiper_index: 2
swiper_desc: nonebot2调用文本API发送随机文本插件编写指南
categories: 
  - nonebot2
abbrlink: 39700
date: 2022-08-13 12:00:00
description: nonebot2调用文本API发送随机文本插件编写指南

---

# 前言

我们经常可以看到能够发送随机文本的QQ机器人，接下来我们会学习到如何编写这种插件

# 效果展示

![](http://img.sevin.cn/i/2023/06/07/647ff3b2491f8.png)

# 正文

##　文本ＡＰＩ选择

文本API可以按照其返回数据的方式分成几种，我这里使用的API的类型是直接返回文本，就比如说访问我自己部署的一个笑话API：[随机笑话](https://api.lklblog.cn/api/qwxh.php) ，他就会随机返回所需的文本，比如说：

> 早上骑车时不小心别到旁边宝马的车头，我摔在地上半天缓不过神，车主下车蹲在我身边失望地说：小兄弟，你这瓷碰的不够专业啊！你躺的地方所照射的阳光并不会让司机瞬盲，而且身体与车头的直线距离太长，很难假造碰撞伤害！我愣住了，问他为何懂的这么多，他拍拍宝马说："你以为它是怎么来的？

![返回例子](http://img.sevin.cn/i/2023/06/07/647ff3b258014.png)

另一种返回json格式的API的使用方法请看这篇文章：[nonebot2调用json格式文本API发送随机文本](https://blog.csdn.net/m0_62568363/article/details/126689576)

至于这种文本API怎么制作，大家可以看我的这篇文章：[超简单随机文本API制作教程](https://blog.csdn.net/m0_62568363/article/details/126328516)。或者你直接去网上找现成的这种类型的现成文本API也可以

## 插件编写

### Step 1 定义命令

首先，我们需要定义插件命令，只有成功调用了命令，才能触发插件操作。在本插件中，我们使用 on_command 装饰器定义一个命令，当用户输入特定的命令时，机器人就会执行相应的操作。例如，我们定义命令为“讲个笑话”：

```python
from nonebot import on_command

jgxh = on_command('讲个笑话')
```

### Step 2 编写插件逻辑

接下来，我们可以在 on_command 修饰器下使用 handle 装饰器来编写插件逻辑，当用户触发命令时，机器人就会执行相应的逻辑。在本插件中，我们需要从文本 API 获取随机文本的 URL，并将其发送给用户。

```python
@ecyt.handle()
async def main():
    # 获取随机文本 URL
    msg = await get_data()

    # 发送文本给用户
    await jgxh.finish(msg)

```

在上面的代码中，我们定义了一个名为 main 的异步函数，使用 await get_data() 来获取随机文本，然后使用 await ecyt.finish()发送随机文本。

### Step 3 调用图片 API

在 main 函数中，我们需要获取文本，而我们可以使用 httpx 库中的异步函数异步获取文本。在示例代码中，我们使用了一个文本 API，这个 API 它可以随机返回笑话的文本。

```python
async def get_data():
    url = 'https://api.sevin.cn/api/qwxh.php'
    async with httpx.AsyncClient() as client:
        resp = await client.get(url)
        data = resp.text.strip()
    return data

```

在上述代码中，我们使用 httpx 库中的 AsyncClient() 来实现异步请求，发出 GET 请求，从 API 获取随机图片 URL，并返回响应内容。

### Step 4 发送图片

在获得文本后，我们需要将其发送给用户。

```python 
await jgxh.finish(msg)
```

在上述代码中，我们调用了 jgxh.finish() 函数，将消息发送给了用户。

### Step 5 完整代码

将以上 Step 1 - Step 4 中的代码合并，便可得到本插件完整代码：

``` Python
from nonebot import on_command
import httpx


jgxh = on_command('讲个笑话')


@jgxh.handle()
async def main():
    msg = await get_data()
    await jgxh.finish(msg)


async def get_data():
    url = 'https://api.sevin.cn/api/qwxh.php'
    async with httpx.AsyncClient() as client:
        resp = await client.get(url)
        data = resp.text.replace("\\n", "\n")
    resp.close()
    return data
```

你需要把代码上面的“讲个笑话”改成你自己触发插件的命令，把代码上面的链接改成你要调用的API链接，然后如果你触发插件的命令是中文的，你可能需要把插件的编码改成utf8（一般默认就是utf8，但是你最好检查一下），不然会引发乱码

# 相关

[nonebot2调用图片API发送随机图片](https://blog.csdn.net/m0_62568363/article/details/126324799)