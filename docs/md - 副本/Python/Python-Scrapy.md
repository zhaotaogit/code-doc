# Python-Scrapy

## 1.安装依赖

```shell
pip install twisted
pip install pywin32
pip install scrapy
```

再控制台输入Scrapy，出现如下效果即为安装正确：

![image-20211123152712806](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Blog_img/image-20211123152712806.png)

## 2.创建一个工程

```shell
scrapy startproject 工程名
```

目录结构：

![image-20211123153042880](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Blog_img/image-20211123153042880.png)

```
scrapy.cfg     # Scrapy 部署时的配置文件
tutorial         # 项目的模块，引入的时候需要从这里引入
    __init__.py    
    items.py     # Items 的定义，定义爬取的数据结构
    middlewares.py   # Middlewares 的定义，定义爬取时的中间件
    pipelines.py       # Pipelines 的定义，定义数据管道
    settings.py       # 配置文件
    spiders         # 放置 Spiders 的文件夹
    __init__.py
```

## 3.创建一个爬虫文件

进入工程目录

在spiders子目录中创建一个爬虫文件

```shell
scrapy genspider spiderName 域名
```

例：

```shell
scrapy genspider first www.baidu.com
Created spider 'first' using template 'basic' in module:
  FirstBoold.spiders.first
```

![image-20211123153509605](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Blog_img/image-20211123153509605.png)

这样就创建了一个爬虫文件

![image-20211123153556662](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Blog_img/image-20211123153556662.png)

## 4.执行工程

```shell
scrapy crawl spiderName
```

## 5.爬虫文件内容解析

```python
import scrapy


class FirstSpider(scrapy.Spider):
    # 爬虫文件的名称：爬虫源文件的唯一标识
    name = 'first'
    # 允许的域名：用来限定start_urls列表中那些url可以被请求发送
    allowed_domains = ['www.baidu.com']
    # 起始的url列表：该列表中存放的url会被scrapy自动进行请求的发送
    start_urls = ['http://www.baidu.com/']
	
    # 用作于数据解析，response参数表示的就是请求成功后对应的响应对象
    def parse(self, response):
        pass

```

## 6.修改爬虫文件并运行

将爬虫文件修改为以下内容：

```python
import scrapy


class FirstSpider(scrapy.Spider):
    name = 'first'
    allowed_domains = ['www.baidu.com']
    start_urls = ['http://www.baidu.com/','https://www.bilibili.com/']

    def parse(self, response):
        print(response)	# 打印相应结果

```

在控制台中执行：**`scrapy crawl first`**

![image-20211123155033506](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Blog_img/image-20211123155033506.png)

发现输出了一大堆东西，但是没有我们打印的response结果，仔细观察输出结果，发现下图输出了` 'ROBOTSTXT_OBEY': True`,这代表爬虫将遵守Robot协议，我们配置为Flase不遵守此协议即可。

![image-20211123155247327](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Blog_img/image-20211123155247327.png)

这就是导致没有输出结果的原因。

我们只需要修改配置文件即可：

打开工程项目下的settings.py文件

![image-20211123155502652](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Blog_img/image-20211123155502652.png)

将`ROBOTSTXT_OBEY = True`修改为`ROBOTSTXT_OBEY = False`即可。

再次执行：

![image-20211123160225203](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Blog_img/image-20211123160225203.png)

这次运行我们加了`--nolog`参数，屏蔽了程序执行的日志，这样控制台只会输出我们想要的内容，但是不推荐使用`--nolog`，因为程序有问题，不会报错，导致无法排错。

通过上图发现程序正常运行，并输出了我们想要的结果。

## 7.Scrapy的数据解析

任务目标：

- 爬取糗事百科中段子类中的发帖人和发帖内容

创建工程和爬虫文件：

```shell
scrapy startproject qiubaiPro	# 创建工程
scrapy genspider qiubai www.xxx.com	# 创建爬虫文件
```

编辑爬虫文件

