---
layout: post
title: Raspberry Pi设置看门狗
date: 2013-08-10 08:43:05
categories:
- 日志
tags:
- Raspberry Pi
---

**安装软件**

    sudo modprobe bcm2708_wdog
    echo "bcm2708_wdog" | sudo tee -a /etc/modules
    sudo apt-get install watchdog
    sudo update-rc.d watchdog defaults

**修改配置**

    sudo nano /etc/watchdog.conf

- 取消掉 watchdog-device = /dev/watchdog 前的注释#号，让他监控的设备指向CPU的硬件看门狗；
- 取消掉 max-load-1 = 24 前的注释#号，当1分钟load进程超过24个的时候就触发重启
- 制定温度配置文件temperature-device = /sys/class/thermal/thermal_zone0/temp
- 设置最高温度max-temperature = 75000
- 还可以设置内存耗尽就重启，如min-memory =1 前的注释#号去掉
- 还可以设置监控的间隔，如 interval = 1 前的注释#号去掉，该1为任意数字，单位是秒，默认是10秒一次监测

**开启服务**

    sudo /etc/init.d/watchdog start

**查看看门狗状态**

    /etc/init.d/watchdog status

**测试**

输入下边代码，Pi会立即崩溃，十秒后重启
    
    : (){ :|:& };:

