---
title: gitbash配置及连接github
date: 2017-11-02 14:18:20
tags: Gitbash
keywords: git,gitbash,gitbash配置,git环境搭建,github连接
categories: "环境"
---
### Git有什么用?  
为什么要搭建Git环境? 
>-因为要把本地文件提交到远程仓库(gitbash,码云等)   

版本库有什么用?
>-类似一个目录，每个文件的修改，删除都能够记录，并且在以后以还原。

<!--more-->
### 搭建Git环境
Git是一款免费、开源的分布式版本控制系统，用于敏捷高效地处理任何或大或小的项目。
#### 下载Git安装包
在Git官网：[https://git-scm.com/](https://git-scm.com/) 下载安装包 Git-2.15.0-64-bit.exe
![](https://github.com/yuhongjing/img-folder/raw/master/img/download_git.png)  
![](https://github.com/yuhongjing/img-folder/raw/master/img/download_git_1.png)  
#### 测试安装正确
桌面右键，打开 Git Bush Here，输入 git --version，出现版本号则说明 Git 环境配置成功，第二步完成！！！
![](https://github.com/yuhongjing/img-folder/raw/master/img/git_version.png)  
#### 配置本机的Git
```
    $ git config --global user.name "你的名字"
    $ git config --global user.email "你的邮箱"
```
#### 生成密匙
```
    $ ssh-keygen -t rsa -C "邮箱同上" 
```
#### 复制密匙
在ｃ盘用户.ssh文件下用文本编辑器打开id_rsa.pub并复制文件的内容。
![](https://github.com/yuhongjing/img-folder/raw/master/img/git_key.png)
#### GitHub注册和配置
GitHub 是一个代码托管平台，因为只支持 Git 作为唯一的版本库格式进行托管，故名 GitHub。  
Github注册：[https://github.com/](https://github.com/)  
![](https://github.com/yuhongjing/img-folder/raw/master/img/github.png)
#### 提交公匙
点击用户下Settings的SSH and GPG keys下New SSH key添加之前的密匙复制进内容就可以了。
![](https://github.com/yuhongjing/img-folder/raw/master/img/git_key_commit.png)
### 连接完成测试
```
    $ssh git@github.com
```
输入代码如果不报错就说明配置完成!

Git使用教程可搜索廖雪峰教程！  
廖雪峰:[https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)



    

 
    
    
