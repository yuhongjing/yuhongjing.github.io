---
title: 单电脑管理多github账户
date: 2018-05-26 15:17:39
tags: SSH
keywords: SSH,github,多用户管理
categories: "环境配置"
---
### 前言
有些时候，可能需要一台电脑连接两个github的账号，或者一台电脑同时需要连接两个平台，例如码云，github等。所以这个时候我们需要在一台电脑上配置多个SSH-Key。
<!--more-->
### 建立多个SSH
首先需要生成多个SSH-key,例如下面就生成了两个SSH-key  
```
$ ssh-keygen -t rsa -C "one@gmail.com"

$ ssh-keygen -t rsa -C "two@gmail.com"
```
ps: 不要一直按enter，需要新的命名，否则会覆盖。(默认文件名为id_rsa)  
### 添加私钥
#### 打开ssh-agent
如果你是github官方的bash：  
`$ ssh-agent -s`
如果你是其它，比如msysgit：  
`$ eval $(ssh-agent -s)`
#### 添加私钥
```
$ ssh-add ~/.ssh/id_rsa_one

$ ssh-add ~/.ssh/id_rsa_two
```
### 创建config配置
在建立的config文件下添加如下代码
```
Host github.com
  HostName github.com
  IdentityFile ~/.ssh/id_rsa

Host pxy.github.com
  HostName github.com
  IdentityFile ~/.ssh/id_rsa_pxy
```
### 部署SSH key
在网站的SSH上面把文件名为*.pub的内容复制进入即可。
### 远程调试测试
```
$ ssh –T one.github.com

$ ssh –T two.github.com
```
### 使用方式
#### 注销全局用户配置
首先注册全局用户的配置，然后进入文件单独配置。
```
git config --unset --global user.name
git config --unset --global user.eamil
```
#### 使用的区别
原本的使用方式  
`$ git clone git@github.com: one的用户名/learngit.git`
现在的使用方式
```
$ git clone git@github.com: one的用户名/learngit.git

$ git clone git@pxy.github.com: two的用户名/learngit.git
```
ps.@后面的地址为我们config配置的Host字段值。从而区分是哪一个用户的。
### 总结
好吧，还是有点坑的了。不过玩过一次后，理清楚顺序后，还是比较清晰的。

