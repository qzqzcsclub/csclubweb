---
title: 超简单随机文本API制作教程
tags:
tags:
  - nonebot2
  - QQ机器人
  - api
swiper_index: 2
swiper_desc: 随机文本API制作教程，超简单，包会！
categories: 
  - nonebot2
date: 2022-08-14 12:00:00
description: 随机文本API制作教程，超简单，包会！

---

#  前言

在我的前两篇文章我教大家怎么编写nonebot2发送随机文本插件：[nonebot2调用文本API发送随机文本_ITSevin的博客-CSDN博客](https://blog.csdn.net/m0_62568363/article/details/126325208)，现在我就教大家怎么在自己的服务器上制作随机文本API

# 步骤

1、首先新建一个joke.txt文件，在txt文件按照一行一个文本的格式写入你所以的文本，切记单个文本内不能换行！！！类似下面这样写

![img](http://img.sevin.cn/i/2023/06/07/647ffd60eb61d.png)

2.然后在我们的一个网站的根目录下创建一个api文件夹，在api文件夹中在创建一个txt文件夹，再把我们刚才的joke.txt上传到txt文件夹中，之后在api文件夹中创建一个joke.php文件，在这个文件里输入如下代码

```php
<?php
$txt='txt/joke.txt';
$a=file($txt);
$b=count($a);
$rand=rand(0,$b);
$rand_shuchu=$a[$rand];
echo $rand_shuchu
?>
```

3.现在我们就可以通过访问http://你网站的URL/api/joke.php调用你的API了![img](http://img.sevin.cn/i/2023/06/07/647ffd60d7f2d.png)

# 相关

[超简单随机图片API制作教程](https://blog.csdn.net/m0_62568363/article/details/126328130)

这里我还推荐一个免费的API管理网站（我自己使用的就是这个）：[萌新源API+API管理后台: 基于layui以及pear-Admin-layui开发的API管理后台](https://gitee.com/meng-xinyuan-mxy/mxy-api)https://gitee.com/meng-xinyuan-mxy/mxy-api)