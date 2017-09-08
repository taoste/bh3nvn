---
layout: post
title: 搭建KindleEar
date: 2017-07-04 11:36:36 +0800
categories:
- 日志
tags:
- kindle
- 读书
---

# 简介
这是一个运行在Google App Engine(GAE)上的Kindle个人推送服务应用，生成排版精美的杂志模式mobi/epub格式自动每天推送至您的Kindle或其他邮箱。

![](https://github.com/bh3nvn/bh3nvn.github.io/raw/master/image/2017/2017-07-04-01.png)

此应用目前的主要功能有：  

* 支持类似Calibre的recipe格式的不限量RSS/ATOM或网页内容收集
* 不限量自定义RSS，直接输入RSS/ATOM链接和标题即可自动推送
* 多账号管理，支持多用户和多Kindle
* 生成带图的杂志格式mobi或带图的有目录epub
* 自动每天定时推送
* 强大而且方便的邮件中转服务
* 和Evernote/Pocket/Instapaper等系统的集成

# 原作者的部署说明

[原作者的Gitbub](https://github.com/cdhigh/KindleEar/blob/master/readme.md)

# Google云端Shell部署步骤
  打开Google云端Shell，执行以下命令：    
  
    rm -f uploader.sh*    
    wget https://raw.githubusercontent.com/bh3nvn/KindleEar-Uploader/master/uploader.sh      
    chmod +x uploader.sh    
    ./uploader.sh    
    
  注意，上面的代码只需要执行一次即可，如果想要重新上传或要更新代码，只需要直接运行最后一行uploader.sh 这个 Shell 文件即可。
