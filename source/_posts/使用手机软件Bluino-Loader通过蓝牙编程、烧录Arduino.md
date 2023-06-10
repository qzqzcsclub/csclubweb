---
title: 使用手机软件Bluino Loader通过蓝牙编程、烧录Arduino
tags:
  - Arduino
  - 烧录
swiper_index: 3
swiper_desc: 一些小伙伴或许因为没有电脑又想学习Arduino而犯愁，但是在这片文章中我将会带领大家来完美解决这个问题，我们将使用手机软件Bluino Loader通过蓝牙编程、烧录Arduino
swiper_cover: http://img.sevin.cn/i/2023/06/07/647fef3307e50.jpg
categories: Arduino
abbrlink: 39793
date: 2022-03-30 12:00:00
description: 一些小伙伴或许因为没有电脑又想学习Arduino而犯愁，但是在这片文章中我将会带领大家来完美解决这个问题，我们将使用手机软件Bluino Loader通过蓝牙编程、烧录Arduino
cover: http://img.sevin.cn/i/2023/06/07/647fef3307e50.jpg

---

# 前言

一些小伙伴或许因为没有电脑又想学习Arduino而犯愁，但是在这片文章中我将会带领大家来完美解决这个问题，我们将使用手机软件Bluino Loader通过蓝牙编程、烧录Arduino

# 材料

## 硬件：

    蓝牙HC-05模块
    面包板
    电容 1uf/16v
    电阻 100 欧姆
    5 条杜邦线
    USB电缆
    Android 设备（支持蓝牙）
    电脑

![](http://img.sevin.cn/i/2023/06/07/647fef330e273.jpg)

## 软件：

    Android设备：来自 Google Play 商店的Bluino Loader​​​​
    电脑：Arduino IDE 

# 步骤：

1、先用电脑给Arduino烧录以下程序（只需烧录一次以后就不需要再次烧录了）

```arduino
void setup() 
{
    Serial.begin(38400);
    delay(500);   
    Serial.println("AT+NAME=Bluino#00");
    delay(500);
    Serial.println("AT+UART=115200,0,0"); //如果你用的是Arduino Uno、Bluino、Mega2560，就不用修改程序
    //Serial.println("AT+UART=57600,0,0");  //如果你用的是Arduino Nano、Leonardo、Micro、Pro Mini 3V3/5V、Duemilanove就把这一行最前面的2个斜杠去掉并在上一行前面加上2个斜杠
      delay(500);
      Serial.println("AT+POLAR=1,0");
      delay(500);
}
     
void loop() {}
```

此代码包含更改蓝牙HC-05 参数的几个函数：

    AT+NAME=Bluino#00 ：更改蓝牙模块名称，默认名称为“HC-05”。
    AT+BAUD=115200,0,0 : 将波特率更改为 115200 (Arduino  Uno、Bluino 和 Mega2560)
    AT+BAUD=57600,0,0 ：将波特率更改为 57600（Arduino Nano、Leonardo、Micro、Pro Mini 3V3/5V 和 Duemilanove）
    AT+POLAR=1,0 : 改变状态引脚条件
    另外，您可以在配对时更改密码以使用非标准密码，AT+PSWD=xxxx

***PS***:蓝牙名称必须为“Bluino#00-9999”，如果您想要自定义名称，则需要使用付费版的 Bluino Loader App

2、如下图连线

![](https://img.sevin.cn/i/2023/06/07/647fef331ac4f.png)

***PS***:注意连接在Arduino和蓝牙之间的电容器和电阻器。这些组件对于在草图上传完成后重置 Arduino 很重要

连接效果图：

![](http://img.sevin.cn/i/2023/06/07/647fef3307e50.jpg)

3、设置蓝牙 HC-05

这是在连接蓝牙模块到Arduino时运行上传到 Arduino 的代码的步骤

请仔细注意这一点。您需要使用这些步骤强制蓝牙模块进入AT命令模式

1. 按住 KEY 按钮
2. 插入 USB 电缆为 Arduino 供电
3. 等待大约 5 秒（仍然按住 KEY 按钮）
4. 拔下并重新插入 USB 以从 AT 命令模式重置

4、运行Bluino Loader

1. 打开软件，点击首选项（没看到就往右划调出菜单）>点击Board>勾选上面的“USB—BLUETOOTH”然后在下面选择你对应的板子>返回主页面>往右划调出菜单>点击新建文件
2. 在这里编写你想烧录到Arduino的程序，然后点击“上传”按钮（圆圈图标中的箭头）
3. 编译无误后，点击“Scan Bluino Hardware”按钮搜索蓝牙设备
4. 选择名称为“Bluino#00”的蓝牙硬件
5. 输入配对码标准“1234”，然后确定
6. 等到程序烧录完成 

现在，你可以用手机重复步骤“运行Bluino Loader”以编写和烧录程序到你的Arduino，而无需将其连接到电脑

***ps***:软件有串口功能，但是要付费使用，请自行研究

# 问题解答

1、烧录程序时软件显示error，烧录失败怎么回事？

这种情况多半是在烧录时的复位上出了问题，那就去掉HC-05上state端口连接的杜邦线和电容，在烧录（上传代码）的时候找准时机（大概是开始烧录后的1-2秒，多试几次就好）按下Arduino上的复位键进行手动复位。

# 留言

这是我发布的第一篇文章，部分图片来源于Bluino Loader官方，谢谢支持！

为了方便大家下载Bluino Loader，您可以到我的个人云盘里面下载：[我的云盘](https://cloud.sevin.cn)