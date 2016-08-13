---
layout: post
title: 制作 QRP Z-Match 天调
date: 2016-08-12 12:36:36 +0800
categories:
- 日志
tags:
- 无线电
- DIY
---

Z-Macth天调在国外已经流行很久了，国内很少看到有人使用，最近看了很多Z-Match天调的文章，计划仿制一个。    
Z-Match的特点如下（From WB3GCK.）：    

Why the popularity? Here are some advantages that the Z-match design offers:    
● Matches balanced loads without the use of lossy baluns.    
●Being a parallel resonant circuit, the Z-match can provide some band-pass filtering for your receiver and harmonic attenuation for your transmitter.    
●A well-designed Z-match tuner has a high Q and is more efficient (less lossy) than other types of tuners.    
●The fixed inductor simplifies construction (no taps or rollers needed).    
●Using a toroid inductor and some small poly film variable capacitors, the Z-match can be built into a very compact package. This sort of thing usually appeals to QRPers.    

There is, of course, no free lunch here. Here are some disadvantages of the Z-match design:    
●Tuning is usually very narrow and can be a bit touchy sometimes to tune up.    
●The range of impedances that can be matched is not as great as in other designs, such as the "T" configuration.    

按照下图，目标是QRP，体积越小越好，电容使用收音机的270p双联可调电容，原来大都使用T130-2或者T130-6磁环，我手里只有T50-6，所以重新计算了匝数，输出端加上PD7MAA的简单调谐指示器。    
![](https://github.com/bh3nvn/bh3nvn.github.io/raw/master/image/2016/2016-08-12-01.jpg)     	

制作完成之后的样子，三围80x60x35mm。左边的电容是TUNING，右边是COUPLING，左上角钮子开关打到上边是平衡输出，打到下边是不平衡输出，右上角的指示灯在调谐匹配时候最亮。    
![](https://github.com/bh3nvn/bh3nvn.github.io/raw/master/image/2016/2016-08-12-02.jpg)     		

接上Ultimate3 0.5瓦发射，天调输出接10米长线，输出如下：    
![](https://github.com/bh3nvn/bh3nvn.github.io/raw/master/image/2016/2016-08-12-03.jpg)     		

经过对比，比端馈的LC匹配天调效率高很多。


