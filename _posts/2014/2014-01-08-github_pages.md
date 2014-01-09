---
author: xwlogic
date: 2014-01-08 11:40:22
layout: post
title: 使用Github Pages搭建个人主页
categories:
- 日志
tags:
- GitHub
---


### **前提** ###
要在GitHub上搭建博客，起码得有一个[GitHub](https://github.com)账号。
 

### **个人主页和项目主页** ###
个人主页：Github为每一个用户分配了一个二级域名`username.github.com`，用户为自己的二级域名创建主页很简单，只需要在Github下创建一个名为`username.github.com`的版本库，并向其master分支提交网站静态页面即可，其中网站首页为index.html。  
项目主页：为项目启用项目主页很简单，只需要在项目版本库中创建一个名为`gh-pages`的分支，并向其中添加静态网页即可，通过网址`http://username.github.com/helloworld`（假设项目名为helloworld）访问。  


### **使用Github Pages功能创建个人主页** ###
1. 登陆Github，创建一个名为`username.github.com`的版本库（注意将username替换成自己的Github账户名）。
2. 点击Setting，选择一个自己喜欢的模板，最后点击发布public按钮。
3. 耐心等待一段时间（不超过10分钟），登陆`http://username.github.com`，会发现自己的个人主页已经生成。


### **使用其他模板创建个人主页** ###
1. 克隆`username.github.com`版本库到本地  

		
2. 删除Github自动生成的文件,注意不要删除.git目录  

		cd username.github.com		
		git rm -r images/
		git rm -r index.html
		git rm -r javascripts/
		git rm -r params.json
		git rm -r stylesheets/
		git commit -m "remove default files"
		git push  
3. 下载别人的主页模板，然后删除其中的.git目录，然后将内容全部复制到自己的主页目录中  

4. 向Github提交修改后的主页  
		
		cd username.github.com
		git add .
		git commit -m "add blog files"
		git push

5. 耐心等待一段时间后，再次打开网址`http://username.github.com`看看主页变样了没~

6. 下面就用遵循Markdown的语法写blog吧，放到_posts文件夹下push到github就行了，github原生支持jekyll哦~


[参考博文][link-block-spec]
[link-block-spec]:http://hahaya.github.io/2013/06/26/build-blog-on-github.html



  
  
  


