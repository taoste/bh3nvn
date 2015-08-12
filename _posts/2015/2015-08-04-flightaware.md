---
layout: post
title: 	FlightAware走起
date: 2015-08-04 12:43:05
categories:
- 日志
tags:
- 无线电
- Raspberry Pi
- Flight
---

闲置的树莓派1代+闲置的RTL-SDR组成了一个PiAware，获得FlightAware的企业账号，也申请了FlightFeeder。。。     
[flightaware.com](http://flightaware.com/)

![](http://i1328.photobucket.com/albums/w532/xwlogic/IMG_20150804_140625987_HDR_zpsc3o0gbyo.jpg)    
![](http://i1328.photobucket.com/albums/w532/xwlogic/1_zpsvoqbm0j9.jpg)    
![](http://i1328.photobucket.com/albums/w532/xwlogic/flightfeeder-v5-500px_zps9kffdhsb.jpg)    

另外，以用户名pi登录ssh登录密码是flightaware，添加了WiFi网卡，省了一条网线。

    sudo nano /etc/wpa_supplicant/wpa_supplicant.conf
    
添加以下代码

    network={
            ssid="Marc0 DD-WRT@WRT54G v4"
            psk="password"
            proto=RSN
            key_mgmt=WPA-PSK
            pairwise=CCMP
            auth_alg=OPEN
    }
  
*** 8月7日更新： ***

可以在PiAware的系统上，按照Plane Finder的教程，安装其客户端，实现一个RPi同时Feed FW和PF，注意要使用RPi2代，一代版本经测试，跑不起来。

![](http://i1328.photobucket.com/albums/w532/xwlogic/_zps8xtk6gsm.jpg)    

Stuff    
![](http://i1328.photobucket.com/albums/w532/xwlogic/IMG_20150807_135645986_HDR_zpsolcy9ixv.jpg)

