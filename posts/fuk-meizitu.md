---
title: 'Fu*k meizitu'
date: 2019-07-29 13:36:30
tags: [python,爬虫,NSFW,编程]
published: true
hideInList: false
feature: https://www.z4a.net/images/2019/07/29/fall_by_wlop-d96fxqh.jpg
---
爬取妹子图全站图片

<!-- more -->

由于我没有提前记录过程 所以没有截图，以后尽量把自己的思考过程都全部截图发出来。



首先通过 [首页](https://www.mzitu.com) 的的所有分页面爬取所有的图片的首页链接 （写完之后发现有另一个界面 更容易爬 但是已经写完了就没有改了 这里放上链接 [全部](https://www.mzitu.com/all/)）

这一步是很简单的， 主要就是吧真正的套图的链接全部整理出来，放在 mongo/meizitu/home 这个表里面，准备二次加工。

```python
#home_url.py

from toolkits.ip_proxies import get_proxies
from bs4 import BeautifulSoup
from fake_useragent import UserAgent
import requests
import pymongo
import time

client = pymongo.MongoClient('localhost', 27017)
meizitu = client['meizitu']
home = meizitu['home']

ua = UserAgent()

headers = {
    'User-Agent': ua.random,
    'Referer': 'https://www.mzitu.com'
}


def get_home_url(i=0):
    url = f'https://www.mzitu.com/page/{i}'
    wb_data = requests.get(url, proxies=get_proxies(), headers=headers, timeout=3)
    soup = BeautifulSoup(wb_data.text, 'lxml')
    real = soup.select('#pins > li > span > a')
    for index, each in enumerate(real):
        home.insert_one({'URL': each.get('href')})

```





接下来就是对爬去的链接做二次加工。

把每个链接对应的套图的 标题，链接，最大页码数 提取出来，因为妹子图的网页结构非常简单，每张图对应的URL 都是首页后面加页码，所以可以利用这个，减少储存的URL数。保存的 title 是作为以后的储存目录子文件夹名。

以及一个用于之后下载时提取每个界面图片的函数（get_imgs(url)）

这里尤其要说 关于 

```python
for i in range(10):
```

的作用。

不知道是由于网站的反扒措施，还是我使用的代理ip池中有ip失效，总之会有request中断的现象，总会导致爬虫强制退出，这一退出就是浪费几十分钟的时间，所以加上 try 的报错处理之后，程序的鲁棒性会提高非常多，这个结构也出现在随后的几个py文件中，随后不在作解释。

这里也强烈建议使用 IP代理 可以参考我的上一篇博文。都打包好了可以直接使用。

```python
#find_imgs.py

from toolkits.ip_proxies import get_proxies
from bs4 import BeautifulSoup
from fake_useragent import UserAgent
import requests
import pymongo
import time


client = pymongo.MongoClient('localhost', 27017)
meizitu = client['meizitu']
home = meizitu['home']
imgs = meizitu['imgs']

ua = UserAgent()


def get_title_and_pages(url):
    headers = {
        'User-Agent': ua.random,
        'Referer': 'https://www.mzitu.com'
    }
    for i in range(10):
        try:
            wb_data = requests.get(url, headers=headers, proxies=get_proxies())
            while wb_data != 200:
                wb_data = requests.get(url, headers=headers,proxies=get_proxies())
        except Exception:
            if i >= 9:
                print('Fuck!')
            else:
                time.sleep(0.5)
        else:
            break

    title = url[-6:]
    soup = BeautifulSoup(wb_data.text, 'lxml')
    titles = soup.select('div.main h2')
    for each in titles:
        title = each.get_text()
        break
    url_max = soup.select('div.pagenavi > a > span')[-2].get_text()
    imgs.insert_one({'title': title, 'url': url, 'url_max': int(url_max)})


def get_imgs(url):
    headers = {
        'User-Agent': ua.random,
        'Referer': 'https://www.mzitu.com'
    }
    for i in range(10):
        try:
            wb_data = requests.get(url, headers=headers, proxies=get_proxies())
            while wb_data.status_code != 200:
                wb_data = requests.get(url, headers=headers, proxies=get_proxies())
        except Exception:
            if i >= 9:
                print('Fuck!')
            else:
                time.sleep(0.5)
        else:
            break
    soup = BeautifulSoup(wb_data.text, 'lxml')
    img_url = soup.select('div.main-image img')[0].get('src')
    return img_url



```





接下来是下载模块

```python
#download_imgs.py

from toolkits.ip_proxies import get_proxies
from fake_useragent import UserAgent
import requests
import os
import time

seq = '/'
ua = UserAgent()

headers = {
    'User-Agent': ua.random,
    'Referer': 'https://www.mzitu.com'
}


def downimg(index, url, path):
    print(url)
    filename = path + seq[0] + str(index) + url[-4:]
    print(filename)
    if os.path.exists(filename):
        return
    for i in range(10):
        try:
            r = requests.get(url, headers=headers, proxies=get_proxies(), stream=True)
        except Exception :
            if i >= 9:
                print('Fuck!')
            else:
                time.sleep(0.5)
        else:
            time.sleep(0.1)
            break
    with open(filename, 'wb') as code:
        for img_data in r.iter_content(128):
            code.write(img_data)


```





最后是主函数：

这里面有一个大坑，坑的无与伦比，这也是这个爬虫我学到的比较重要的东西之一，pymongo创造的链接，是有时效性的，及时加了 no_cursor_timeout=True 他本身的链接就是以后时效性的，所以，出了跑错处理，还需要进行重连。

```python
def download_all():
    client_local = pymongo.MongoClient('localhost', 27017)
    meizitu_local = client_local['meizitu']
    imgs_local = meizitu_local['imgs']
    items = imgs_local.find(no_cursor_timeout=True)
```

这一段 就是在每一次进行 下载 调用时都进行一次重连。当然这一般就是在发生链接断开错误时才会再次调用的。（据网上资料，链接有效时间为10分钟）

```python
#main.py

from test.home_url import get_home_url
from test.find_imgs import get_title_and_pages,get_imgs
from test.download_img import downimg
from bs4 import BeautifulSoup
from fake_useragent import UserAgent
import requests
import pymongo
import os
import time

client = pymongo.MongoClient('localhost', 27017)
meizitu = client['meizitu']
home = meizitu['home']
imgs = meizitu['imgs']

rootpath = '/home/x/BORBER/File/Tmp/meizitu' # 自己改
seq = '/'


def mkdir(path):
    folder = os.path.exists(path)
    if not folder:
        os.makedirs(path)


def home_all_url():
    for i in range(1, 226):
        get_home_url(i)
        print(f'Now in {i}')


def imgs_all_url():
    for index, each in enumerate(home.find(no_cursor_timeout=True)):
        print(f'Now in {index}')
        print(each['URL'])
        get_title_and_pages(each['URL'])
        home.delete_one({'URL': each['URL']})


def download_all():
    client_local = pymongo.MongoClient('localhost', 27017)
    meizitu_local = client_local['meizitu']
    imgs_local = meizitu_local['imgs']
    items = imgs_local.find(no_cursor_timeout=True)
    for item in items:
        filepath = rootpath + seq[0] + item['title']
        print(filepath)
        mkdir(filepath)
        for i in range(1, item['url_max']):
            downimg(i, get_imgs(item['url']+seq[0]+str(i)), filepath)
        imgs.delete_one({'url': item['url']})
    items.close()


def safe_download():
    for i in range(9999):
        try:
            download_all()
        except Exception:
            print('Fuck')
            time.sleep(0.5)
            download_all()
        else:
            break


def clear_all():
    meizitu.drop_collection('home')
    meizitu.drop_collection('imgs')


if __name__ == '__main__':
    home_all_url()
    imgs_all_url()
    safe_download()

```

此版本理论上可以一次运行成功 爬取全站 17万+图片 共计18.1G数据

![16286196bfda2cc08.png](https://www.z4a.net/images/2019/07/29/16286196bfda2cc08.png)
![2c6341d3c5e38c041.png](https://www.z4a.net/images/2019/07/29/2c6341d3c5e38c041.png)
![3a94d521745bd3db4.png](https://www.z4a.net/images/2019/07/29/3a94d521745bd3db4.png)

身体是革命的本钱啊 骚年， 滑稽