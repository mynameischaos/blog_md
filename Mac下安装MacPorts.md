---
title: Mac下安装MacPorts
date: 2016-10-15 16:56:00
tags: Tools
categories: Tools
---


### 什么是MacPorts

Mac下，我们经常用dmg、pkg， 或者homebrew来安装软件， 除此以外，MacPorts也是比较方便的来帮助你安装程序，跟BSD中的ports道理一样。MacPorts就像apt-get、yum、brew一样，可以快速安装软件。

MacPorts是开源社区发起的一项方便开发者在shell下进行编译、安装和升级等操作的开源项目，旨在方便Mac环境下de开发者。更多请看：[官网](http://www.macports.org)。

下面讲一下两种安装方法：

### 安装MacPorts（1）

1. 下载MacPorts, [下载地址](https://www.macports.org/install.php)， 在链接中下载符合自己系统版本的软件即可。 下载好后无脑下一步即可～

2. 设置环境变量，才好在shell中任何一个路径下使用port命令。
	
	* vim ~/.profile
	* 最后一行添加：export PATH=/opt/local/bin:/opt/local/sbin:$PATH  
	* 使～/.profile更新的生效：source ~/.profile
	
### 安装MacPorts（2）

通过源代码安装MacPorts， 参考[Mac OS X中MacPorts安装和使用](http://www.ccvita.com/434.html)

### 使用MacPorts

常用命令：

(1) 搜索MacPorts索引中的软件

``` bash
port search NAME
```

(2) 安装新的软件

``` bash
sudo port install NAME
```

(3) 卸载已经安装的软件 

```bash
sudo port uninstall NAME
```

(4) 查看版本较低的软件

``` bash
port outdated
```

(5) 升级版本较低的软件

``` bash
sudo port upgrade outdated
```

(6) 使用示例
 
``` bash
sudo port install wget
```



### 参考链接

[http://www.ccvita.com/434.html](http://www.ccvita.com/434.html)

[http://www.linuxidc.com/Linux/2012-01/52111.htm](http://www.linuxidc.com/Linux/2012-01/52111.htm)

[https://www.macports.org/install.php](https://www.macports.org/install.php)