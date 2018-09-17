---
title: Git clone
date: 2018-07-19 20:31:55
tags: Gitbash
keywords: git,gitbash,gitbash配置
categories: "技术"
---
### git clone 下载太慢的解决方式
设置代理的命令  
```
git config --global http.proxy http://127.0.0.1:34828
git config --global https.proxy https://127.0.0.1:34828
```
这个不需要设置sock5  
<!--more-->
取消代理的命令:  
```
git config --global --unset http.proxy
git config --global --unset https.proxy
```
也可以直接编辑git的设置文件，位置在用户目录下的`.gitconfig`,可能是隐藏文件
```
编辑如下
[https]
    proxy = https://127.0.0.1:34828
[http]
    proxy = http://127.0.0.1:34828    
```