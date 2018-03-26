---
title: 小程序wepy框架使用过程中的注意事项
date: 2017-12-05 14:52:45
tags: 
    - 微信小程序
---
# 小程序wepy框架使用过程中的注意事项
<!-- more-->
1. 组件的js类应该继承 ` wepy.component `
2. 动态传值和静态传值的区别
   - 静态传值    
   静态传值在组件端类型只能是string,在宿主端使用的是 _*静态的值*_
   - 动态传值
   动态传值组件端可以选择多种类型组合,如 ` [String,Int]`,设置默认值,设置反向绑定(`twoWay: true`),即组件数据反向绑定到宿主,在宿主端使用的是动态值(_data中的动态值_),使用`:prop1.sync`可以实现数据的绑定
3. [使用less来管理全局css的颜色等,使用参展官方less文档](http://www.bootcss.com/p/lesscss/),可以建立全局的page类,用来管理一些公共的颜色,样式,资源等
4. input组件的bindinput方法,取得value值是应该
```
  onChangeText(e) {
        console.log("获取到的value是", e.detail.value)
        return e.detail.value
      }        
```
  这个写法是用问题的(关键字错误)
```
  onChangeText(value,e){
    console.log("获取到的value是",value)
    return value
}
```
