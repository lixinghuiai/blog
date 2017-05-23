---
title: 向GitHub的第一次提交
date: 2017-05-23 09:47:28
categories: git 
tags:
---
# 向GitHub的第一次提交
#### 加载文件
首先将要托管的项目放入上图所在的目录（即有.git文件夹和.gitignore所在目录）当中，执行
> git add . 

. 是把文件夹里面的所有文件都加载进来,也可以进行单个加载，如下：
> git add README.md,index.html

提交文件，创建时间点
> git commit -m "init commit"

上面的意思是提交文件先到本地仓库，同时添加注释“init commit”,可以随时用
> git status

上面git commit命令执行完成后界面如下图：
![](http://upload-images.jianshu.io/upload_images/1685562-ac4668b5bfdd527d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#### 添加远程主机
> $ git remote add <主机名> <URL地址>

克隆版本库的时候，所使用的远程主机自动被Git命名为origin。origin可变，随自己添加时命名，关于Git远程操作详情请参：Git远程操作详解

添加成功后如下图：
![](http://upload-images.jianshu.io/upload_images/1685562-8258aa25156b8aa1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
#### 推送代码：
> $git push origin master
