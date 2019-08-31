---
title: 'IRC with HexChat'
date: 2019-08-22 21:29:32
tags: [聊天,IRC,软件]
published: true
hideInList: false
feature: https://www.z4a.net/images/2019/08/22/8.png
---
[IRC](https://zh.wikipedia.org/wiki/IRC) 主要用于群体聊天，但也可以用于个人的聊天

<!-- more -->

### 介绍:

 IRC 一般用于 专业团体 及 开源社区讨论,当然 也有小圈子的讨论组.详情请见 [维基百科](https://zh.wikipedia.org/wiki/IRC)

 IRC 可以完全匿名,也没有监控.你只需要遵守你参与的频道的规则即可.这也意味着你可以自己创建一个频道 不受任何人的监管.他不要求你的手机号 甚至某种概念下你也不需要一个邮箱 ,因为 你可以在不注册时使用任何一个未被注册的名字作为临时名字. 当然了 使用一个匿名邮箱来注册一个常用名字才是明智之选.(请注意 是匿名邮箱 而非临时邮箱)


### IRC 注册:

首先安装 [HexChat](https://hexchat.github.io) 全平台支持 并且免费(Windows 平台 可选择付费 两版本无差别)

![1531970365866ed08.png](https://www.z4a.net/images/2019/08/22/1531970365866ed08.png)

点击连接 一般都是直接freenode 服务器

![2edec82672f97351d.png](https://www.z4a.net/images/2019/08/22/2edec82672f97351d.png)

在这里输入下面的代码

```sh
/nick "your name"
/msg nickserv register "密码" "邮件地址"

#会有邮件输入邮件中的命令 

/msg NickServ VERIFY REGISTER "XXX" "XXXXXXXX"
```

然后每次登录 都会提示你 需要激活才能使用

```shell
#用下面这条命令验证你的身份
/msg NickServ identify "password"
```

### HexChat 汉化:

![3905330441d5440d3.png](https://www.z4a.net/images/2019/08/22/3905330441d5440d3.png)

![447e31806a0438675.png](https://www.z4a.net/images/2019/08/22/447e31806a0438675.png)

如图设置即可

### 加入频道:

选择 -> 服务器 -> Channel list 

![52e6217ddbde4e986.png](https://www.z4a.net/images/2019/08/22/52e6217ddbde4e986.png)

选择一个加入即可 (如果没有显示 点击一下 搜索)

### 中文乱码:

![6217c0d66a43785b1.png](https://www.z4a.net/images/2019/08/22/6217c0d66a43785b1.png)

![72af7f5c7e5ff8ead.png](https://www.z4a.net/images/2019/08/22/72af7f5c7e5ff8ead.png)

字体设置成微软雅黑就好

![8.png](https://www.z4a.net/images/2019/08/22/8.png)

搞定

以后 可能会有进阶的使用技巧更新