```python
import scrapy


class QiubaiSpider(scrapy.Spider):
    name = 'qiubai'
    # allowed_domains = ['www.xxx.com']
    # 待爬取的Url
    start_urls = ['https://www.qiushibaike.com/text/']

    def parse(self, response):
        # 解析作者的名称+段子内容
        # 获取节点
        div_list = response.xpath('/html/body/div[1]/div/div[2]/div')
        # 遍历节点
        for div in div_list:
            # 获取作者名和段子内容
            # extract可以将Selector对象中所存储的data对象提取出来
            # 如果是对列表使用extract，可以将列表中所有Selector对象中所存储的data对象提取出来
            author = div.xpath('./div[1]/a[2]/h2/text()')[0].extract()
            author = div.xpath('./div[1]/a[2]/h2/text()').extract_first()	# 同上
            content = div.xpath('./a[1]/div/span[1]//text()')[0]
            print(author.strip(), content.strip())
            break
```

修改配置文件`setting.py`:

```python
# UA
USER_AGENT = 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/95.0.4638.69 Safari/537.36'
# Robots协议
ROBOTSTXT_OBEY = False
# 显示日志等级
LOG_LEVEL = "ERROR"
```

运行工程：`scrapy crawl qiubai`：

![image-20211123175333718](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Blog_img/image-20211123175333718.png)

发现段子内容打印的是一个Selector对象，而作者名并没有被Selector包裹，说明extract()是提取Selector中的data内容。

##  8.持久化存储

### 1.基于终端命令存储

> 只能将parse方法的返回值存储在本地文件中

修改爬虫文件：

```python
import scrapy


class QiubaiSpider(scrapy.Spider):
    name = 'qiubai'
    # allowed_domains = ['www.xxx.com']
    start_urls = ['https://www.qiushibaike.com/text/']

    def parse(self, response):
        # 解析作者的名称+段子内容
        div_list = response.xpath('/html/body/div[1]/div/div[2]/div')
        data_all = []
        for div in div_list:
            author = div.xpath('./div[1]/a[2]/h2/text()')[0].extract()
            author1 = div.xpath('./div[1]/a[2]/h2/text()').extract_first()
            content = div.xpath('./a[1]/div/span[1]//text()').extract()
            content = ''.join(content)
            dit = {
                'author':author,
                'content':content
            }
            data_all.append(dit)
        return data_all

```

终端执行：`scrapy crawl qiubai -o data.json`:

![image-20211123185601067](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Blog_img/image-20211123185601067.png)

查看当前目录，已经生成了data.json文件:

![image-20211123185641646](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Blog_img/image-20211123185641646.png)

假如我们要保存成txt行不行呢？

试一下：

![image-20211123185723863](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Blog_img/image-20211123185723863.png)

发现报错了，提示只支持`json`, `jsonlines`, `jl`, `csv`, `xml`, `marshal`, `pickle`这几种文件。

### 2.基于管道存储

- 编码流程
  1. 数据解析
  2. 在item类中定义相关属性
  3. 将解析的数据封装存储到item类型的对象
  4. 将item类型的对象提交给管道进行持久化存储操作
  5. 在管道类的process_item中要将其接受到的item对象中存储的数据进行持久化存储
  6. 在配置文件中开启管道

例：

1. 数据解析

   修改qiubai文件：

   ```python
   import scrapy
   from qiubaiPro.items import QiubaiproItem
   
   
   class QiubaiSpider(scrapy.Spider):
       name = 'qiubai'
       # allowed_domains = ['www.xxx.com']
       start_urls = ['https://www.qiushibaike.com/text/']
       def parse(self, response):
           item = QiubaiproItem()
           # 解析作者的名称+段子内容
           div_list = response.xpath('/html/body/div[1]/div/div[2]/div')
           data_all = []
           for div in div_list:
               author = div.xpath('./div[1]/a[2]/h2/text()')[0].extract()
               author1 = div.xpath('./div[1]/a[2]/h2/text()').extract_first()
               content = div.xpath('./a[1]/div/span[1]//text()').extract()
               content = ''.join(content)
               item['author'] = author
               item['content'] = content
               yield item  # 将item提交给管道
   ```

