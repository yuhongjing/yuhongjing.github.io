---
title: 解决Linux重启后DNS被重写
date: 2018-05-30 21:37:35
tags: linux
keywords: ubuntn网络,lunux,DNS
categories: "填坑"
---
### 前言
本人的系统是'Ubuntu18.04 LTS'，而网上的教程一般是16.X之前的版本，所以说按照网上的办法修改什么base,tail,head，都是不可以的。  
右键进入终端输入命令'cat /etc/resolv.conf'可以查看到当前的DNS配置文件，默认是没有什么谷歌，电信等DNS的，需要我们自己配置。而配置后重启计算机，刚才配置的又不见了。这是一个在linux系统下比较常见的问题。下面就是我的解决方法。  
<!--more-->
### 修改文件为只读
网上的很多方法，我都已经试过了，都不能有效的解决我的问题。但是，其实问题很简单，将文件设置为只读即可。  
首先，先手动添加DNS，命令如下'sudo gedit /etc/resolv.conf'即可编辑。  
然后，将文件更改为只读，命令如下'sudo chattr +i /etc/resolv.conf'即可。  
现在，就算重启也不会出现DNS被重置的情况了。  
### 备注
'sudo chattr +i /etc/resolv.conf'当吧'+i'改为'-i'时，即为可以通过超级用户更改。  


