---
title: Markdown Tutorial
date: 2016-09-18 15:20:00
tags: markdown
categories: 技术
---

Markdown是一种标记语言，通过简单的标记语法可以使文档具有一定的格式。

提到标记语言大家肯定会想到HTML，Markdown不是想取代HTML,也不是想模仿HTML，因为Markdown的语法只对应于HTML的一小部分，所以也不是想为了方便HTML的书写。它只是为了文档更容易读、写和随意改。

HTML是一种发布的格式，Markdown是一种书写的格式。



## Markdown语法
Markdown的语法非常的简单，基本语法如下：

### 1.标题设置
* 行首插入1~6个#，然后加一个空格再加标题内容，表示标题的深度1~6阶.
# This is H1
## This is H2
### This is H3
#### This is H4
##### This is H5
###### This is H6
* 在标题的下面添加三个“＝”或“－”(其中前者表示一级标题，后者表示二级标题)  


### 2.区块引用
* 使用“>”符号加内容，可以嵌套，嵌套层数由“>”个数决定。  
>这就是区块引用  
* ">"后加五个空格，区块背景会加深。  

* >     这个区块的背景被加深了。

### 3.强调字体
* 加粗(内容两端各加两个"\*")  
**粗体**
* 斜体(内容两端各加一个"\*")  
*斜体*

### 4.列表
有序列表(序号加英文句号)   
1. 橘子  
2. 牛奶  
3. 咖啡    

无序列表("*"或者“-”或者“+”后面加空格后再加内容)  
* 柠檬  
* 香蕉  
* 草莓  

### 5.超链接
* “[名称] (链接)” 实际名称和链接中间是没有空格的。这种方式叫做内联方式。  
[百度](http://www.baidu.com)  
[谷歌](http://www.google.com)  
[博主](http://www.zhs.space/about)  
* 引用方式  “\[名称]\[1] + \[1]: 链接”  
```
[Google][1], [Baidu][2]  
[1]: http://www.google.com
[2]: http://www.baidu.com  
```


### 6.图片  
直接引用图片:

	![图片名字，可以为空](/path/to/img.jpg)  
	![Alt text](/path/to/img.jpg "Optional title")  

参考式的图片:

	![alt text][1]  
	[1]: /users/blog/img/dog.jpg

说明：设置图片大小和居中的两种方法  
1）使用img标签
`<img src="/image/xxx.png" width = "300" height = "200" alt="图片名称" align=center />`
2）使用支持图片大小更改操作的 Mou 编辑器  
`![](./pic/pic1_50.png =100x100)`
注意： =前面有一个空格，这里大小就是100x100不是100*100
### 7.代码
一行代码，比如shell命令可以用"\`代码\`"  
`printf()`  
多行代码就在每行代码前加一个tab或者四个空格，  
或者只需要在代码开始和结束时各加三个"`"

```C
int main() {
	return 0;
}
```

### 8.脚注


> 此处有引文[^File]  
> [^File]: 《智能时代》  
> 效果就是跟论文的引文一样的效果，点击可以跳转。


### 9.分割线
* 每行文字后面加两个空格表示换行。
我这觉话说的够长了，我想换行了。  
换行成功了吗？
* 直接在一行文字后面空一行也表示这里空一行。
* 画水平线(HR): ------或者******或者======

## Markdown编辑器
* OSX  
Atom  
Byword  
[Mou](http://25.io/mou/)(博主目前使用的这款Mou0.8.7，但是Mou1.0要收费啦～)  
Mo
Typora  
MacDown(这款不错是免费的～)  
RStudio  
* Linux  
Atom  
ReText  
UberWriter  
RStudio  
* Windows  
Atom  
MarkdownPad  
Miu  
Typora  
RStudio  
* iOS  
Byword  
* 浏览器插件  
MaDo (Chrome)  
Marxico（Chrome)  
* 高级应用  
Sublime Text 2 + MarkdownEditing / 教程  

## 参考：  
[Markdown 11种基本语法](http://www.cnblogs.com/hnrainll/p/3514637.html)  
[Markdown 语法说明 (简体中文版)](http://www.appinn.com/markdown)  
[Markdown 指南](https://www.binarization.com/archives/www.wikimilk.org/markdown-guide/#help)