2. 在item类中定义相关属性

   打开工程目录下的item文件：

   ```python
   import scrapy
   
   
   class QiubaiproItem(scrapy.Item):
       # define the fields for your item here like:
       # name = scrapy.Field()
       # 创建2个属性
       author = scrapy.Field()
       content = scrapy.Field()
   ```

3. 将解析的数据封装存储到item类型的对象

   这一步其实就是第一步qiubai文件中的第2行和10和19-20行：

   - `from qiubaiPro.items import QiubaiproItem` 导入item文件中的`QiubaiproItem `类
   - `item = QiubaiproItem()` 创建一个item对象
   - `item['author'] = author`和`item['content'] = content`给对象的author和content属性赋值

   

4. 将item类型的对象提交给管道进行持久化存储操作

	- `yield item`  返回item对象

5. 在管道类pipelines的process_item中要将其接受到的item对象中存储的数据进行持久化存储

   修改工程目录下的pipelines.py文件

   ```python
   # Define your item pipelines here
   #
   # Don't forget to add your pipeline to the ITEM_PIPELINES setting
   # See: https://docs.scrapy.org/en/latest/topics/item-pipeline.html
   
   
   # useful for handling different item types with a single interface
   from itemadapter import ItemAdapter
   
   
   class QiubaiproPipeline:
       f = None
   
       # 开启爬虫时执行，只执行一次
       # 重写父类方法
       def open_spider(self, spider):
           print("开始爬虫.....")
           self.f = open('qiubai.txt', 'w', encoding='utf-8')
   
       # 专门用来处理item对象
       # 该方法可以接收爬虫文件提交过来的item对象
       # 该方法每接到一个item对象就会调用一次
       def process_item(self, item, spider):
           author = item['author']
           content = item['content']
           self.f.write(author + ':' + content + '\n')
           return item
   
       # 关闭爬虫时执行，只执行一次。 (如果爬虫中间发生异常导致崩溃，close_spider可能也不会执行)
       def close_spider(self, spider):
           print("爬虫结束....")
           self.f.close()
   ```

6. 在配置文件中开启管道

   修改工程目录下settings.py文件

   将

   ```python
   ITEM_PIPELINES = {
       # 300表示是优先级，数值越小，优先级越高
       'qiubaiPro.pipelines.QiubaiproPipeline': 300,
   }
   ```

   取消注释

### 3.将爬取的数据存两份

任务目标：将爬取的数据一份存到txt文件，一份存到mysql数据库

基于上一节的代码进行修改

在pipelines.py添加代码：

```python
import pymysql


class MysqlPipeline:
    conn = None
    cour = None

    def open_spider(self, spider):
        self.conn = pymysql.connect(host="127.0.0.1", port=3306, user='root', password='123456', db='qiubai',
                                    charset='utf8')

    def process_item(self, item, spider):
        self.cour = self.conn.cursor()
        try:
            self.cour.execute('insert into qiubai value ("%s","%s")' % (item['author'], item['content']))
            self.conn.commit()
        except Exception as e:
            print(e)
            self.conn.rollback()
        return item	
    # 这里的item代表将item传给下一个类，在QiubaiproPipeline类中的MysqlPipeline方法，最终返回了item，如果不返回item，那MysqlPipeline类就接受不到item对象。

    def close_spider(self, spider):
        self.cour.close()
        self.conn.close()

```

修改setting.py文件：

```python
ITEM_PIPELINES = {
    # 300表示是优先级，数值越小，优先级越高
    'qiubaiPro.pipelines.QiubaiproPipeline': 300,
    'qiubaiPro.pipelines.MysqlPipeline': 301,	# 添加这一条，优先级设置为301，代表爬取的数据会先执行QiubaiproPipeline类，然后执行MysqlPipeline类
}
```

