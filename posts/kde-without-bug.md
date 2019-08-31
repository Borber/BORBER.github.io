---
title: 'KDE without BUG'
date: 2019-06-17 18:00:43
tags: [Manjaro,KDE,Linux,桌面,BUG]
published: true
hideInList: false
feature: https://www.z4a.net/images/2019/06/17/LonelyParade.jpg
---
​		本文旨在收集Manjaro KDE 系统在日常使用中的BUG解决办法.与君共享.

<!-- more -->

​		在 KDE的日常使用中,不免会有很多的BUG,这其中有一部分是Linux系统本身的不和谐导致的.但是不可否认的是,有一部分就是因为简单的打包不当,或者因为一个特殊的设置原因罢了.


1.  搜狗输入法 安装 及 BUG 修复

    ```bash
    #使用 yay 包管理
    sudo pacman -S yay
    #下面的默认全选
    sudo yay -S fcitx-sogoupinyin fcitx-configtool fcitx-im
    #因为源的问题 往后如果恢复 可不做
    sudo pacman -U https://arch-archive.tuna.tsinghua.edu.cn/2019/04-29/community/os/x86_64/fcitx-qt4-4.2.9.6-1-x86_64.pkg.tar.xz
    #建议写入 .xprofile 没有的话 就没关系 vim会自己创建
    vim ~/.xprofie
    #在文件末尾写入以下三行：
    GTK_IM_MODULE=fcitx
    QT_IM_MODULE=fcitx
    XMODIFIERS="@im=fcitx"
    按 ESC 
    输入 :wq 回车
    #要是重启后搜狗还是麻烦用要是重启后搜狗还是麻烦用，应该是少了fcitx-qt4，
    #执行下面的命令
    sudo yay -S fcitx-qt4
    reboot
    ```

    

2.  deepin.com.qq.office 无法启动 (其他基于deepin-wine的同理)

    ```bash
    yay -S gnome-settings-daemon
    sudo cp /etc/xdg/autostart/org.gnome.SettingsDaemon.XSettings.desktop ~/.config/autostart/
    
    #将GNOME Setting的自启动选项打上勾即可。
    ```

    

3.  网易云音乐 无法输入中文

    ```bash
    vim /usr/share/applications/netease-cloud-music.desktop
    #修改
    Exec=/opt/netease/netease-cloud-music/netease-cloud-music %U
    yay -S vlc
    rebooot
    ```

    

4.  Deepin-TIM或Deepin-QQ调整界面DPI字体大小的方法

    ```bash
    #首先退出 QQ 或 TIM
    #进 gotop dd 可以彻底关闭
    nv WINEPREFIX="$HOME/.deepinwine/Deepin-TIM" winecfg
    #显示 中 设置dpi 建议120
    ```

5.  科学上网 [下载地址](https://github.com/shadowsocksrr/electron-ssr/releases/download/v0.2.7/electron-ssr-0.2.7.tar.gz) 

    ```bash
    #先下载文件进入下载目录
    yay -U electron-ssr-0.2.7.tar.gz
    ```

6.  远程协助软件 TeamViewer 无法连接

    ```bash
    sudo systemctl enable teamviewerd
    reboot
    ```

7.  Manjaro安装virtualbox并安装扩展

    ```bash
    #包管理器搜索virtualbox
    #安装一下包
    #Oracle VM VirtualBox (virtualbox)
    virtualbox-ext-oracle
    linux XXX(内核版本)-virtualbox-guest-mmodules
    linux XXX(内核版本)-virtualbox-host-mmodules
    #扩展包已经安装但是需要设置
    sudo gpasswd -a $USER vboxusers
    sudo modprobe vboxdrv
    reboot
    ```

    待续

    

    ​    解决方法部分来自 网络 部分来自 QQ群: [478058928](https://jq.qq.com/?_wv=1027&k=5zjyKCP) [Manjaro-Linux交流群] 在此感谢