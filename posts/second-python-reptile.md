---
title: 'Second python spider'
date: 2019-07-16 16:30:35
tags: [python,爬虫,NSFW,编程,漫画]
published: true
hideInList: false
feature: https://www.z4a.net/images/2019/07/16/6b8c14f8gw1f0vg7ga9raj21040lzdmx.png
---
 爬取[zero搬运网](http://www.zerobyw4.com/) 漫画 有福利哦 🤪
 
<!-- more -->

 朋友( [Miracoi](https://miracol.cn/) )说自己的泡面板没漫画可看,我也正好昨天开始学爬虫 看看能不能爬些漫画给他看,我就找了一个漫画网站,开始了.

[zero搬运网](http://www.zerobyw4.com/) 看了一眼 注册用户可以看 除最新章节的所有,但是对应的下载有次数限制,可观看没有啊.嘿嘿嘿 搞起.

1. 注册 登录

2. 拿到 cookie 具体可以看 我发布的 [First python reptile](https://borber.xyz/post/first-python-reptile/) 其中第三步

3. 替换下面代码的 cookie 以及 你的文档储存地址

   ```python
   from bs4 import BeautifulSoup
   import requests
   import os
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
       for NUM in range(1,46):
           url = 'http://www.zerobyw4.com/plugin.php?id=jameson_manhua&c=index&a=ku&&page=' +str(NUM)
           web_data = requests.get(url)
           Soup = BeautifulSoup(web_data.text, 'lxml')
           urls = Soup.select('div.uk-card > div > a')
           for each in urls:
               one(web_head+each.get('href')[1:])
   
   def one(url):
       web_data = requests.get(url)
       Soup = BeautifulSoup(web_data.text, 'lxml')
       details = Soup.select('a.uk-button-default')
       title = Soup.select('h3.uk-heading-line')
       folderpath = ''
       for each in title:
           if len(each.get_text()) > 4:
               folderpath = rootpath[:-1] + each.get_text()
               mkdir(folderpath)
               break
       chapterNum = 0
       for each in details:
           filepath = folderpath+seq[0]+str(chapterNum)
           mkdir(filepath)
           chapterNum = chapterNum+1
           realimg(web_head+each.get('href')[1:],filepath)
   
   
   def realimg(url,filepath):
       web_data = requests.get(url,headers=header)
       Soup = BeautifulSoup(web_data.text, 'lxml')
       imgs = Soup.select('div.mb0 > img')
       NUM = 0
       for img in imgs:
           downimg(img.get('src'),filepath,NUM)
           NUM = NUM+1
   
   
   def downimg(url,filepath,NUM):
       r = requests.get(url, stream=True)
       if r.status_code != 200:
           return
       filename = filepath+seq[0]+str(NUM)+filend
       with open(filename, 'wb') as code:
          for img_data in r.iter_content(128):
              code.write(img_data)
   
   start()
   
   ```

    漫画哪有 python有趣 嘿嘿嘿 😃