---
title: 折腾utuntu的遇到的问题
date: 2018-03-20 14:39:27
tags:
---
# 折腾utuntu的遇到的问题
<!-- more -->
1. [sublimetext3中文输入法的问题（亲测可行）](http://blog.csdn.net/XiaoshaXs/article/details/51969055)
1. [navicat的中文乱码](http://blog.csdn.net/u010856630/article/details/52575581)
1. [navicat破解](http://blog.csdn.net/superit401/article/details/78110079)
1. [多线程下载工具--uget+aria2](http://burner1024.blog.163.com/blog/static/17447800420126191858424/)
1. [更换ubuntu主题](https://www.linuxprobe.com/ubuntu-16-04-lts-arc-gtk.html)
1. [使用Fillder进行抓包，直接在官网下载linux版本，使用mono运行](https://www.telerik.com/download/fiddler)
1. 在启动Fiddler时，会重置系统代理，所有在关闭后，要手动去开启代理
1. [学习vim](https://github.com/dofy/learn-vim)
1. [idea激活码](http://idea.lanyus.com/)
1. [idea的内存优化](http://blog.csdn.net/a491857321/article/details/72829205)
1. [ubuntu17.10 上传速度慢的问题](http://blog.csdn.net/u010934417/article/details/75043166),产生的原因是域名解析耗费时长过长，在hosts文件中加入自己的ip地址，如 192.168.2.47 MC ,后面的名称可以随便写，保存之后上传就可以了
1. idea可以在终端启动，但是创建快捷方式的时候，启动提示找不到JDK，可以参照[这个地方](https://www.zhihu.com/question/38162314?sort=created)
1. 搜狗输入法异常（包括无法切换输入法，自动变成双拼，无显示设置图标等等），通用的解决办法是结束掉fcitx（小企鹅）线程(`killall fcitx`)，结束掉搜狗线程（`sudo killall sogou-qimpanel`），删除搜狗的配置文件（在 `~/.config/` ，以sougou开头的三个文件），然后重启fcitx `fcitx & ` ,重启搜狗输入法 `sogou-qimpanel &`，应该就可以了