---
layout: post
title: 	FlightAware走起
date: 2015-08-04 12:43:05
categories:
- 日志
tags:
- 无线电
- Raspberry Pi
---

闲置的树莓派1代+闲置的RTL-SDR组成了一个PiAware，获得FlightAware的企业账号，也申请了FlightFeeder。。。 
网址：![http://zh.flightaware.com/](http://zh.flightaware.com/)

![](http://i1328.photobucket.com/albums/w532/xwlogic/IMG_20150804_140625987_HDR_zpsc3o0gbyo.jpg)    
![](http://i1328.photobucket.com/albums/w532/xwlogic/1_zpsvoqbm0j9.jpg)    
![](http://i1328.photobucket.com/albums/w532/xwlogic/flightfeeder-v5-500px_zps9kffdhsb.jpg)    

另外，猜出了官方PiAware的ssh登录密码，添加了WiFi网卡，省了一条网线。

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
  
  
