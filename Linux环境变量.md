---
title: Linux下环境变量设置
date: 2016-10-17 20:30
tags: Linux
categories: Linux
---

### 分类

Linux下的环境变量按生存周期来划分，可以划分为两种：

1)**永久的：**需要修改配置文件， 变量永久生效

2)**临时的：**直接在终端使用export命令声明即可，但是关闭shell后失效。
 
### 设置方法

#### 在/etc/profile中添加变量——即是全局的，对所有用户都生效（永久的）

``` bash
vim /etc/profile
export PATH=$PATH:/usr/local/bin:/usr/local/sbin
```

保存后，使设置生效： **source /etc/profile**

#### 在用户目录下的.bash_profile中添加变量——对当前用户有效(永久的)

``` bash
vim ~/.bash_profile
export PATH=$PATH:/User/zhonghuasong/JAVA/apache-tomcat-7.0.72/bin
```

保存后，使设置生效： **source ~/.bash_profile**

#### 直接在命令行中设置环境变量——临时的，关闭shell后即失效

``` bash
export PATH=$PATH:/User/zhonghuasong/JAVA/apache-tomcat-7.0.72/bin
```









