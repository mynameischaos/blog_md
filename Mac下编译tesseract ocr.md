---
title: Mac编译tesseract ocr
date: 2016-10-16 10:25:00
tags: OCR
categories: OCR
---

### Tesseract OCR

Tesseract提供了非常好的OCR engine(光学字符识别引擎)。Tesseract从1985年就开始开发了，2006年后就由Google接手继续开发了。目前支持的语言已经超过100种了，而且还可以进一步训练以支持新的语言。开发者可以利用提供的C和C++ API来开发自己的应用。 该程序已经开源了。[Tesseract](https://github.com/tesseract-ocr/tesseract)

### Max OS X下安装

#### Homebrew安装Tesseract

``` bash
brew install tesseract
```

#### MacPorts安装（如果MacPorts不会安装，请参考之前博客[MacPorts](http://zhs.space/2016/10/15/Mac%E4%B8%8B%E5%AE%89%E8%A3%85MacPorts/)）

```bash
sudo port install tesseract
```

#### 安装语言包（[语言包编码格式](https://github.com/tesseract-ocr/tesseract/blob/master/doc/tesseract.1.asc#languages)）

```bash
sudo port install tesseract-<langcode>
```
注：也可以直接下载语言包，放到：/usr/local/share/tessdata目录下即可。

#### 更多系统安装请查看[安装](https://github.com/tesseract-ocr/tesseract/wiki)

### Tesseract编译

有的时候你会觉得以上用起还不爽，想自己看看源代码，改改源代码，想自己编译一下tesseract程序。

#### OS X with MacPorts

##### 安装所需要的包

```bash
sudo port install automake autoconf
sudo port install pkgconfig
sudo port install leptonica
sudo port install libtool
```

##### 编译以及安装

```bash
git clone git@github.com:tesseract-ocr/tesseract.git
cd tesseract
./autogen.sh
./configure --with-extra-libraries=/opt/local/lib
make
sudo make install
```

##### 安装带训练工具的tesseract

安装所需要的包：

```bash
sudo port install cairo pango 
sudo port install icu +devel
```

编译以及安装：

```bash
git clone https://github.com/tesseract-ocr/tesseract/
cd tesseract
./autogen.sh
./configure \
    --with-extra-libraries=/opt/local/lib \
    --with-extra-includes=/opt/local/include \
    LDFLAGS=-L/opt/local/lib \
    CPPFLAGS=-I/opt/local/include
make
sudo make install

make training
sudo make training-install

```


### 参考链接

[Tesseract官网](https://github.com/tesseract-ocr/tesseract)
