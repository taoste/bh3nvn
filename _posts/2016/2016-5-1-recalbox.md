---
layout: post
title: 树莓派变身模拟器--Recalbox
date: 2016-05-01 08:36:36 +0800
categories:
- 日志
tags:
- 游戏
- Raspberry Pi
---

树莓派上的模拟器，对比了recalbox、retropie和lakka之后，最终选择了recalbox。
下载了recalbox镜像之后复制到SD卡（不用Win32DiskImager写入），插入树莓派，会自动安装系统。    
安装重启后，通过SSH登录进行配置，用户名：root，密码：recalboxroot    
文件系统默认是只读的，需要重新挂在成可读写文件系统：

    mount -o remount, rw /boot 
    
编辑启动配置文件：

    nano /boot/config.txt 
    
![](http://i1328.photobucket.com/albums/w532/xwlogic/_zpswet0o9i6.jpg)

通过网络访问recalbox的共享文件\\RECALBOX\share\system\recalbox.conf,使用UltraEdit进行编辑：    
主要是关闭kodi系统，设置无线路由密码、语言、时区等，我的电视是SONY 55W800B，FullHD，所以设置global.videomode=CEA 5 HDMI
支持各类游戏手柄，中文游戏名称，赶紧重温经典吧！

![](http://i1328.photobucket.com/albums/w532/xwlogic/IMG_20160426_223301746_HDR_zpsapfgiqug.jpg)
![](http://i1328.photobucket.com/albums/w532/xwlogic/IMG_20160426_223324844_zps8ylcn1zp.jpg)
![](http://i1328.photobucket.com/albums/w532/xwlogic/IMG_20160426_223334248_zpsoilkf7qb.jpg)
![](http://i1328.photobucket.com/albums/w532/xwlogic/IMG_20160426_223343508_zpsnwniqjxg.jpg)
![](http://i1328.photobucket.com/albums/w532/xwlogic/IMG_20160426_223351094_zpsl9mggwlc.jpg)
![](http://i1328.photobucket.com/albums/w532/xwlogic/IMG_20160426_223416751_HDR_zpsyz6krg6z.jpg)
![](http://i1328.photobucket.com/albums/w532/xwlogic/IMG_20160426_223528475_zpsamx45wuz.jpg)
![](http://i1328.photobucket.com/albums/w532/xwlogic/IMG_20160426_223653920_zpswbhncf4w.jpg)
![](http://i1328.photobucket.com/albums/w532/xwlogic/IMG_20160426_223756690_zpskulymakn.jpg)