![image-20211123234530728](https://cdn.jsdelivr.net/gh/zhaotaogit/images/Blog_img/image-20211123234530728.png)

查看mysql数据库中是否已有存取数据：

![image-20211130222547726](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/image-20211130222547726.png)

这里我运行了多次，所以qiubai表存在98条数据，总之，证明了程序成功爬取数据并存到了mysql中。

## 9.全站数据爬取

> 就是将网站中某板块下的全部页码对应的数据进行爬取

xiaohua.py

```python
import scrapy


class XiaohuaSpider(scrapy.Spider):
    name = 'xiaohua'
    # allowed_domains = ['www.xxx.com']
    start_urls = ['https://www.tupianzj.com/meinv/mm/']
    url = 'https://www.tupianzj.com/meinv/mm/list_218_%d.html'
    page_num = 2

    def parse(self, response):
        li_list = response.xpath("/html/body/div[2]/div/div/div[3]/div/ul/div/li")
        for i in li_list:
            img_name = i.xpath('./a/label/text()').extract_first()
            print(img_name)
        new_url = format(self.url % self.page_num)
        self.page_num += 1
        if self.page_num < 31:
            # 手动请求发送
            yield scrapy.Request(url=new_url, callback=self.parse)	# 回调函数
```

## 10.请求传参

使用场景：如果爬取解析的数据不在同一张页面中(深度爬取)

```python
import scrapy
from bossPro.items import BossproItem


class BossSpider(scrapy.Spider):
    name = 'boss'
    # allowed_domains = ['https://www.zhipin.com/c100010000/?query=python&ka=sel-city-100010000']
    start_urls = ['https://www.zhipin.com/c100010000/?query=python&ka=sel-city-100010000']

    url = 'https://www.zhipin.com/c101210100/?query=python&page=%d&ka=page-%d'
    page_num = 2

    def parse(self, response):
        # print(response.text)
        li_list = response.xpath('/html/body/div[1]/div[3]/div/div[3]/ul/li')
        # print(li_list)
        for i in li_list:
            item = BossproItem()
            # /html/body/div[1]/div[3]/div/div[3]/ul/li[1]/div/div[1]/div[1]/div/div[1]/span[1]/a
            # /html/body/div[1]/div[3]/div/div[3]/ul/li[1]/div/div[1]/div[1]/div//*[@id="main"]/div/div[3]/ul/li[1]/div/div[1]/div[1]/div
            job_name = i.xpath('./div/div[1]/div[1]/div/div[1]/span[1]/a/text()').extract_first()
            item['job_name'] = job_name
            job_detail = 'https://www.zhipin.com/' + i.xpath('.//*[@class="primary-box"]/@href').extract_first()
            # print(job_detail)
            # 详情页的信息交给parse_detail来处理，将当前的item传过去
            yield scrapy.Request(job_detail, callback=self.parse_detail, meta={'item': item})
        # 一共爬3页
        if self.page_num <= 3:
            self.page_num += 1
            new_url = format(self.url % self.page_num)
            yield scrapy.Request(new_url, callback=self.parse)

    def parse_detail(self, response):
        # print(response.text)
        item = response.meta['item']
        job_desc = response.xpath('/html/body/div[1]/div[2]/div[3]/div/div[2]/div[2]/div[1]/div//text()').extract()
        job_desc = ''.join(job_desc)
        item['job_desc'] = job_desc
        yield item
```

## 11.图片数据爬取之ImagesPipeline

**Scrapy字符串和图片爬取的区别：**

- 字符串：子需要基于xpath进行解析且提交管道进行持久化存储
- 图片：xpath解析出图片src的属性值。单独的对图片地址发起请求获取图片二进制类型的数据

**ImagesPipeline**

- 只需要将img的src属性值进行解析，提交到管道，管道会对图片进行src进行请求发送获取图片的二进制类型的数据，且还会帮我们进行持久化存储。

**使用流程:**

1. 数据解析(图片的地址)
2. 将存储图片的地址的item提交到制定的管道类
3. 在管道文件中自定制一个基于ImagesPipleline的一个管道类
   1. get_media_request
   2. file_path
   3. item_completed
4. 在配置文件中指定图片存储的目录，指定开启的管道

文件结构：

![image-20211220002940158](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/image-20211220002940158.png)

img.py:

```python
import scrapy
from imgsPro.items import ImgsproItem

class ImgSpider(scrapy.Spider):
    name = 'img'
    # allowed_domains = ['www.xxx.com']
    start_urls = ['https://sc.chinaz.com/tupian/']

    def parse(self, response):
        div_list = response.xpath('/html/body/div[2]/div[5]/div[1]/div[2]/div/div')
        # print(div_list)
        for div in div_list:
            # 使用伪属性
            src = 'https:'+div.xpath('./div/a/img/@src2').extract_first()
            item = ImgsproItem()
            item['src'] = src
            yield item
```

item.py:

```python
# Define here the models for your scraped items
#
# See documentation in:
# https://docs.scrapy.org/en/latest/topics/items.html

import scrapy


class ImgsproItem(scrapy.Item):
    # define the fields for your item here like:
    # name = scrapy.Field()
    src = scrapy.Field()
```



pipelines.py:

```python
# Define your item pipelines here
#
# Don't forget to add your pipeline to the ITEM_PIPELINES setting
# See: https://docs.scrapy.org/en/latest/topics/item-pipeline.html


# useful for handling different item types with a single interface
from itemadapter import ItemAdapter

from scrapy.pipelines.images import ImagesPipeline
import scrapy


# 注释掉不用这个
# class ImgsproPipeline:
#     def process_item(self, item, spider):
#         return item

class imgsPipeline(ImagesPipeline):
    # 根据图片地址进行数据请求
    def get_media_requests(self, item, info):
        print(1)
        yield scrapy.Request(item['src'])

    # 指定存储路径
    def file_path(self, request, response=None, info=None, *, item=None):
        print(2)
        imgName = request.url.split('/')[-1]
        print(imgName)
        return imgName

    def item_completed(self, results, item, info):
        print(3)
        return item  # 返回给下一个管道类
```

settings.py增加/修改：

```python
# 设置ua
USER_AGENT = 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/96.0.4664.110 Safari/537.36'
# 是否遵守robot协议
ROBOTSTXT_OBEY = False
# 指定开启的管道
ITEM_PIPELINES = {
   # 'imgsPro.pipelines.ImgsproPipeline': 300,
   'imgsPro.pipelines.imgsPipeline': 300,
}
# 指定图片存储的目录
IMAGES_STORE = './imgs'
```

## 12.中间件

- 下载中间件
  - 位置：引擎和下载器之间
  - 作用：批量拦截到整个工程中所有的请求和响应
  - 拦截请求：
    - UA伪装
    - 代理ip
  - 拦截响应：
    - 篡改响应数据，响应对象

拦截请求例：

项目结构:

![image-20211226151550413](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/image-20211226151550413.png)

middle.py

```python
import scrapy


class MiddleSpider(scrapy.Spider):
    name = 'middle'
    # allowed_domains = ['www.xxx.com']
    start_urls = ['http://www.baidu.com/s?&wd=ip']

    def parse(self, response):
        page_text = response.text
        with open('ip.html', 'w', encoding='utf-8') as f:
            f.write(page_text)
```

middlewares.py

```python
# Define here the models for your spider middleware
#
# See documentation in:
# https://docs.scrapy.org/en/latest/topics/spider-middleware.html
import random

from scrapy import signals

# useful for handling different item types with a single interface
from itemadapter import is_item, ItemAdapter


class MiddleproDownloaderMiddleware:
    # Not all methods need to be defined. If a method is not defined,
    # scrapy acts as if the downloader middleware does not modify the
    # passed objects.
    user_agent_list = [
        "Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.1 "
        "(KHTML, like Gecko) Chrome/22.0.1207.1 Safari/537.1",
        "Mozilla/5.0 (X11; CrOS i686 2268.111.0) AppleWebKit/536.11 "
        "(KHTML, like Gecko) Chrome/20.0.1132.57 Safari/536.11",
        "Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/536.6 "
        "(KHTML, like Gecko) Chrome/20.0.1092.0 Safari/536.6",
        "Mozilla/5.0 (Windows NT 6.2) AppleWebKit/536.6 "
        "(KHTML, like Gecko) Chrome/20.0.1090.0 Safari/536.6",
        "Mozilla/5.0 (Windows NT 6.2; WOW64) AppleWebKit/537.1 "
        "(KHTML, like Gecko) Chrome/19.77.34.5 Safari/537.1",
        "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/536.5 "
        "(KHTML, like Gecko) Chrome/19.0.1084.9 Safari/536.5",
        "Mozilla/5.0 (Windows NT 6.0) AppleWebKit/536.5 "
        "(KHTML, like Gecko) Chrome/19.0.1084.36 Safari/536.5",
        "Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/536.3 "
        "(KHTML, like Gecko) Chrome/19.0.1063.0 Safari/536.3",
        "Mozilla/5.0 (Windows NT 5.1) AppleWebKit/536.3 "
        "(KHTML, like Gecko) Chrome/19.0.1063.0 Safari/536.3",
        "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_8_0) AppleWebKit/536.3 "
        "(KHTML, like Gecko) Chrome/19.0.1063.0 Safari/536.3",
        "Mozilla/5.0 (Windows NT 6.2) AppleWebKit/536.3 "
        "(KHTML, like Gecko) Chrome/19.0.1062.0 Safari/536.3",
        "Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/536.3 "
        "(KHTML, like Gecko) Chrome/19.0.1062.0 Safari/536.3",
        "Mozilla/5.0 (Windows NT 6.2) AppleWebKit/536.3 "
        "(KHTML, like Gecko) Chrome/19.0.1061.1 Safari/536.3",
        "Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/536.3 "
        "(KHTML, like Gecko) Chrome/19.0.1061.1 Safari/536.3",
        "Mozilla/5.0 (Windows NT 6.1) AppleWebKit/536.3 "
        "(KHTML, like Gecko) Chrome/19.0.1061.1 Safari/536.3",
        "Mozilla/5.0 (Windows NT 6.2) AppleWebKit/536.3 "
        "(KHTML, like Gecko) Chrome/19.0.1061.0 Safari/536.3",
        "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/535.24 "
        "(KHTML, like Gecko) Chrome/19.0.1055.1 Safari/535.24",
        "Mozilla/5.0 (Windows NT 6.2; WOW64) AppleWebKit/535.24 "
        "(KHTML, like Gecko) Chrome/19.0.1055.1 Safari/535.24"
    ]
    # 写两个列表 原因是代理IP的类型中有 http 和 https两种类型
    # 可被选用的代理IP
    PROXY_http = [
        '153.180.102.104:80',
        '195.208.131.189:56055',
    ]
    PROXY_https = [
        '120.83.49.90:9000',
        '95.189.112.214:35508',
    ]

    # 拦截请求
    # User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/96.0.4664.110 Safari/537.36
    def process_request(self, request, spider):
        # UA伪装
        request.headers['User-Agent'] = random.choice(self.user_agent_list)
        # request.meta['proxy'] = 'http://106.15.197.250:8001'
        return None

    # 拦截响应
    def process_response(self, request, response, spider):
        return response

    # 拦截发生异常的请求
    def process_exception(self, request, exception, spider):
        # 代理
        if request.url.split(':')[0] == 'http':
            request.meta['proxy'] = 'http://' + random.choice(self.PROXY_http)
        else:
            request.meta['proxy'] = 'https://' + random.choice(self.PROXY_https)
        return request  # 将修改
```

拦截响应例：

- 爬取网易新闻中的新闻数据(标题和内容)
  - 通过网易新闻的首页解析出五大板块对应的详情页url（没有动态加载）
  - 每一个板块对应的新闻标题都是动态加载出来的（动态加载）
  - 通过解析出每一天新闻详情页的url获取详情页的页面源码，解析出新闻内容
  
  
