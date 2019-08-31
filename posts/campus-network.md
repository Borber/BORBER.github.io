---
title: 'Campus Network'
date: 2019-08-29 18:16:31
tags: [python,爬虫,网络,selenium]
published: true
hideInList: false
feature: https://www.z4a.net/images/2019/08/29/2019-08-29_18-19-04.png
---
python自动重联校园网

<!-- more -->


在大学的朋友都知道,校园网是一个极其操蛋,而且是必须要用的东西,我的大学的价格是28元一月 一个账号,只能一台设备使用,这意味着,如果你手机连接之后,你的电脑就不能使用了,这又是何等的操蛋.

不过我也是比较幸运的是,在开学的前一个月,在上英语视听说的机房里,看到了校园网的登陆界面是有缓存着账号和密码的,而且不同于我们的学生号,它只有短短的六位,以及我在旁边几台电脑中,皆发现了此账号,我敏锐的意识到,这是一个VIP账号,或者是老师账号.

在我进入该账号的校园网管理界面时,我就知道这是一个为期四年的长久计划.

![2019-08-29_13-55-24.png](https://www.z4a.net/images/2019/08/29/2019-08-29_13-55-24.png)

我通过html 元素修改 将 password 改为 text 直接获得了明文密码,并且在之后的实验中,确定 这个账号和学生账号不同,它可以同时登陆,4-5台设备,这也意味着,蹭网的事,不会使账号的主人无网可上.并且,在宿舍时,只要共用一台路由器,便可以通过路由器只占用一个设备位置.

事情本来到这里就已经完了,但是随后的时间里,特别是到了醉经,我们宿舍的账号会被挤下登录,而我又经常将电脑放在宿舍跑python 之类的脚本.这无疑会对我造成很大的损失.

于是我决定写一个 python 脚本来自动检测网络,然后自动重连校园网.以下时源码,

```python
from selenium import webdriver
from selenium.webdriver.chrome.options import Options

import requests
import time

# 设置 Chrome 无头模式
chrome_options = Options()
chrome_options.add_argument('--headless')
chrome_options.add_argument('--disable-gpu')

# 登录界面
url = "http://210.37.41.236/eportal/index.jsp?wlanuserip=6b9e0b7cf1ba82f98927ab3dd58dfef5&wlanacname=ce7755baddb6cd2593ede4c17d854ca1&ssid=&nasip=7d60263d360a32aefa21b68e87982d7a&snmpagentip=&mac=ab225743a9a996c006024dd049800474&t=wireless-v2&url=2c0328164651e2b4f13b933ddf36628bea622dedcc302b30&apmac=&nasid=ce7755baddb6cd2593ede4c17d854ca1&vid=606ceeeed9248aad&port=a8318b3106364528&nasportid=f5eb983692924fa26e6431fe9df4835f22c9893813d335dd1c7d4d602b2b63697dd071dc9b821903"


def get_connect():
    driver = webdriver.Chrome(options=chrome_options)  # options=chrome_options
    driver.get(url)                                                 # 打开浏览器
    driver.find_element_by_name("username").send_keys("XXXXXX")     # 输入密码
    driver.find_element_by_name("pwd_tip").click()                  # 这里是一个坑 后面讲
    driver.find_element_by_name("pwd").send_keys("XXXXXX")          # 输入密码
    driver.find_element_by_id("selectDisname").click()              # 打开网络模式选择窗口
    driver.find_element_by_id("_service_0").click()                 # 选择外网
    driver.find_element_by_id("jizhummNo").click()                  # 选择记住密码
    driver.find_element_by_id("loginLink_div").click()              # 点击登录
    driver.close()                                                  # 关闭浏览器


count = 0
while True:                                         # 死循环
    try:
        time.sleep(1)                               # 休眠一秒
        requests.get("https://www.baidu.com")       # 通过请求百度 来判断网络状态
    except Exception:
        count += 1
        print(count)
        get_connect()                               # 一旦无法连接百度 便重新登录

```

这里有一个大坑, 一开始我期望,直接通过寻找 "pwd" 输入密码即可 但是 他会一直报错: 

```python
 message: element not interactable
```

不可交互 我一直不理解,谷歌,百度,了很久,没有解决办法,最后自己通过 Chrome 的 控制台 发现每次点击password ,"pwd" 的属性都会改变一点,但是我尝试 pwd.click() 时发现一样报错,我终于怀疑到 它上面的一个元素了 "pwd_tip" 只有点击一次它 , "pwd" 才能工作. 这个应该就是网站的保护机制吧,但总之 我成功了.

并且使用 pyinstaller 将其打包成了 exe 可执行文件

![2019-08-29_14-15-11deb589bcf315b88e.png](https://www.z4a.net/images/2019/08/29/2019-08-29_14-15-11deb589bcf315b88e.png)

如图 它一个白天 为我自动登陆了4次