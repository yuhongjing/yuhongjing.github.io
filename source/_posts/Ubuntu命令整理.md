---
title: Ubuntu命令整理
date: 2018-05-31 10:29:33
tags: linux
keywords: Ubuntu指令
categories: "技术"
---
### 前言
刚接触了Ubuntu系统，对于目前使用到的一些基础命令做了个大概的整理。
<!--more-->
### 文件/文件夹管理
#### 查看/寻找
ls [-a| -l]	列出当前目录文件(不包含隐藏文件)[包含隐藏文件|包含详细信息]
find 路径 -name "字符串" 	查找路径下满足字符串匹配的字符串
#### 创建/删除
mkdri 目录名 	创建一个目录
rmdir 目录名	删除一个目录
rm 文件名 [文件名] 	删除一个文件或读个文件
rm -rf 非空目录名	删除一个非空目录下的一切
#### 移动/改名
mv 路径/文件 绝对路径	移动文件
mv 文件名 新文件名  	目录改名
### 系统管理
uname -a 	查看内核版本
cat /etc/issue	查看ubuntu版本
sudo ethtool eth0	查看网卡状态
cat /proc/cpuinfo	查看cpu信息
reboot		重启计算机
### 打包/解压
tar [-c| -x| -v| -z] 			创建包|释放包|显示命令过程|压缩包
tar –cvf benet.tar /home/benet 		把/home/benet目录打包 
tar –zcvf benet.tar.gz /mnt 		把目录打包并压缩 
tar –zxvf benet.tar.gz 			压缩包的文件解压恢复 
tar –jxvf benet.tar.bz2 		解压缩 
### make编译
make 			编译 
make install 		安装编译好的源码包 
### apt命令
apt-cache search package 		搜索包 
apt-cache show package 			获取包的相关信息，如说明、大小、版本等 
sudo apt-get install package 		安装包 
sudo apt-get install package - - reinstall 	重新安装包 
sudo apt-get -f install 		修复安装”-f = –fix-missing” 
sudo apt-get remove package 			删除包 
sudo apt-get remove package - - purge 		删除包，包括删除配置文件等 
sudo apt-get update 		更新源 
sudo apt-get upgrade 		更新已安装的包 
sudo apt-get dist-upgrade 		升级系统 
sudo apt-get dselect-upgrade 		使用 dselect 升级 
apt-cache depends package 		了解使用依赖 
apt-cache rdepends package 		是查看该包被哪些包依赖 
sudo apt-get build-dep package 		安装相关的编译环境 
apt-get source package 			下载该包的源代码 
sudo apt-get clean && sudo apt-get autoclean 		清理无用的包 
sudo apt-get check 	检查是否有损坏的依赖 
sudo apt-get clean 	清理所有软件缓存（即缓存在/var/cache/apt/archives目录里的deb包）
### 关键词/快捷键
#### 快捷键
Ctrl+Alt+T	打开终端
Tab	自动补全
Win+A	打开软件大全
Alt+Tab	切换活动窗口
#### 关键词
dpkg	安装或删除.deb的软件包
apt-get	安装,卸载,更新软件
ls	查看目录
sudo	超级用户模式
vi	进入vi模式
cat	查看文件内容
### 一些操作方法
#### vi模式下
按I键，进入编辑模式。按ESC键退出编辑模式，输入wq！保存并退出。
### 最后
刚玩Ubuntu不久，听说这是最适合Linux新手的系统,使用起来的感觉也的确特别好。不过命令也太多了，而且似乎很多MSOS的软件都无法使用，什么百度云盘、腾讯系的软件都不可以使用，连小程序开发工具都无法使用，还必须借助Wine来运行，唉～不得不说目前我还是离不开MSOS。


