---
title: git基本命令
date: 2016-09-22 21:26:00
tags: git
categories: 技术
---

1. 创建一个新的repository:  
在github上New一个repo，并且写好相应的名字(Repository name)和描述(Description)，然后选择Create repository。假设repo名字叫做MyTest.  
$cd ~/Test   //切换到Test目录  
$git init    //初始化git仓库  
$echo "# MyTest" >> README.md   //写一些README信息  
$git add .   //把所有文件加入到索引  
$git commit -m "your commit information"  //提交到本地仓库，以及更新日志信息  
$git remote add origin https://github.com/mynameischaos/MyTest.git   //添加远程仓库  
$git push -u origin master   //将本地仓库提交到远程仓库  
然后输入账号和密码即可。

-------
更新中
