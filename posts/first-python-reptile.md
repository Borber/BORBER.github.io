---
title: 'First python spider'
date: 2019-07-16 12:27:14
tags: [python,爬虫,壁纸,编程,NSFW]
published: true
hideInList: false
feature: https://www.z4a.net/images/2019/07/16/2018-07-13-005825.jpg
---
爬取wallhaven壁纸网站NSFW资源😍

<!-- more -->


刚刚开始学习 python 写了一个小爬虫来爬取 豆瓣失败了,于是转而爬取 [wallhaven](https://wallhaven.cc/) 它拥有大量的超清壁纸资源 并且只要注册就可以开启 NSFW 选项 浏览,下载皆无限制.

首先 如果你只想爬取普通的资源 就可以不注册 也不使用 cookies .将下面的程序小改就可以做到.但是在此只介绍如何爬取包含NSFW的资源.

1. 首先注册网站 登录

2. ![1.png](https://www.z4a.net/images/2019/07/16/1.png)在 lastest 页面中选择 NSFW 选项 (蓝色箭头)并点击刷新按钮(红色箭头)

3. ![2c6289b60c5340c40.png](https://www.z4a.net/images/2019/07/16/2c6289b60c5340c40.png)

   在页面中 按f12调出 network 刷新页面(浏览器的刷新 区别于第二步) 选择第一个 找到 Request Headers 里的 cookie 全部复制

4. 将第三步复制的 cookie 黏贴到 下面代码块中的  cookies_text = '你自己的' 替换'你自己的'  filepath 选择一个你想放的地方 然后运行就好了 推荐直接复制到 pychram里面运行

```python
from bs4 import BeautifulSoup
import requests
cookie = {}
def get_cookies():
    cookies_text = '你自己的'
    for each in cookies_text.split(';'):
        name,value = each.strip().split('=',1)
        cookie[name] = value
def downimg(url):
    filepath = 'E:\File\Tmp\ ' #自己写
    r = requests.get(url, stream=True)
    if r.status_code != 200:
        return
    with open(filepath[:-1]+url[-10:], 'wb') as code:
        for img_data in r.iter_content(128):
            code.write(img_data)


def realimg(url):
    web_data = requests.get(url,cookies=cookie)
    Soup = BeautifulSoup(web_data.text, 'lxml')
    imgs = Soup.select('#wallpaper')
    for img in imgs:
        downimg(img.get('src'))

def start(num):
    url = 'https://wallhaven.cc/search?categories=111&purity=111&sorting=date_added&order=desc&page='+num
    web_data = requests.get(url,cookies=cookie)
    Soup = BeautifulSoup(web_data.text, 'lxml')
    img_web_links = Soup.select('#thumbs > section > ul > li > figure > a.preview')
    for img_web in img_web_links:
        realimg(img_web.get('href'))


get_cookies()
for i in range(1,26514):
    start(str(i))
```

😂玩的开心