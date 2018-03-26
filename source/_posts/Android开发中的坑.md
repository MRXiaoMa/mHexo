---
title: Android开发中的坑
date: 2017-12-13 15:09:19
tags: 
    - Android
    - 组件化
---
# Android开发中遇到的坑
<!-- more -->

- 使用svg报错,需要在build.gradle中增加vector的兼容支持
  ```
    android {

    defaultConfig {
        vectorDrawables.useSupportLibrary = true
    }
   }
  ```
- 解决项目依赖冲突,可以使用gradle命令` dependencies `查看包依赖树,然后过滤掉重复的包(一般情况下gradle会自动处理依赖,遇到冲突时需要手动解决),解决方式如下示例如下
  ```
   compile ('com.android.support:design:22.2.1')
            {
                exclude group: 'com.android.support'
            }
  ```
- 使用room数据库框架时出现各种问题,一定要使用正式版本,不用用beta版,不要用beta,不要用beta
- 在android中使用三角函数 sin30°的写法为` Math.sin(30*Math.PI/180)`,pi就是π值,在角度值里面一个π等于180°,所以30°可以写成` 30*Math.pi/180`
- 自定义控件自定义属性时,同一个arrts里面不能含有相同的name,即使这两个name分属于不同的自定义控件,所以推荐name添加控件的前缀,如MView和YView同时含有一个叫name的属性,那么我们写的时候可以这样` <attr name="mview_name" format="integer"/>`和`   <attr name="yview_name" format="integer"/>`,可以避免折这个问题
- 自定义控件在scrollview中不显示,ondraw方法不执行.原因就在于scrollview中控件的大小都是自适应的,所以要在` onMeasure()`方法中,当测量模式`AT_MOST(不约束,marth)`和`UNSPECIFIED(最小值,wrap)`时,调用`setMeasuredDimension(width,height)`,从新设置宽度和高度
- 使用隐示意图跳转到自己定义的activity时,必须添加` <category android:name="android.intent.category.DEFAULT"/>`才能正常跳转,如
  ```
   <activity android:name=".activity.ProtocolActivity">
            <intent-filter>
                <action android:name="protocol_activity"/>
                <category android:name="android.intent.category.DEFAULT"/>
            </intent-filter>
        </activity>
  ```
- AndroidStudio 崩溃之后无法查看日志,可以设置显示模式为No filters,log等级设置为Warn,参考 [这个地方](https://www.zhihu.com/question/32024327)
- `Wrong state class, expecting View State but received class android.support.v7.widget.RecyclerView$Sa`错误,当在同一个activity中使用的三个fragment中出现了相同的id,状态互相覆盖,这种情况可以在布局中使用tag标签替换id
- 在使用google官方的tablayout时,动态导航条的长度,可以使用反射获取每一个item,然后根据屏幕宽度,item数量和item的宽度动态设置导航条的`leftMargin`和`rightMargin`,实现更改导航条的效果,参考[这个兄弟的](http://blog.csdn.net/u013134391/article/details/70833903)
- glide4.0中BitmapTransformation的写法有变化,具体可以参考其已经实现了的`RoundedCorners`,在配置自定义的GlideModule是,要在类上添加注解`@GlideModule`,_特别注意:如果要自定义glidemodule,必须要要引入`compile 'com.github.bumptech.glide:annotations:${version}'`,这个库会根据注解生成代码,然后就可以在在代码中使用`GlideApp.wite(mContext).load(src)......`_
- glide4.0无法加载网络图片,经过检查,是自定义的glideModule里面的 applyOptions方法实现由问题,正确的实现[参考这里](https://muyangmin.github.io/glide-docs-cn/doc/configuration.html)
- 华为手机log.d(),无法打印日志,要打开系统的日志功能,在拨号界面输入`*#*#2846579#*#*`,ProjectMenu---后台设置----LOG设置---LOG开关 点击打开
- AndroidStudio3.0 使用google()仓库被墙,可以更换成阿里云的景象,景象的地址是``
- 遇到support版本冲突.可以强制force版本.方法位
 ```
 configurations.all {
   resolutionStrategy.eachDependency { DependencyResolveDetails details ->
       def requested = details.requested
       if (requested.group == 'com.android.support') {
           if (!requested.name.startsWith("multidex")) {
               details.useVersion '24.1.0'
           }
       }
   }
}
 ```