---
title: Laravel配置
date: 2018-05-17 16:14:45
tags: Laravel
keywords: Laravel,Laravel环境安装
categories: "环境"
---
### 前言
![](https://github.com/yuhongjing/img-folder/raw/master/img/Laravel/top.png)
作为只接触过Thinkphp框架的我，每次看见Github上被Laravel刷屏的趋势榜单，终于仍不住来研究一下传说中优雅的Laravel。
<!--more-->
### 安装的苦恼
安装Laravel的第一道门槛就是“墙”！在我上大一的时候，就经常听学姐说安装Laravel花费了很久很久时间。  
所以安装Laravel前，请先准备“梯子”。这样仅需1分钟就能搞定Laravel的配置。  
幸运的是，我所在的学校的校园网是可以访问外网的，所以我最终仅花费就了一分钟，搞定了Laravel的配置。 
### 安装Composer
进入Laravel的官网，直接下载Composer的安装包即可，下载后进行安装。  
以默认地址安装会自动配置PATH变量，否则需手动配置PATH变量。  
其中有一项需要选择自己电脑上的PHP.exe的支持文件。  
安装完毕后打开命令行输入`Composer`出现提示，即说明安装成功！
### 通过Laravel安装器安装
安装Composer后通过以下代码即可全局安装Laravel安装器。    
`composer global require "laravel/installer"`  
安装成功后，然后进入你想创建项目的地址，输入以下命令即可创建项目。  
`laravel new 项目名`  
出现如下图片就OK。  
 ![](https://github.com/yuhongjing/img-folder/raw/master/img/Laravel/start.png)  
### 最后
之前一直听说安装Laravel很麻烦，其实只是“墙”的问题。  
我一直很疑惑一款优雅的框架，怎么会安装这么麻烦，原来只是方法不对罢了。  

