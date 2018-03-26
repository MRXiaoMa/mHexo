---
title: linux学习中遇到的问题
date: 2017-12-20 18:56:37
updated: 2017-12-22 11:19:52
tags: linux
---

# linux学习中遇到的问题
<!-- more -->
1. 在给/etc设置权限777后,出现ssh不能连接的问题,使用`service ssh restart`时,服务器报错`Permissions 0777 for '/Users/username/.ssh/id_rsa' are too open.`,使用`chmod 400 ~/.ssh/id_rsa`设置权限为只读后恢复正常,在使用递归设置权限时,一点要小心
2. 在服务器上同时假设hexo(博客客户端)和gogs(git管理工具)时,如果使用同一个账户部署出现ssh冲突,导致gogs不能使用ssh,这时应该针对hexo和gogs分别建立账户,问题解决

