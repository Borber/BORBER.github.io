---
title: 'Third python spider'
date: 2019-07-16 22:07:02
tags: [python,爬虫,编程]
published: true
hideInList: false
feature: https://www.z4a.net/images/2019/07/16/2018-07-13-010717.jpg
---
爬取 58同城 招聘信息 🤩

<!-- more -->

这是我写的的第三个爬虫用来爬取 58同城上的招聘信息 也没有什么大用只是用来练手的,我觉得 编程是一个只有动手才能学会的东西.

这次的爬虫和前两次有些许不同,58 同城有自己的反爬措施.所以这次加上了限制请求频率的 time.sleap (其实 第二个爬虫也最好加入,因为我在使用第二个爬虫时,出现了远程服务器拒绝访问)

这此对于 selector 有的全新的认识 使用大大灵活了

58同城不需要注册就可以浏览 所以只要获取cookie就好

代码如下 :

```python
from bs4 import BeautifulSoup
import os
import time
import urllib
import requests
import time

header = {
    'user-agent':'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/77.0.3833.0 Safari/537.36',
    'cookie':'你自己的'
}
urls = []
file = open('E:\CODE\python\out\BORBER.txt','w') #自己写
def get_urls():
    for i in range(1,19):
        url = f'https://bj.58.com/ruanjiangong/pn{i}/?PGTID=0d302f82-0000-1864-07d2-bb7c42c41f7c&ClickID=2'
        urls.append(url)
    for each in urls:
        get_detials(each)

def get_detials(url):
    wb_data = requests.get(url)
    soup = BeautifulSoup(wb_data.text,'lxml')
    Address = soup.select('span.address')
    Job_names = soup.select('span.name')
    Job_salarys = soup.select('p.job_salary')
    Job_wels = soup.select('div.job_wel > span')
    Com_Names = soup.select('div.comp_name > a')
    Job_requires = soup.select('p.job_require')
    for Addres,Job_name,Job_salary,Job_wel,Com_Name,Job_require in zip(Address,Job_names,Job_salarys,Job_wels,Com_Names,Job_requires):
        data = {
            'Address':Addres.get_text(),
            'Job_name':Job_name.get_text(),
            'Job_salary':Job_salary.get_text(),
            'Job_wel':Job_wel.get_text(),
            'Com_Name':Com_Name.get_text(),
            'Job_require':Job_require.get_text().replace('&nbsp',' ')
        }
        fileprint(data)
def fileprint(data):
    file.write('地址: ' + data['Address'])
    file.write('\n')
    file.write('职位: '+data['Job_name'])
    file.write('\n')
    file.write('要求: '+data['Job_require'])
    file.write('\n')
    file.write('薪酬: '+data['Job_salary'])
    file.write('\n')
    file.write('福利: '+data['Job_wel'])
    file.write('\n')
    file.write('公司: '+data['Com_Name'])
    file.write('\n')
    file.write('\n===================================\n')

get_urls()
for url in urls:
    get_detials(url)
    time.sleep(2)
```

看了一下 京城就是京城啊 😅



附:[爬取结果](https://www.lanzous.com/i50oi6d
) 