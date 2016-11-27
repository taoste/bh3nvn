---
layout: post
title: Ubuntu 16.04安装chrome部署GAE
date: 2016-11-27 11:36:36 +0800
categories:
- 随笔
tags:
- 生活
- 数码
---

1、下载chrome最新版然后终端执行命令：sudo dpkg -i xxx.deb    

2、修复依赖关系：sudo apt-get install -f    

3、安装 libnss3-tools 包：sudo apt-get install libnss3-tools    

4、安装python-openssl：sudo apt-get install python-openssl    

5、修改xx/goagent3.0/local/packages.egg/linux/gevent/ssl.py的line 386    
- def get_server_certificate(addr, ssl_version=PROTOCOL_SSLv3, ca_certs=None)        
+ def get_server_certificate(addr, ssl_version=PROTOCOL_TLSv1, ca_certs=None)    
原因：SSLv3协议由于设计缺陷已经被python禁用，可以使用TLSv1协议代替        

6、下载最新的SwitchyOmega，将其直接拖拽到浏览器的“扩展程序”（chrome://chrome/extensions/）页面安装    

7、在SwitchyOmega中导入GAE的备份文件SwitchyOptions.bak    

8、导入GAE的证书：certutil -d sql:$HOME/.pki/nssdb -A -t TC -n "goagent" -i ~/GAE/goagent-3.0/local/CA.crt     

9、运行gae：sudo python proxy.py    

10、enjoy～

  	
