---
title: Scrapy Tutorial
date: 2016-09-22 20:00:00
tags: scrapy
categories: 技术
---

### 1. 安装Scrapy包
* pip install scrapy, [安装教程](http://doc.scrapy.org/en/1.1/intro/install.html#intro-install)
* Mac下可能会出现：OSError: [Errno 13] Permission denied: '/Library/Python/2.7/site-packages/pyasn1'
* 应该是权限问题，解决方案：sudo pip install scrapy

### 2. 使用教程
##### 1. 创建一个Scrapy工程
`scrapy startproject tutorial`

```Python   
tutorial/
   
   scrapy.cfg            # 配置文件
   
   tutorial/             # 工程的python模块，你将从这里引入你的代码
   __init__.py

   items.py          # 工程的项目文件

   pipelines.py      # 工程的流水线文件

   settings.py       # 工程的设置文件

   spiders/          # 你将安放爬虫程序的目录
    __init__.py
```




##### 2. 定义Item
* Items是将要被爬虫数据加载的容器，工作方式类似于Python的字典(dict)，在Scrapy中，也可以使用原生的Python字典，但是Iterms提供了一些额外的保护机制防止写未申明的域和防止拼写错误。
* 创建一个scrapy.Item类，然后定义它的属性scrapy.Field(),类似于ORM(关系对象模型)
* 爬[quotes.toscrape.com](quotes.toscrape.com)中的文本和作者为例，在items.py中编辑如下代码：


```Python
import scrapy

class QuoteItem(scrapy.Item):
    text = scrapy.Field()
    author = scrapy.Field()
```

##### 3. 定义爬虫程序
创建一个爬虫，首先要继承scrapy.Spider，并且定义一些属性:  

* name: 定义这个爬虫的名字，在同一个工程中必须是唯一的。
* start_urls: 开始爬虫的url列表
* parse(): 定义爬虫的方法，也叫做下载每个url的响应(Response)对象，response作为此方法第一个也是唯一一个参数。 此方法的主要作用是：解析响应数据和提取爬取数据中更多的url
* 在spiders目录中创建quotes_spider.py文件，并编写以下代码:

```Python
import scrapy


class QuotesSpider(scrapy.Spider):
    name = "quotes"
    start_urls = [
        'http://quotes.toscrape.com/page/1/',
        'http://quotes.toscrape.com/page/2/',
    ]

    def parse(self, response):
        filename = 'quotes-' + response.url.split("/")[-2] + '.html'
        with open(filename, 'wb') as f:
            f.write(response.body)
```

##### 4. 开始爬虫
在工程的顶层目录执行以下命令：

`scrapy crawl quotes`

解释过程：其实是对start_urls中的链接进行http请求，然后对请求的结果进行解析，也就是执行parse()函数。

##### 5. 提取其中的Item

**(1). 引入选择器(Selectors)**  
有许多方法从web页面中提取数据，Scrapy采用的是一种基于XPath和CSS表达式的机制，叫做Scrapy Selector。 
以下是几个XPath的表达式及其含义： 

* /html/head/title : 从html标签中的head标签中选择title元素， 等价的CSS选择器： html > head > title
* /html/head/title/text() : 选择title中的text， 等价的CSS选择器：html > head > title ::text
* //td : 从文档中选择所有的<td>元素， 等价的CSS选择器： td
* //div[@class="mine"] : 选择一个包含属性 class="mine"的div， 等价的CSS选择器： div.mine, @表示属性

**CSS VS XPath**： 提取数据可以只用CSS选择器，但是XPath的功能更加强大，因为除了可以定位结构以外，它还可以查询内容，例如选择那些链接内容中包含"Next Page"的链接。所以鼓励使用XPath。  
为了方便CSS和XPath的表达，Scrapy提供了Selector类和方便的快捷键来避免当每次从响应中选择某些文本时候都自己写选择器。  
你可以将选择器看作是文档结构中表示节点的对象。所以第一个需要写的选择器是和根节点有关的。  
选择器有以下四个基本的方法：  

* xpath(): 返回一个选择器列表，每一个都表示xpath表达式作为参数选择的节点。
* css(): 返回一个选择列表，同上。
* extract(): 返回选择数据的统一编码字符串。
* re(): 返回一个利用正则表达式作为参数所提取的统一编码的字符串的列表。

**(2). 在shell中尝试选择器**  
好处就是可以直接得到一个response变量，然后可以直接执行一些选择器即可看到响应的结果，例如：  
`scrapy shell "http://quotes.toscrape.com"`  (链接一定要用引号引起来)

```Python
[ ... Scrapy log here ... ]

2016-09-01 18:14:39 [scrapy] DEBUG: Crawled (200) <GET http://quotes.toscrape.com> (referer: None)
[s] Available Scrapy objects:
[s]   crawler    <scrapy.crawler.Crawler object at 0x109001c90>
[s]   item       {}
[s]   request    <GET http://quotes.toscrape.com>
[s]   response   <200 http://quotes.toscrape.com>
[s]   settings   <scrapy.settings.Settings object at 0x109001610>
[s]   spider     <DefaultSpider 'default' at 0x1092808d0>
[s] Useful shortcuts:
[s]   shelp()           Shell help (print this help)
[s]   fetch(req_or_url) Fetch request (or URL) and update local objects
[s]   view(response)    View response in a browser

 >>>

In [1]: response.xpath('//title')
Out[1]: [<Selector xpath='//title' data=u'<title>Quotes to Scrape</title>'>]

In [2]: response.xpath('//title').extract()
Out[2]: [u'<title>Quotes to Scrape</title>']

In [3]: response.xpath('//title/text()')
Out[3]: [<Selector xpath='//title/text()' data=u'Quotes to Scrape'>]

In [4]: response.xpath('//title/text()').extract()
Out[4]: [u'Quotes to Scrape']

In [11]: response.xpath('//title/text()').re('(\w+)')
Out[11]: [u'Quotes', u'to', u'Scrape']
```

**(3). 提取数据**

代码如下：  

```Python
import scrapy

class QuotesSpider(scrapy.Spider):
    name = "quotes"
    start_urls = [
        "http://quotes.toscrape.com/page/1/",
        "http://quotes.toscrape.com/page/2/",
    ]

    def parse(self, response):
        for quote in response.xpath('//div[@class="quote"]'):
            text = quote.xpath('span[@class="text"]/text()').extract_first()
            author = quote.xpath('span/small/text()').extract_first()
            print(u'{}: {}'.format(author, text))
```


**(4). 利用我们的Item**

代码如下：

```Python
import scrapy
from tutorial.items import QuoteItem


class QuotesSpider(scrapy.Spider):
    name = "quotes"
    start_urls = [
        'http://quotes.toscrape.com/page/1/',
        'http://quotes.toscrape.com/page/2/',
    ]

    def parse(self, response):
        for quote in response.xpath('//div[@class="quote"]'):
            item = QuoteItem()
            item['text'] = quote.xpath('span[@class="text"]/text()').extract_first()
            item['author'] = quote.xpath('span/small/text()').extract_first()
            yield item
```

**(5). 跟踪链接**

代码如下：

```Python
import scrapy
from tutorial.items import QuoteItem


class QuotesSpider(scrapy.Spider):
    name = "quotes"
    start_urls = [
        'http://quotes.toscrape.com/page/1/',
    ]

    def parse(self, response):
        for quote in response.xpath('//div[@class="quote"]'):
            item = QuoteItem()
            item['text'] = quote.xpath('span[@class="text"]/text()').extract_first()
            item['author'] = quote.xpath('span/small/text()').extract_first()
            yield item
        next_page = response.xpath('//li[@class="next"]/a/@href').extract_first()
        if next_page:
            next_page = response.urljoin(next_page)
            yield scrapy.Request(next_page, callback=self.parse)
```

**(6). 存储爬到的数据**

`scrapy crawl quotes -o items.json`

将产生items.json文件，并且是JSON格式的数据。  
在大的项目中，可能需要写Item Pipeline.
