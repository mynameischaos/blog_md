---
title: git push免输入账号和密码方法
date: 2016-10-5 23:36
tags: git
categories: git
---

最近在做些oj，所以需要频繁的git push提交代码，每次都要输入帐号和密码，感觉不舒服，于是乎就做了如下设置，然后就可以开心的提交啦～

### Linux或者Mac下方法：

1. 创建文件，进入文件，输入内容：
```bash
cd ~
touch .git-credentials
vim .git-credentials
https://{username}:{password}@github.com
```

2. 在终端下输入：
```bash
git config --global credential.helper store
```

3. 打开~/.gitconfig文件，会发现多了一项:
```bash
[credential]
    helper = store
```

### Windows方法：
1. 方法同上面，只是第一步创建git-credentials有点不同。在%HOME%目录中，一般为C:\users\Administrator，也可以是你自己创建的系统用户名目录，反正都在C:\users\中。文件名为.git-credentials,由于在Window中不允许直接创建以"."开头的文件，所以需要借助git bash进行，打开git bash客户端，进行%HOME%目录，然后用touch创建文件 .git-credentials, 然后后面的操作同上面。
2. 还有一种方法参考[Windows下设置git push免密码](http://www.cnblogs.com/ballwql/p/3462104.html)。


#### 参考文献:
[git push时候总提示输入账号密码 - 免除设置](http://blog.csdn.net/kevinew/article/details/24588123/)  
[Windows下设置git push免密码](http://www.cnblogs.com/ballwql/p/3462104.html)