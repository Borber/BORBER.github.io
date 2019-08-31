---
title: 'Add Aplayer'
date: 2019-08-03 16:11:22
tags: [音乐,Gridea,美化]
published: true
hideInList: false
feature: https://www.z4a.net/images/2019/08/03/MoonAndNight-4k-wallpaper.jpg
---
Gridea 添加 Aplayer 音乐播放插件

<!-- more -->

## 教程：

1. 在head.ejs中添加

```html
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/aplayer/1.10.1/APlayer.min.css">

```

2. 在footer.ejs中添加

```html
<script src="https://cdn.jsdelivr.net/npm/color-thief-don@2.0.2/src/color-thief.js"></script>
<script src="https://cdn.jsdelivr.net/npm/meting@1.1.0/dist/Meting.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/aplayer/1.10.1/APlayer.min.js"></script>

```

3. 以下是相应的插入代码， 吸底模式可以在 body的任意地方 推荐顶部（效果可在本博客首页左下角查看） ， 其他的就是在对应位置 可以在 md文件中插入使用 内联html 即 **在文章中插入音乐**

```html
<!-- 吸底模式 默认播放表列隐藏 如需默认显示 删除 aplayer-narrow 即可 -->
  <div id="aplayer9" class="aplayer aplayer-fixed aplayer-narrow" data-id="" data-server=”netease" data-type="playlist" data-autoplay=”true” data-mode=”circulation”></div>
<!-- 迷你模式 -->
  <div id="aplayer6" class="aplayer aplayer-narrow" data-id="" data-server=”netease" data-type="playlist" data-autoplay=”true” data-mode=”circulation”></div>
<!-- 列表模式 -->
  <div id="aplayer5" class="aplayer aplayer-withlrc aplayer-withlist" data-id="" data-server=”netease" data-type="playlist" data-autoplay=”true” data-mode=”circulation”></div>

```



### 参数配置如下：

1. data-id: 歌曲/专辑/歌单对应的id。注意这里需要是歌曲原本的id,不是你自己歌单中点击后显示的。 （必须）
2. data-server: 音乐平台， 大致支持以下几个，我只测了一下网易音乐和虾米音乐。（必须）

- netease(网易云音乐)
- tecent(qq音乐)
- xiami(虾米音乐)
- kugou(酷狗音乐)

1. data-type:请求类型（必须）
   - song(单曲)
   - album(专辑)
   - playlist(歌单)
   - search(搜索)
2. data-mode: 播放模式(可选)
   - random(随即)
   - single(单曲)
   - circulation(列表循环)
   - order(列表)
3. data-autoplay: 自动播放(可选)
   - false
   - true



歌曲id 参见下图

![1607ae71f0bd3abd9.png](https://www.z4a.net/images/2019/08/03/1607ae71f0bd3abd9.png)

### 效果

<div id="aplayer5" class="aplayer aplayer-withlrc aplayer-withlist" data-id="2748492595" data-server=”netease" data-type="playlist" data-autoplay=”false” data-mode=”circulation”></div>

																																																																	 https://cloud.tencent.com/developer/support-plan?invite_code=3ddc7ex0dku8o