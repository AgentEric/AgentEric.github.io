---
title: Manjaro Chrome54+ Flash不能使用的解决办法
date: 2017-01-16 22:58:32
updated: 2017-02-06 22:58:32
categories:
- 技术
tags: 工具
---

最近一直在用 [Manjaro-Linux](https://manjaro.org/)，越用越来越爱上它了……给大家安利一下。
不过，刚开始用它的时候，很惊喜也有点郁闷，因为它安装的Chrome都是最新版Chrome54+，默认不再开启Flash Player。对于绝大多数小白来说，这是最紧要的。更重要的是在网上没有相对应的解决办法（我是指针对Manjaro系统），所以在我解决之后，我决定写一篇博文，供大家提供参考。
<!--more-->
On Manjaro(or otherwise Linux System)
1.If you have installed PeperFlash(If you haven't installed,jump to step 2 )如果你已经安装Flash，如果没有请直接看第二步
Open Chrome,In the address bar,type **chrome:plugins** to open the Plug-inspage.打开Chrome，在地址栏输入“chrome:plugins”，打开插件页面。

![chrome-plugins.jpg](http://upload-images.jianshu.io/upload_images/877666-9aef236ef8a19d29.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

On the Plug-ins screen that appears, find the Adobe Flash Player listing. Check the status (Enabled or Disabled).在打开的插件页面，找到Flash，检查Flash的状态，是否允许运行。 
Select **Always allowed to run** to always allow Flash Player to run.选择总是允许运行。
Close the Plug-ins screen,restart Chrome.关闭插件页面，重启Chrome。
2.Install PepperFlash First
在manjaro中使用包管理器搜索PepperFlash，点击安装即可。

![location](http://upload-images.jianshu.io/upload_images/877666-26486f55ad6e83df.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

进入PepperFlash安装路径，里面有两个文件libpepflashplayer.so和manifest.json，记住这两个文件的路径，一会儿我们要copy这个文件到chrome目录下。

![location1.png](http://upload-images.jianshu.io/upload_images/877666-4712db3c7a273dca.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![terminalpepperflash.png](http://upload-images.jianshu.io/upload_images/877666-114286cc670eea13.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

进入terminl,输入su -l 进入root权限。

进入chrome路径，如下图所示，使用命令mkdir PepperFlash创建文件夹
cd PepperFlasha	进入文件夹

![chromelocation.png](http://upload-images.jianshu.io/upload_images/877666-b6377fcd8192bed9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

cp XXX.../libpepflashplayer.so .	将libpepflashplayer.so文件copy到当前路径(.代表拷贝到当前目录)
cp XXX.../manifest.json .			将manifest.json拷贝到当前路径

cd /usr/share/applications 
vim google-chrome.desktop		使用vim打开google-chrome.desktop，在所有的/usr/bin/google-chrome-stable 后面添加命令 --ppapi-flash-path=/opt/google/chrome/PepperFlash/libpepflashplayer.so，保存退出。

**所有操作可能需要root权限，su -l**，请务必保证安装了vim文本编辑工具。

重启Chrome，检查第一步，插件页面是否开启了Flash插件。

经过这一系列操作，你的Chrome已经可以调用Flash了，你又可以快乐地看美剧啦！