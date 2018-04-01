---
title: ubuntu分辨率不能调整的问题
date: 2018-04-01 12:33:16
tags: ubuntu
---

# ubuntu分辨率无法设置为1920x1080

<!-- more -->
## [参考这里](http://blog.sina.com.cn/s/blog_49f914ab0100hd38.html)
### 电脑是双显卡（gtx960显卡），系统是ubuntu16.04


 直接开门见山，我的解决方法是修改 `/etc/X11/xorg.conf`文件里面的 HorizSync（行频）和 VertRefresh（场频）， 这个每个显示器都会有这个参数，可以在厂商得到，真心没想到，最后的原因居然是这个。

 **HorizSync和VertRefresh不能乱改，不能乱改，不能乱改，一定要是确切的得到参数，在xorg.conf文件修改如下内容**
 ```
 Section "Monitor"
    Identifier     "Monitor0"
    HorizSync       30-83
    VertRefresh     56-76
    ModeLine       "1920x1080_60.00" 173.00 1920 2048 2248 2576 1080 1083 1088 1120 -hsync +vsync
    Option         "PreferredMode" "1920x1080_60.00"
EndSection
 ```
 经过验证，只需要修改 `HorizSync`和`VertRefresh`这两个参数就可以，关于这`xorg.cong`文件的说明参考文章开头的引用。

 
 
修改完成之后，重启，你就会发现在显示里面可以看到1920x1080这个分辨率了，接下来，来看下这个分辨率是如何坑了我好几天的。

- 安装ubuntu后，发现每次启动的时候屏幕都要花一下，经过goole后，查看自己的设备信息，发现一直使用的集成显卡，要使用独显要安装驱动
- 驱动选择nvidia的专业驱动，这里推荐大家安装nvidia的专业驱动，**这里如果使用社区的驱动，后面有大坑，故不推荐使用**，关于社区驱动和专业驱动，请自行百度，驱动安装过程不表，基本都是一下小问题，大家搜一艘都是可以解决的
- happy的重启后，发现分辨率变成了1080x768,本来想着再用 `xrander`添加一次就好了嘛。。事实证明我还是太年轻了，在执行到最后一部的时候 `xrander --addmode DVI-I-0 "1920x1080_60.00"`的时候，报错了，大致意思是该分辨率不能匹配屏幕。
- 开始goole，baidu，有让重新装驱动的，有让改xorg.cong文件的，有说是VGA连接线有问题的，然后这些说法，都不能解决（其中的心酸就不说了），就在绝望的时候发现了[这个文章](http://blog.sina.com.cn/s/blog_49f914ab0100hd38.html),文章时间虽然久远，但是道理讲的透彻
- 按照博文的说法，增加了modeLine和modes，重启发现无法解决，然后看到了这句话  `依我的看法，在获取到了正确的行频HorizSync 和场频VertRefresh之后，Modeline选项已没有多少意义，可以不写`，去网上查了我这个屏幕的参数，设置上去，重启，果然更高的分辨率就出来了！[分辨率图](/home/mc/图片/fen.png)
- 其实，最开始，错误日志都提醒我们了，不匹配，可是还是饶了一个大圈才解决问题。
