---
title: nonebot2调用json格式图片API发送随机图片
tags:
  - nonebot2
  - python
  - QQ机器人
swiper_index: 3
swiper_desc: nonebot2调用json格式图片API发送随机图片教程以及插件模板，满满干货！
categories: 
  - nonebot2
date: 2022-08-26 12:00:00
description: nonebot2调用json格式图片API发送随机图片教程以及插件模板，满满干货！

---

# 前言

前文讲了如何调用直接返回图片链接的格式的API，有粉丝问如何调用json格式的，于是就有了这篇文章

[nonebot2调用图片API发送随机图片](https://blog.csdn.net/m0_62568363/article/details/126324799)

# 正文

## json处理讲解

推荐这篇文章，将Python处理json格式讲得通俗易懂，以下的讲解我就默认你看了这篇文章已经学会了json的序列化和反序列化（以后如果有时间我会讲一些这种nonebot额外的Python基础）

[干货｜Python处理JSON格式的数据，太详细了吧！](https://blog.csdn.net/weixin_38037405/article/details/107075666)

## 插件编写

1. 这里以调用樱花随机二次元图片API-樱花的json格式的图片API为例，我们先获取API的URL

![img](http://img.sevin.cn/i/2023/06/07/64803224a6e79.png)

2. 然后在浏览器上打开上面获取的URL，观察他返回的json数据。我们可以看到，他返回的图片链接对应的是"imgurl"

![img](http://img.sevin.cn/i/2023/06/07/648032248609c.png)

3. 之后我们就可以就可以通过json.loads将以上的数据反序列化到一个字典当中，再获取字典中imgurl对应的值就能得到图片链接了

```python
import json

get_dic = json.loads(resp.text)
imgurl = get_dic['data']
```

## 插件模板

把模板放在着了，大家可以参考我下面的代码以及查看nonebot官方文档自行研究，或者参考[nonebot2调用图片API发送随机图片](https://blog.csdn.net/m0_62568363/article/details/126324799)的讲解，代码如下

```python
from nonebot import on_command
from nonebot.adapters.onebot.v11 import MessageSegment
import httpx
import json


ecyt = on_command('二次元图')


@ecyt.handle()
async def main():
    msg = await get_pic()
    await ecyt.finish(MessageSegment.image(msg))


async def get_pic():
    url = 'https://www.dmoe.cc/random.php?return=json'
    async with httpx.AsyncClient() as client:
        resp = await client.get(url)
        get_dic = json.loads(resp.text)
    data = get_dic["imgurl"]
    return data
```

你需要把代码上面的“二次元图”改成你自己触发插件的命令，把代码上面的链接改成你要调用的API链接，把从json数据获取图片链接的步骤按照你调用的API返回的数据进行修改，然后如果你触发插件的命令是中文的，你可能需要把插件的编码改成utf-8（一般默认就是utf-8，但是你最好检查一下），不然会引发乱码

# 相关

[超简单随机图片API制作教程](https://blog.csdn.net/m0_62568363/article/details/126328130)

[nonebot2调用json格式文本API发送随机文本](https://blog.csdn.net/m0_62568363/article/details/126689576)

