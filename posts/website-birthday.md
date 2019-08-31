---
title: 'Website birthday'
date: 2019-08-30 00:59:27
tags: [Gridea,美化,json]
published: true
hideInList: false
feature: https://www.z4a.net/images/2019/08/30/2019-08-30_01-01-32.png
---
Gridea 主题 添加 网站已稳定运行：XX 天 XX 时 XX 分 XX 秒

<!-- more -->


###  birthday.ejs:

在主题的include 文件夹下 新建 birthday.ejs 将下面的代码复制进去.

```js

<% if (site.customConfig['BirthDay']) { %>
    <!--网站稳定运行代码-->
    网站已稳定运行：<span id="website_running_time" style="color: #00BFFF;"><font style="color:#FFF">398</font> 天 <font style="color:#FFF">17</font> 时 <font style="color:#FFF">28</font> 分 <font style="color:#FFF">54</font> 秒</span>
    <script language="javascript">
        function show_date_time(){
            window.setTimeout("show_date_time()", 1000);
            BirthDay=new Date("<%= site.customConfig['BirthDay'] %>");
            today=new Date();
            timeold=(today.getTime()-BirthDay.getTime());
            sectimeold=timeold/1000
            secondsold=Math.floor(sectimeold);
            msPerDay=24*60*60*1000
            e_daysold=timeold/msPerDay
            daysold=Math.floor(e_daysold);
            e_hrsold=(e_daysold-daysold)*24;
            hrsold=Math.floor(e_hrsold);
            e_minsold=(e_hrsold-hrsold)*60;
            minsold=Math.floor((e_hrsold-hrsold)*60);
            seconds=Math.floor((e_minsold-minsold)*60);
            website_running_time.innerHTML='<font style=color:#FFF>'+daysold+'</font> 天 <font style=color:#FFF>'+hrsold+'</font> 时 <font style=color:#FFF>'+minsold+'</font> 分 <font style=color:#FFF>'+seconds+'</font> 秒';}
        show_date_time();
    </script>
<% } %>
```



### config.json:

然后 在你的 主题config.json中 添加下面一段配置:

```json
{
      "name": "BirthDay",
      "label": "建站日期 | 用于显示 网站已经稳定运行 XX 天 XX 时 XX 分",
      "group": "个性化",
      "value": "",
      "type": "input",
      "note": "6/17/2019 00:23:23"
    },
```

除了 name,type 其他你都可以改

然后在你的 footer.ejs 中的合适位置中 加入下方代码(我推荐在 <%-themeConfig.footerInfo%> 上方加入)

```ejs
<%- include('./birthday') %>
```

如图

![2019-08-30_00-54-17.png](https://www.z4a.net/images/2019/08/30/2019-08-30_00-54-17.png)

### USE:

重启客户端 填写你网站的生日并保存:

![2019-08-30_00-55-34.png](https://www.z4a.net/images/2019/08/30/2019-08-30_00-55-34.png)

> 月/日/年 "空格" 时:分:秒

然后预览一下看看效果 就可以点同步了