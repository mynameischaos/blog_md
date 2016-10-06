---
title: CLion下的相对路径
date: 2016-10-3 22:44:00
tags: CLion
categories: CLion
---

**问题描述：**  
在CLion下用C++实现读文件，将要读的文件和程序源文件放到了同一个目录下，于是乎就干脆的使用了相对路径。读取文件时候发现读取是乱码的，返回也是不对的。那是因为默认CLion是没有设置工作目录的(我以为工作目录默认是源程序所在目录)。  
**解决办法：**  
Run->Edit Configurations->Working directory 下设置工作目录(一般设置为源程序所在目录)。