---
title: Thinkphp基于linux的坑
date: 2017-12-01 22:19:44
tags: linux
keywords: Thinkphp,linux,大小写
categories: "填坑"
---
## 关于Thinkphp的缓存
因为thinkphp会有一个runtime的缓存文件，而linux的文件默认没有写的权限，所以我们需要将文件设置为777即读写的权限。

## 关于Thinkphp的URL大小写敏感
Thinkphp5会默认将url转为小写，然后再linux系统中是区分大小写的url，这将会导致无法找到文件。  
所以在config添加一句'url_convert'=>false,就可以取消thinkphp的url自动转换为小写。