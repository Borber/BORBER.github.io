---
title: 'Use selenium'
date: 2019-08-14 23:06:24
tags: [python,爬虫,selenium]
published: true
hideInList: false
feature: https://www.z4a.net/images/2019/08/14/2019-08-14_23-09-26.png
---
使用 [selenium](https://www.seleniumhq.org) 抓取网页

<!-- more -->


之前一直使用的 [BeautifulSoup4](https://beautifulsoup.readthedocs.io/zh_CN/v4.4.0/) 以及 少许使用 [Requests](https://2.python-requests.org//zh_CN/latest/) 但是由于自身实力关系,爬取动态加载的网页,还是不得不使用  selenium 在实验期间,遇到了一些困难,在此记录.

```python
from selenium import webdriver
from selenium.webdriver.common.keys import Keys
from selenium.webdriver.chrome.options import Options
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
from bs4 import BeautifulSoup
import time


url = "http://www.baidu.com"
driver.get(url)
elem = driver.find_element_by_name("wd")
elem.clear()
elem.send_keys("BORBER")
elem.send_keys(Keys.RETURN)


with open("baidu.html", "w", encoding="utf-8") as f:
    f.write(driver.page_source)
driver.close()
```

以上这是我最初的代码 它无法抓取 搜索后的界面代码. 以至于我开始怀疑 selenium的效果

但是经过排查,发现是界面没有加载完成便开始抓取导致.

在使用 time.sleep() 之后 解决了这个问题,但这不是selenium 的写法.



以下是修改后,加入了显示等待的代码,

```python
from selenium import webdriver
from selenium.webdriver.common.keys import Keys
from selenium.webdriver.chrome.options import Options
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
from bs4 import BeautifulSoup
import time

chrome_options = Options()
chrome_options.add_argument('--headless')
chrome_options.add_argument('--disable-gpu')

driver = webdriver.Chrome()  # options=chrome_options
url = "http://www.baidu.com"
driver.get(url)
elem = driver.find_element_by_name("wd")
elem.clear()
elem.send_keys("BORBER")
elem.send_keys(Keys.RETURN)

try:
    WebDriverWait(driver, 10).until(EC.presence_of_element_located((By.ID, "page")))
    with open("baidu.html", "w", encoding="utf-8") as f:
        f.write(driver.page_source)
finally:
    time.sleep(2)
    driver.close()
with open("baidu.html", "w", encoding="utf-8") as f:
    f.write(driver.page_source)
driver.close()
```

不过路途经过 知乎 看见这篇文章 [为什么不推荐Selenium写爬虫](https://zhuanlan.zhihu.com/p/33542626)  感觉 selenium 的优势不大 所以不出意外,又要开始学习 **[Scrapy](https://scrapy.org)** 以及  [Requests](https://2.python-requests.org//zh_CN/latest/)  了.

学无止境