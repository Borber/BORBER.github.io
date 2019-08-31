---
title: 'Linux Gridea repair'
date: 2019-06-17 13:47:08
tags: [Gridea,Linux,BUG]
published: true
hideInList: false
feature: https://www.z4a.net/images/2019/06/17/wlop-6.jpg
---
​		在我从原始的Hexo 管理博客,转向 **[Gridea](https://gridea.dev)** 时,我遇到了如下的错误:


<!-- more -->



![18.png](https://www.z4a.net/images/2019/06/17/18.png)

​		这是在我点击尝试远程连接时,调试台出现的报错信息.但是我不知道问题具体出在哪里,我尝试过与 **Gridea** 的官方人员进行交流,在进行了TeamViewer的远程协助之后,还是无法解决,但是在我询问官方人员,能否直接进行git初始化时,他回到道:“那样可能可以链接,但同步可能不行”,我意识到了这可能是一个正确的方向.

​		于是我成功了.

​		我的平台是: Manjaro KDE,Git



###   解决方案:


1.  按照官方的配置,设置好所有选项.

2.  进入 **Gridea** 的根目录 删除 output 文件夹 

    ```
    rm -rf optput
    ```

    

3.  将你将要部署的仓库clone到 **Gridea** 根目录下 

    ```
    git clone git@github.com:NAME/RNAME.git
    ```

    

4.  修改 clone到本地的仓库文件夹名 为 output

    ```
    mv RNAME output
    ```

    

5.  测试连接性 : <mark oncopy=" ">成功</mark>



以上.

​		以及在使用 **Gridea** 部署时出现网站显示效果与本地预览不一致时,请尝试使用浏览器无痕模式访问查看.如果是正确的那么是OK的.等一段时间,正常的浏览也会变回正确样式

$\color{DarkTurquoise}{以及:}$  在自定义设置中设置 rss 链接为 /atom.xml 就好