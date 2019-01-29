---
title: win10配置bash
date: 2019-01-29 21:29:03
tags: bash
keywords: win10,bash
categories: "操作系统"
---
### 前言
一直以来，在windows系统中使用bash命令都是通过下载的`git bash`来操作。  
每次使用linux相关的命令时都需要打开这个工具，真的相当的苦恼了。  
不过现在win10内置了bash命令，可以安装linux的子系统，真是爽翻了。
<!--more-->
### 添加方式
win10内置了bash，可是默认没有开启，开启的步骤如下:  

1. 打开windows设置->更新和安全->开发者选项->开发人员模式
2. 打开控制面板->程序->启用或关闭windows功能->适用于windows的linux子系统
3. 重启,打开cmd并输入`bash`命令，此时会提示你进入`window store`进行选择linux系统安装或者直接输入y即可安装
4. 如果是给了一个网址，直接粘贴在浏览器就可以打开windows商店，搜索linux，并安装Ubuntu即可

### 最后
之前在windows安装的所有环境变量和linux是不相通的，所以需要再次在linux的环境下安装。  
现在可以爽爽的在win环境下使用linux的命令了！