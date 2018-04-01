---
title: ubuntu搭建环境
date: 2018-04-01 12:33:38
tags: ubuntu
---
# 折腾ubuntu
## 这里使用的ubuntu版本是16.04,推荐使用LTS长期支持版，开发板有很多的小问题，如果是初次接触ubuntu，在这些问题上会浪费很久时间（网络，驱动，中文，奇葩的小问题），但是搜索之后都差不多能够解决，这就看个人了

<!-- more -->

1. ubuntu的默认分辨率没有1920x1080的，要手动添加分辨率
   - xrandr命令查看自己的分辨率信息，记住自己的显示器代号，（VGA或Virturl或者DVI-I-1等等）
   - cvt可以自定义一个分辨率，如`cvt 1920 1080 60`，返回结果如下    
       ```
       1920x1080 59.96 Hz (CVT 2.07M9)   hsync: 67.16 kHz; pclk: 173.00 MHz
       Modeline "1920x1080_60.00"  173.00 1920 2048 2248 2576  1080 1083 1088 1120 -hsync +vsync
       ```
   - 使用`xrandr --newmode`增加这个上面的分辨率
       ```
       xrandr --newmode "1920x1080_60.00" 173.00  1920 2048 2248 2576  1080 1083 1088 1120 -hsync +vsync
       ```
   - `xrandr --addmode`增加这个分辨率到显示器上面
       ```
       xrandr --addmode DVI-I-1 "1920x1080_60.00"
       ```    
     注意这个地方的DVI-I-1代表显示器，具体的值要根据`xrandr`返回的值来设置，到这一步，我们的显示器分辨率已经改好了，但是现在只是这一次有效，重启电脑后就有变回来了，所以接下来    
    - 添加到开机启动,`vi ~/.profile`,在后面添加
        ```
        xrandr --newmode "1920x1080_60.00" 173.00  1920 2048 2248 2576  1080 1083 1088 1120 -hsync +vsync
        xrandr --addmode DVI-I-1 "1920x1080_60.00"
        ```
       重启电脑，OK
1. 安装git  
    ```
    sudo apt-install git   
    ```
1. 安装nodeJs   
这里使用nvm来安装node.js    
    - 安装nvm   
        ```
        wget -qO- https://raw.githubusercontent.com/creationix/nvm/v0.33.0/install.sh | bash
        ```
        重启终端
    - 安装nodeJs
        ```
        nvm install 8.10
        ```
        最后的版本好可以通过 `nvm ls-remote` 查询，这里可能下载很慢，我们可以把tar包下载下来，放到nvm的缓存目录中
1. 安装vim `sudo apt-get install vim`
1. 安装SS
    - 安装SS，可以参照 [这里](https://www.jianshu.com/p/0cfb43874a72)
    - 安装PAC 参考 [这里](https://blog.csdn.net/u012810317/article/details/52139361)
        ```
        sudo pip install genpac
        sudo genpac --proxy="SOCKS5 127.0.0.1:6677" -o autoproxy.pac--gfwlist-url="https://raw.githubusercontent.com/gfwlist/gfwlist/master/gfwlist.txt"
        ```
    - 设置启动代理方式  
     系统设置 --> 网络 --> 网络代理     
     “方法”选择“自动”
     “配置URL”填写 `file:///etc/autoproxy.pac`
    - 终端翻墙 
        - 安装polipo
            ```
            sudo apt-get install polipo
            ```
        - 修改配置文件
            ```
            $ cd /etc/polipo/
            $ sudo chmod 777 config # 为config文件申请最高权限
            $ vi /etc/polipo/config
            ```     
            然后在config里面加入下面三句话
            ```
            socksParentProxy = "localhost:1080"
            socksProxyType = socks5
            logLevel=4
            ```
        - 关闭启动poplipo
            ```
            sudo service polipo stop
            sudo service polipo start
            ```
        - 验证
            ```
            http_proxy=http://localhost:8123 curl ip.gs#查询你的IP地址和地理信息
            ```
            这个地方可以看到查询到的位置已经到了美国
        - 设置别名简化
            ```
            vi .bashrc
            alias hp="http_proxy=http://localhost:8123" 
            ```
            执行` source ~/.bashrc` 更新操作
        - 测试
            ```
            hp curl ip.gs
            ```
            可以看到已经切换到了美国
        - 如果需要变成全局代理,可以修改 .branrc文件,具体操作 [查看这里](https://blog.csdn.net/jesse_mx/article/details/52863204)
1. 安装搜狗输入法 `https://pinyin.sogou.com/linux/`，直接运行或者`dpkg -i`安装，重启电脑
1. 安装chrome,直接下载安装就好
1. 安装JDK  
    - 官网下载jdk
    - 解压到合适的目录
    - 设置环境变量  
        ```
        export JAVA_HOME=/home/mc/dev/java/jdk1.8.0_161
        export JRE_HOME=${JAVA_HOME}/jre
        export CLASSPATH=.:${JAVA_HOME}/lib:${JRE_HOME}/lib
        export PATH=${JAVA_HOME}/bin:$PATH
        ```
    - 刷新 `source ~/.bashrc `
1. 安装Studio,官网下载,注意gradle下载很慢,可以下载下来放到 `~/.gradle`目录.
1. 安装微信，钉钉，wps等
    - 安装wps 官网下载更新
    - 安装微信,可以使用[这个版本](https://github.com/geeeeeeeeek/electronic-wechat)
    - 安装钉钉,ty
1. 安装Idea
1. 安装tomcat
