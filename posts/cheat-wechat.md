---
title: 'Cheat wechat'
date: 2019-08-26 10:50:23
tags: [python,API,json]
published: true
hideInList: false
feature: https://www.z4a.net/images/2019/08/26/IMG_20190826_105609.jpg
---
调用 API 刷微信步数

<!-- more -->


 转自此文  **[微信刷步 云自动刷版本 带API 一键天天霸榜](https://www.52pojie.cn/thread-1014157-1-1.html)** 

#### 使用方法：

1. 下载卓易健康 然后注册账号（推荐使用数字注册）

2. 卓易健康上关联微信

3. 下载程序 输入你的注册的账号 (注意 这里说的账号 就是 卓易健康的==用户名==)  和 你要刷的步数

    1-35000 自定义填写（固定的）
    -1 是直接 98800
    -2 是 25000-35000 随机



以下是 python实现.

```python
import requests
name = input("User Name:")
js = {
    "method": "register",
    "username": name,
    "walk": -1
}
requests.post("http://149.129.116.219/api-wechat-operation", json=js)
json = requests.get(f"http://149.129.116.219/api-wechat-operation-username-{name}").json()
print(json)
```

4. 运行程序 输入卓易健康的用户名即可 {注意 一定要绑定微信 ... 不然你刷个啥啊}

5. 愉快的装逼吧.

    ![Screenshot_2019-08-26-10-52-47-183_com.tencent.mm.jpg](https://www.z4a.net/images/2019/08/26/Screenshot_2019-08-26-10-52-47-183_com.tencent.mm.jpg)

    

按照 原文作者的说法 应该是 一次使用 ,天天帮你刷.