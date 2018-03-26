---
title: Andorid代码片段收集
date: 2017-12-26 17:52:40
tags:
    - Andorid
    - Java
---

# Android代码片段收集
<!-- more -->
1. rxjava实现点击两次退出应用
    ```
     PublishSubject<Integer> backStream=PublishSubject.create();
    @Override
    public void onBackPressed() {
        if (backStream.hasObservers()){
            backStream.onNext(1);
        }
        else {
            backStream.timeInterval().subscribe(integerTimed -> {
                if (integerTimed.time(TimeUnit.SECONDS)<2){
                    HomeActivity.super.onBackPressed();
                }else{
                    ToastUtils.showShort("再按一次退出");
                }
            });
            ToastUtils.showShort("再按一次退出");
        }
    }
    ```
2. 关于异常捕获和空判断
    ```
        public void updateDocInfo(long id){
        Document doc=null;
        try{
        doc=getDocById(id);
        }catch(Exception e){
        log.error("get document error",e);
        }
       if(doc!=null){
       log.into("update doc,id");
        doUpdateDoc(doc);
       }
       }
    ```
    尽量避免这样的代码,捕获了异常只打印了日志,如果出现异常,调试的视乎完全不知道走到那里去了,什么错误都不会报,导致调试bug浪费时间,针对这种情况
    - 直接把异常抛出去,早点蹦掉,早点解决,否则等到上线后才出现这个问题,得不偿失
    - 下方的非空判断一定要加else语句,在里面一定要有反馈

