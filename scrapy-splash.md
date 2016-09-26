---
title: 利用scrapy-splash爬取JS生成的动态页面
date: 2016-09-24 12:07:00
tags: scrapy
categories: scrapy
---

目前，为了加速页面的加载速度，页面的很多部分都是用JS生成的，而对于用scrapy爬虫来说就是一个很大的问题，因为scrapy没有JS engine，所以爬取的都是静态页面，对于JS生成的动态页面都无法获得。  

**解决方案：**  

* 利用第三方中间件来提供JS渲染服务： [scrapy-splash](https://github.com/scrapy-plugins/scrapy-splash) 等。
* 利用webkit或者基于webkit库

 

**Splash是一个Javascript渲染服务。它是一个实现了HTTP API的轻量级浏览器，Splash是用Python实现的，同时使用Twisted和QT。Twisted（QT）用来让服务具有异步处理能力，以发挥webkit的并发能力。**  

--------------

下面就来讲一下如何使用scrapy-splash：  

1. 利用pip安装scrapy-splash库：  
    `$ pip install scrapy-splash`
2. scrapy-splash使用的是Splash HTTP API， 所以需要一个splash instance，一般采用docker运行splash，所以需要安装[docker](http://splash.readthedocs.io/en/latest/install.html)。  
3. 安装[docker](https://www.docker.com/), 安装好后运行docker。
4. 拉取镜像(pull the image)：  
`$ docker pull scrapinghub/splash`
5. 用docker运行scrapinghub/splash：  
`$ docker run -p 8050:8050 scrapinghub/splash`
6. 配置splash服务（以下操作全部在settings.py）：  

	1）添加splash服务器地址： 
	
	```python
	SPLASH_URL = 'http://localhost:8050'  
	```
	2）将splash middleware添加到DOWNLOADER_MIDDLEWARE中：  
	
	```python
	DOWNLOADER_MIDDLEWARES = {
    'scrapy_splash.SplashCookiesMiddleware': 723,
    'scrapy_splash.SplashMiddleware': 725,
    'scrapy.downloadermiddlewares.httpcompression.HttpCompressionMiddleware': 810,
	}
	```
	3)Enable SplashDeduplicateArgsMiddleware:  
	
	```python
	SPIDER_MIDDLEWARES = {
    'scrapy_splash.SplashDeduplicateArgsMiddleware': 100,
	}
	```
	4)Set a custom DUPEFILTER_CLASS:  
	
	```python
	DUPEFILTER_CLASS = 'scrapy_splash.SplashAwareDupeFilter'
	```
	5)a custom cache storage backend:  
	
	```python
	HTTPCACHE_STORAGE = 'scrapy_splash.SplashAwareFSCacheStorage'
	```
	
	
7. 例子  
获取HTML内容：  

```Python
import scrapy
from scrapy_splash import SplashRequest

class MySpider(scrapy.Spider):
    start_urls = ["http://example.com", "http://example.com/foo"]

    def start_requests(self):
        for url in self.start_urls:
            yield SplashRequest(url, self.parse, args={'wait': 0.5})

    def parse(self, response):
        # response.body is a result of render.html call; it
        # contains HTML processed by a browser.
        # ...        
```

参考链接：  
[scrapy_splash教程](https://github.com/scrapy-plugins/scrapy-splash)  
[Scrapy爬虫中使用Splash处理页面JS](http://ae.yyuap.com/pages/viewpage.action?pageId=919763)
