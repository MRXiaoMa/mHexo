---
title: flutter环境搭建
date: 2017-12-25 14:59:45
tags:
    - flutter
    - dark
---

# flutter环境搭建

<!-- more -->

1. 安装flutter,运行`git clone https://github.com/flutter/flutter.git`
2. 添加环境变量到flutter的bin目录
3. 使用`flutter doctor`安装依赖,_注意,这个地方需要科学上网或者使用国内的源_
    - 使用国内的源,添加环境变量`PUB_HOSTED_URL=https://pub.flutter-io.cn`和`FLUTTER_STORAGE_BASE_URL=https://storage.flutter-io.cn`,重启终端运行,[参考这里](http://flutter-dev.com/bbs/topic/46/flutter-%E5%9B%BD%E5%86%85%E9%95%9C%E5%83%8F%E9%85%8D%E7%BD%AE%E6%96%B9%E6%B3%95)
    - 下载成功后终端报错`Error: Unable to 'pub upgrade' flutter tool. Retrying in five seconds..`,[参考这里](https://github.com/flutter/flutter/issues/12666),要把`$cachePath`文件夹移动的`bin`下的`cache`目录中,`$cachePath`如果不存在,可以把项目删除,从新clone
