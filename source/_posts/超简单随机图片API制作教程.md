---
title: 超简单随机图片API制作教程
tags:
  - nonebot2
  - QQ机器人
  - api
swiper_index: 3
swiper_desc: 随机图片API制作教程，超简单，包会！
categories: 
  - nonebot2
date: 2022-08-14 12:00:00
description: 随机图片API制作教程，超简单，包会！

---

#  前言

在我的前两篇文章我教大家怎么编写nonebot2发送随机图片插件：[nonebot2调用图片API发送随机图片_ITSevin的博客-CSDN博客](https://blog.csdn.net/m0_62568363/article/details/126324799)，现在我就教大家怎么在自己的服务器上制作随机图片API

# 步骤

1、首先我们将我们找来的图片放到一个我们电脑（Windows系统）的文件夹里，然后我们需要将这些图片按照顺序重命名，重命名成(1).jpg,(2).jpg的格式（别的类型的图片也可以，但是一定要统一类型），批量重命名的方法就是将这些图片全部选中，右键点击重命名，然后把原有的名字除了文件扩展名全部删掉，再点击回车，这个时候我们就能看到已经批量命名好了

![img](http://img.sevin.cn/i/2023/06/07/647ffb6263f32.png)

2.然后在我们的一个网站的根目录下创建一个api文件夹，在api文件夹中在创建一个img文件夹，再把我们重命名好的图片上传到img文件夹中，之后在api文件夹中创建一个img.php文件，在这个文件里输入如下代码

```php
<?php
$seed = time();
$num = rand(1,173);
$picpath = "http://api.lklblog.cn/api/img/ (".$num.").jpg";
echo $picpath
?>
```

你需要把代码上面的173改成你的图片数量，把api.lklblog.cn改成你的网站URL，把jpg改成你图片的扩展名

3.现在我们就可以通过访问http://你网站的URL/api/img.php调用你的API了

![img](http://img.sevin.cn/i/2023/06/07/647ffb62671a6.png)

然后你可以访问API返回的随机图片的URL看看有没有出现图片，有的话就代表成功了

![img](http://img.sevin.cn/i/2023/06/07/647ffb6297604.png)

PS：如果你不想要这种返回随机图片URL的API ，你可以通过重定向改成直接返回随机图片的API（看不懂的话就直接把下面的代码覆盖到img.php中），代码如下

```php
<?php
$seed = time();
$num = rand(1,173);
$picpath = "http://api.lklblog.cn/api/img/ (".$num.").jpg";
die(header("Location: $picpath"));
?>
```

同样的，你需要把代码上面的173改成你的图片数量，把api.lklblog.cn改成你的网站URL，把jpg改成你图片的扩展名

然后你再访问http://你网站的URL/api/img.php就会直接返回图片了

# 相关

[超简单随机文本API制作教程](https://blog.csdn.net/m0_62568363/article/details/126328516)

这里我还推荐一个免费的API管理网站（我自己使用的就是这个）：[萌新源API+API管理后台: 基于layui以及pear-Admin-layui开发的API管理后台](https://gitee.com/meng-xinyuan-mxy/mxy-api)