---
layout: post
title: 	Raspberry Pi+PCM5102A+LCD1602+VOLUMIO 制作流媒体HiFi播放器
date: 2014-08-30 15:43:05
categories:
- 日志
tags:
- Raspberry Pi
- DIY
---

   
1、PCM1502A是TI公司高端DAC芯片，使用的是I2S接口，支持16至32位音频数据格式；支持高达384kHz的采样率，动态范围112dB，失真度-93Db。

成品可以选择HiFiberry.org或ukonline2000.com出品的成品PCBA。完全兼容Raspberry Pi。

2、烧录Volumio最新版本到RPi,在System中激活I2S驱动重启。

3、参考[https://learn.adafruit.com/drive-a-16x2-lcd-directly-with-a-raspberry-pi/overview](https://learn.adafruit.com/drive-a-16x2-lcd-directly-with-a-raspberry-pi/overview)连接LCD1602。我把背光加上三极管用RPi的IO口控制，开机之后背光点亮，关机之后背光熄灭。

安装rpi.gpio的时候注意，由于VOLUMIO采用了新的python版本，所以adafruit的方法会出现错误，因为新的python对老版本不兼容。

解决方法有两个，一个是把python降级，按照adafruit教程一步一步安装rpi.gpio。另外就是使用现有的python，直接安装，我采用的这个方式，比较简单：

    wget http://sourceforge.net/projects/raspberry-gpio-python/files/raspbian-wheezy/python-rpi.gpio_0.5.6-1_armhf.deb
    dpkg -i python-rpi.gpio_0.5.6-1_armhf.deb

4、按照自己需求改python源码内容，我的显示内容见最后图片。添加自启动脚本的时候如果报错，执行

    sudo update-rc.d lcd remove
    sudo update-rc.d lcd defaults

5、显示IP的代码部分，先判断wlan0再判断eth0，方便使用，显示中IP前边的字母E代表eth0，W代表wlan0。
禁用掉ipv6，在/boot/cmdline中添加：

    ipv6.disable=1
    
设置时区：

    dpkg-reconfigure tzdata

![](http://i1328.photobucket.com/albums/w532/xwlogic/IMG_20140830_151856720_zps031737da.jpg)

![](http://i1328.photobucket.com/albums/w532/xwlogic/IMG_20140830_151905146_zps2e1496b2.jpg)

![](http://i1328.photobucket.com/albums/w532/xwlogic/IMG_20140830_151938326_zpsff18dcc9.jpg)

![](http://i1328.photobucket.com/albums/w532/xwlogic/IMG_20140830_153405149_zps7a4c5bfc.jpg)

![](http://i1328.photobucket.com/albums/w532/xwlogic/IMG_20140830_153412445_zps9e409130.jpg)


