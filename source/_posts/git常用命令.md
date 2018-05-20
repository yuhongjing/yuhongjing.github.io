---
title: git常用命令
date: 2018-04-07 22:26:00
tags: Gitbash
keywords: git,gitbash,gitbash命令
categories: "技术"
---
# Git的常用命令
配置全局用户NAME和E-mail  
> $ git config --global user.name "Your Name"  
> $ git config --global user.email "email@example.com"   
   
<!--more-->

仓库初始化  
> $ git init  

添加文件到仓库 
> $ git add 文件名  

提示：可反复添加。一个小数点为所有文件。 

提交到git仓库  
> $ git commit -m "注释"  

查看仓库状态  
> $ git status  

比较当前的文件修改  
> $ git diff 文件名  

查看提交历史  
> $ git log  --pretty=oneline  

回退版本  
> $ git reset --hard HEAD^  

删除文件  
> $ rm 文件名  

与远程仓库协作  
> $ git remote add origin git地址  

删除本地库与远程库的关联  
> $ git remote rm origin  

推送到远程仓库  
> $ git push origin 分支名  

克隆一个远程库  
> $ git clone git地址  

创建一个分支  
> $ git branch 分支名  

切换分支  
> $ git checkout 分支名  

创建并切换一个分支  
> $ git checkout -b 分支名  

查看分支  
> $ git branch  

合并分支到当前
> $ git merge 分支名  

删除分支  
> $ git branch -d 分支名  



