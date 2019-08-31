---
title: 'Chat robot'
date: 2019-08-16 17:36:07
tags: [python,编程,测试,json]
published: true
hideInList: false
feature: https://www.z4a.net/images/2019/08/16/2019-08-16_17-38-40.png
---
测试 json 的解析

<!-- more -->

利用聊天机器人API  8 行代码 写一个AI聊天机器人

```python
import requests
print("开始聊天吧:")
while True:
    msg = input()
    if msg == "退出":
        break
    url = f'http://api.qingyunke.com/api.php?key=free&appid=0&msg={msg}'
    print(requests.get(url).json()['content'])
```

看起来智商不太高的样子

![2019-08-16_17-32-55.png](https://www.z4a.net/images/2019/08/16/2019-08-16_17-32-55.png)