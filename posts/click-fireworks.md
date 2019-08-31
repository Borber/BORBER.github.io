---
title: 'Click  fireworks'
date: 2019-08-03 15:56:21
tags: [Gridea,美化]
published: true
hideInList: false
feature: https://www.z4a.net/images/2019/08/03/1.png
---
Gridea 博客添加 点击 爆炸特效


<!-- more -->


将下方代码添加到 你当前使用主题的index.ejs 即可加入到首页，我推荐只将其加入到首页，文章页 尽量保持简洁。

```HTML
    <!--    点击爆炸特效 start-->
    <canvas class="fireworks" style="position: fixed;left: 0;top: 0;z-index: 1; pointer-events: none;" ></canvas>
    <script src="https://cdn.bootcss.com/animejs/2.2.0/anime.min.js"></script>
    <script src ="https://borber.cn/media/scripts/lib/fireworks.js"> </script>
    <!--    点击爆炸特效 ends-->

```

如果有问题的话 尝试添加下面这段代码到你的 head.ejs 

```html
<script src="https://cdn.bootcss.com/jquery/3.4.1/jquery.min.js"></script>

```

