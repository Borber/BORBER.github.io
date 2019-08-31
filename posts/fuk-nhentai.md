---
title: 'Fu*k nhentai'
date: 2019-07-30 12:42:35
tags: [python,爬虫,代理,NSFW]
published: true
hideInList: false
feature: https://www.z4a.net/images/2019/07/30/Coronation-Wallpaper.jpg
---
爬取 [nhentai](https://nhentai.net) 指定图册。

<!-- more -->


 输入具体网址以及一个空格，即可。 注意文件结构，以及 toolkits/ip_proxies toolkits/down_load 工具包的搭建参考上一篇博文。



```python
from bs4 import BeautifulSoup
from toolkits.ip_proxies import get_proxies
from toolkits.down_load import down_load
from fake_useragent import UserAgent
import requests
import os
import pymongo


client = pymongo.MongoClient('localhost', 27017)
nhentai = client['nhentai']
imgs = nhentai['imgs']

rootpath = '/home/x/BORBER/File/Tmp/nhentai' # 自己改
seq = '/'

ua = UserAgent()
headers = {
    'User-Agent': ua.random,
    'Referer': 'https://nhentai.net'
}


def mkdir(path):
    folder = os.path.exists(path)
    if not folder:
        os.makedirs(path)


def get_title_pages(url, index=1):
    r = requests.get(url, headers=headers, proxies=get_proxies())
    soup = BeautifulSoup(r.text, 'lxml')
    title = soup.select('#info > h2')
    path = rootpath+seq+title[0].get_text()
    mkdir(path)
    max_pages = soup.select('#info > div:nth-child(4)')
    data = {
        'index': index,
        'title': title[0].get_text(),
        'url': url,
        'max': int(max_pages[0].get_text().split()[0]),
        'path': path
    }
    imgs.insert_one(data)


def get_img(url):
    r = requests.get(url, headers=headers, proxies=get_proxies())
    soup = BeautifulSoup(r.text, 'lxml')
    return soup.select('#image-container > a > img')[0].get('src')


def download_all():
    for item in imgs.find():
        for i in range(1, item['max']+1):
            down_load(get_img(item['url']+str(i)), item['path']+seq[0]+str(i), i, item['max']+1, headers)


if __name__ == '__main__':
    nhentai.drop_collection('imgs')
    print('Enter the specific link to the pictures:')
    ur = input()[:-1]
    get_title_pages(ur)
    download_all()

```

