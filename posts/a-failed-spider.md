---
title: 'A failed spider'
date: 2019-07-24 01:44:33
tags: [python,爬虫,编程,小说]
published: true
hideInList: false
feature: https://www.z4a.net/images/2019/07/24/2018-05-24-234858.jpg
---
失败的爬虫 成功的尝试

<!-- more -->


在爬取完漫画网站之后，我在想，我还能用自己浅薄的知识做点什么，但实在是因为自己 python的基本功不够扎实，以及自己的需求过于模糊，所以最后还是选择了爬取笔趣阁的小说。练习python，熟悉bs4 和 requsets 的使用。

因为想要使用多进程，所以是用的与之前不一样的写法，以及困于PyChram的输入网址之后直接回车就会打开浏览器，所以默认多加一个字符长度，默认是空格

首先是爬取文章标题

```python
#

from bs4 import BeautifulSoup
import requests


def get_titles(urlx):
    wb_data = requests.get(urlx)
    wb_data.encoding = 'UTF-8'
    soup = BeautifulSoup(wb_data.text, 'lxml')
    return soup.select('h1')[0].get_text()


```

其次是 爬取文章目录

```python
#

from bs4 import BeautifulSoup
import requests
import pymongo

head = 'https://www.biquge.com.cn'
client = pymongo.MongoClient('localhost', 27017)
BQG = client['BQG']
chapters = BQG['chapters']


def get_chapters(urlx):
    wb_data = requests.get(urlx)
    wb_data.encoding = 'UTF-8'
    soup = BeautifulSoup(wb_data.text, 'lxml')
    local_chapters = soup.select('dd > a')
    for index, each in enumerate(local_chapters):
        local_chapter = {
            'index': index,
            'url': head+each.get('href')
        }
        chapters.insert_one(local_chapter)


```

然后是 爬取 文章内容

```python
#

from bs4 import BeautifulSoup
import requests
import pymongo

client = pymongo.MongoClient('localhost', 27017)
BQG = client['BQG']
books = BQG['books']
chapters = BQG['chapters']
articles = BQG['articles']


def get_articles(urlx):
    wb_data = requests.get(urlx)
    wb_data.encoding = 'UTF-8'
    soup = BeautifulSoup(wb_data.text, 'lxml')
    wb_data.close()
    title = {'T|C': 1, 'm': soup.select('div.bookname > h1')[0].get_text()}
    articles.insert_one(title)
    content = soup.select('#content').__str__().replace('[<div id="content">', '').replace('</div>]', '').replace('\xa0', '').split('<br/><br/>')
    for each in content:
        paragraph = {
            'T|C': 0,
            'm': each
        }
        articles.insert_one(paragraph)
```

主程序：

```python
import pymongo
import os
from multiprocessing import Pool
from zerox.bqg_get_chapters import get_chapters
from zerox.bqg_get_articles import get_articles
from zerox.bqg_get_titles import get_titles

client = pymongo.MongoClient('localhost', 27017)
BQG = client['BQG']
books = BQG['books']
chapters = BQG['chapters']
articles = BQG['articles']
rootpath = '/home/x/BORBER/File/Tmp/novel/'
filend = '.txt'


def write_in(item):
    if item['T|C'] == 1:
        file.write(item['m'])
        file.write('\n\n\n\n')
    else:
        print('  ')
        file.write(item['m'])
        file.write('\n\n')


if __name__ == '__main__':
    BQG.drop_collection('books')
    BQG.drop_collection('chapters')
    BQG.drop_collection('articles')
    pool = Pool()
    print('Enter the specific link to the novel:')
    url = input()[:-1]
    title = get_titles(url)
    a = rootpath + title + filend
    file = open(rootpath + title + filend, 'w')
    get_chapters(url)
    for item in chapters.find():
        get_articles(item['url'])
    for item in articles.find():
        write_in(item)



```

以下提供 监测程序：

```python
import time
import pymongo
import os

client = pymongo.MongoClient('localhost', 27017)
BQG = client['BQG']
books = BQG['books']
chapters = BQG['chapters']
articles = BQG['articles']

while True:
    os.system('clear')
    print(chapters.find().count()+articles.find().count())
    time.sleep(2)

```

文件结构：

```shell
-zero
	-zerox  #python package
		-bqg_get_chapters.py
		-bqg_get_articles.py
		-bqg_get_titles.py
		-count.py
		-main.py
		-__init__.py
```

但是 为什么文章叫 失败的爬虫呢？ 因为我只成功了两次，后面的话就会报错了，应该是 笔趣阁的反扒手段，所以还是同样，如果以后我的技术进步了，我会着手改进这个爬虫的 ，有想尝试的朋友可以先试着加个 headers 到 get方法。

**此爬虫需要使用 mongoDB**

真的去下苦工 打基础了 (๑•̀ㅂ•́)و✧