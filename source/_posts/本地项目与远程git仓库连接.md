---
title: 本地项目与远程git仓库连接
date: 2017-11-04 22:14:01
tags: Gitbash
keywords: Git,Github,Github连接远程仓库
categories: "环境"
---
1. 打开项目文件夹,输git init新建仓库,创建完会有一个.git文件夹   
2. 添加所有文件 git add .
3. 提交到本地仓库 git commit -m -a "备注信息"
4. 在远程仓库的项目下复制SSH
5. 本地仓库输入 git remote add origin (远程仓库的ssh) 连接远程仓库
6. 将本地项目推送到远程仓库 git push -u origin master

ps. 如果弹出bug，多半是本地没有README.md pull下来就行了。