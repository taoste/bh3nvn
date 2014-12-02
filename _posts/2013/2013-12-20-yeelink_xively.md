---
layout: post
title: yeelink/xively环境节点搭建@RPi
date: 2013-12-20 08:43:05
categories:
- 日志
tags:
- 物联网
- Raspberry Pi
---

### **监测项目** ###
1. PM2.5瞬时值
2. PM2.5一小时均值
3. 温度
4. 湿度

由于RPi没有Ad输入口，所以用DAQ-106PM2.5监测表改装后通过urat把数据发送给RPi。

RPi系统版本：2013-05-25-wheezy-raspbian

DAQ-106改动主要是为了让出uart tx引脚，加上电平转换电路接入RPi的rx。

**1、升级系统**

    sudo apt-get update

**2、配置RPi的uart**

修改inittab

    sudo nano /etc/inittab

注释掉T0:23:respawn:/sbin/getty -L ttyAMA0 115200 vt100

    #T0:23:respawn:/sbin/getty -L ttyAMA0 115200 vt100
修改cmdline.txt 

    sudo  nano /boot/cmdline.txt 
删除Remove  console=ttyAMA0,115200 kgdboc=ttyAMA0,115200字段

重启
    
    sudo reboot

**3、安装minicon和python-serial**

    sudo apt-get install minicom
    sudo apt-get install python-serial
uart测试：

    minicom -b 9600 -o -D /dev/ttyAMA0
连上DAQ-106，如果有数据打印出来，表明uart通讯正常。

**4、因为需要数据频繁读写，所以在内存里边开辟个区域用来存放中间文件**

先在/mnt下建个临时文件夹

    sudo mkdir /mnt/tmp
然后把开辟的内存区域挂在到这里，完成后可以使用df命令查看

    sudo mount -t tmpfs -o size=5m  tmpfs /mnt/tmp

配置fstab文件，增加一行，使以上工作开机生效

    tmpfs /mnt/tmp tmpfs size=5m 0 0

**5、创建相关文件**

先在~目录下创建个pm25文件夹

    mkdir /home/pi/pm25

切换到这个文件夹

    cd pm25
创建文件

    nano pm25.py

输入以下内容

    import serial
    ser=serial.Serial('/dev/ttyAMA0',9600,timeout=20)
    ser.open()
    data=ser.readline()
    ser.close()
    s=data.split(" ")[0]
    c=data.split(" ")[2]
    h=data.split(" ")[4]
    k=data.split(" ")[6]
    if s=="s":
      if c=="c":
       if h=="h":
         if k=="k":
          pm25=data.split(" ")[1]
          pm251h=data.split(" ")[3]
          temp=data.split(" ")[5]
          rh=data.split(" ")[7]
          pm25=int(pm25)
          res='{"value":%d}' %pm25
          output=open('/mnt/tmp/datapm25.txt','w')
          output.write(res)
          output.close

          pm251h=int(pm251h)
          res='{"value":%d}' %pm251h
          output=open('/mnt/tmp/datapm251h.txt','w')
          output.write(res)
          output.close
  
          temp=int(temp)
          res='{"value":%d}' %temp
          output=open('/mnt/tmp/datatemp.txt','w')
          output.write(res)
          output.close
  
          rh=int(rh)
          res='{"value":%d}' %rh
          output=open('/mnt/tmp/datarh.txt','w')
          output.write(res)
          output.close

s、c、h、k用来简单校验通信数据。txt文件是按照yeelink的api接口要求保存json格式的数据。

把pm25.py拷贝到/mnt/tmp/下运行一下试试，应该生成相关的数据记录文件。

    cp pm25.py /mnt/tmp
    cd /mnt/tmp
    python pm25.py
    ls
没问题，下一步

**6、创建脚本，实现自动调用**

在~/pm25目录下创建个sh文件，调用pm25.py并把数据通过curl发送给yeelink服务器

    nano yeelink.sh

输入以下内容
  
    sudo python /mnt/tmp/pm25.py
    curl --request POST --data-binary @"/mnt/tmp/datapm25.txt" --header "U-ApiKey:你的ApiKey" http://api.yeelink.net/v1.0/device/你的设备id/sensor/你的传感器编号/datapoints
依次把各个数据文件按照上面格式写入yeelink.sh,

给脚本加上执行权限

     chmod +x yeelink.sh

并把文教拷贝到/mnt/tmp/下

    cp yeelink.sh /mnt/tmp
    cd /mnt/tmp

执行以下试试看

    ./yeelink.sh

打开你的yeelink看看，是不是有数据上去了~~~

修改rc.local文件，开机时候自动把pm25文件件下的文件拷贝到/mnt/tmp下

    sudo nano /etc/rc.local

在exit 0这行之上写上

    sudo cp /home/pi/pm25/*.* /mnt/tmp/


修改crontab实现每分钟调用一次，上传一组数据

    sudo crontab -e
添加
    
    */01 * * * * /mnt/tmp/yeelink.sh

如果要上传数据到xively，只要修改pm25.py文件，按照xively的要求保存json格式为文件，然后编写xively相应的sh文件即可。

我的环境节点@yeelink：[http://www.yeelink.net/devices/6692#](http://www.yeelink.net/devices/6692# "yeelink")

我的环境节点@xively：[https://xively.com/feeds/291868862](https://xively.com/feeds/291868862 "xively")
