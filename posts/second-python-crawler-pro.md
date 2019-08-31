---
title: 'Second python spider pro'
date: 2019-07-18 00:30:52
tags: [python,爬虫,编程,NSFW,漫画]
published: true
hideInList: false
feature: https://www.z4a.net/images/2019/07/18/1.jpg
---
 爬取[zero搬运网](http://www.zerobyw4.com/) 漫画 有福利哦 🤪 Pro

<!-- more -->

写完第二个爬虫之后,写了好几个,但是总归是因为技术原因,达不到自己想要的效果,在重写第二个爬虫时这种感觉尤为强烈,所以写完这个之后,回去继续看剩下的网课,充实自己

 因为不会反爬以及多线程 , 以及模拟登录 等等一系列的技术,所以写的非常简陋,但是还是用上了 MongoDB 因为涉及到数据库的操作 所以不是简单复制下来就能跑,需要安装相应的 包,以及软件,但现在比较懒,所以省略,如果有朋友遇见困难,可以评论区留言,我会回复,或者更新的.

1. 爬取全站版本 是我一开始写的,但是由于数据太大,需要长时间的访问,不可避免地导致反爬机制,以及链接断开之后,没有重连手段,导致十分鸡肋,所以产生更改目标,重写爬取单部漫画方案.
2. 在全站版本上修改的单部版本,但没想到是大改,所以,单部版本更加优秀 可以 参考单部 修改全站版本 还是本人太懒 不想改了.

```python
from bs4 import BeautifulSoup
import requests
import os
import time
import pymongo

client = pymongo.MongoClient('localhost',27017)
Mongo_zero = client['zero']
Mongo_urls = Mongo_zero['urls']
Mongo_detials = Mongo_zero['detials']
Mongo_img_links = Mongo_zero['img_links']

header = {
    'User-Agent':'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/77.0.3833.0 Safari/537.36',
    'Cookie':'你自己的'

}

web_head = 'http://www.zerobyw4.com'
rootpath = 'E:\File\Tmp\ ' #自己改
seq = '\ '
filend = '.jpg'

def mkdir(path):
    folder = os.path.exists(path)

    if not folder:  # 判断是否存在文件夹如果不存在则创建为文件夹
        os.makedirs(path)  # makedirs 创建文件时如果路径不存在会创建这个路径
        print
        "---  new folder...  ---"
        print
        "---  OK  ---"

    else:
        print
        "---  There is this folder!  ---"



def start():
    count = 0
    for NUM in range(1,46):
        url = 'http://www.zerobyw4.com/plugin.php?id=jameson_manhua&c=index&a=ku&&page=' +str(NUM)
        web_data = requests.get(url)
        Soup = BeautifulSoup(web_data.text, 'lxml')
        urls = Soup.select('div.uk-card > div > a')
        titles = Soup.select('p.uk-text-truncate > a')
        for url,title in zip(urls,titles):
            data = {
                'index':count,
                'title':title.get_text(),
                'url':web_head+url.get('href')[1:]
            }
            count += 1
            print(data)
            mkdir(rootpath[:-1]+seq[0]+data['title'])
            Mongo_urls.insert_one(data)
        time.sleep(2)

def one():
    for item in Mongo_urls.find():
        web_data = requests.get(item['url'])
        Soup = BeautifulSoup(web_data.text, 'lxml')
        details = Soup.select('a.uk-button-default')
        for count,each in enumerate(details):
            data = {
                'index':item['index'],
                'count':count,
                'url':web_head + each.get('href')[1:]
            }
            print(data)
            mkdir(rootpath[:-1]+seq[0]+item['title']+seq[0]+str(data['count']))
            Mongo_detials.insert_one(data)
        time.sleep(2)


def realimg():
    num = 0
    for item in Mongo_detials.find():
        web_data = requests.get(item['url'], headers=header)
        Soup = BeautifulSoup(web_data.text, 'lxml')
        imgs = Soup.select('div.mb0 > img')
        NUM = 0
        for img in imgs:
            data = {
                'num':num,
                'title':Mongo_urls.find({'index':item['index']})[0]['title'],
                'chapter':item['count'],
                'count':NUM,
                'url':img.get('src')
            }
            NUM = NUM + 1
            print(data)
            Mongo_img_links.insert_one(data)
        time.sleep(2)



def downimg():
    for item in Mongo_img_links.find():
        filename = rootpath[:-1] + seq[0] + item['title'] + seq[0] + str(item['chapter']) + seq[0] + str(item['count']) + filend
        if os.path.exists(filename):
            continue
        r = requests.get(item['url'], stream=True)
        if r.status_code != 200:
            return
        with open(filename, 'wb') as code:
            for img_data in r.iter_content(128):
                code.write(img_data)
        r.close()
        time.sleep(1)

start()
one()
realimg()
downimg()

```

2. 爬取单部漫画

```python
from bs4 import BeautifulSoup
import requests
import os
import pymongo

client = pymongo.MongoClient('localhost', 27017)
Mongo_zero = client['zero']
Mongo_Details = Mongo_zero['details']
Mongo_img_links = Mongo_zero['img_links']

header = {
    'User-Agent': '',  # yours
    'Cookie': ''  # yours

}

web_head = 'http://www.zerobyw4.com'
rootpath = '/home/x/BORBER/BORBER/File/Tmp'  # yours
seq = '/'


def mkdir(path):
    folder = os.path.exists(path)
    if not folder:
        os.makedirs(path)


def one(url_x, rootpath_s):
    web_data = requests.get(url_x, headers=header)
    soup = BeautifulSoup(web_data.text, 'lxml')
    details = soup.select('a.uk-button-default')
    title = soup.select('li > h3.uk-heading-line')[0].get_text()
    rootpath_x = rootpath_s + seq[0] + title
    mkdir(rootpath_x)
    for index, each in enumerate(details):
        data = {
            'chapter': index,
            'title': each.get_text(),
            'url': web_head + each.get('href')[1:]
        }
        mkdir(rootpath_x + seq[0] + data['title'])
        print(data)
        Mongo_Details.insert_one(data)
    return rootpath_x


def realimg():
    num = 0
    for item in Mongo_Details.find():
        web_data = requests.get(item['url'], headers=header)
        soup = BeautifulSoup(web_data.text, 'lxml')
        imgs = soup.select('div.mb0 > img')
        count = 0
        for img in imgs:
            data = {
                'num': num,
                'chapter': item['chapter'],
                'count': count,
                'url': img.get('src')
            }
            num += 1
            count += 1
            print(data)
            Mongo_img_links.insert_one(data)


def downimg(rootpath_x):
    for item in Mongo_img_links.find():
        filename = rootpath_x + seq[0] + Mongo_Details.find({'chapter': item['chapter']})[0]['title'] + seq[0] + str(item['count']) + item['url'][-4:]
        print(filename)
        # if os.path.exists(filename):
        #     continue
        r = requests.get(item['url'], headers=header, stream=True)
        with open(filename, 'wb') as code:
            for img_data in r.iter_content(128):
                code.write(img_data)


Mongo_zero.drop_collection('details')
Mongo_zero.drop_collection('img_links')
print('输入你想下载的漫画详情页网址:')
url = input()
rootpath = one(url, rootpath)
realimg()
downimg(rootpath)

```

 漫画哪有 python有趣 嘿嘿嘿 😃