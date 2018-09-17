---
title: Java开发环境的搭建
date: 2017-11-01 20:35:32
tags: Java
keywords: Java,java环境配置
categories: "环境"
---
### 一、安装JDK
下载地址:[http://www.oracle.com/technetwork/java/javase/downloads/index.html](http://www.oracle.com/technetwork/java/javase/downloads/index.html)  
根据自己的平台下载适合的JDK版本   
![](https://github.com/yuhongjing/img-folder/raw/master/img/jdk.png)  
大部分时候是无需选择Public JRE，因为Devepment Tools为JDK的核心。已经包含了
运行Java程序的JRE。  
<!--more-->
### 二、设置PATH环境变量
对于Java程序开发而言，主要使用两个JDK的命令:javac.exe和java.exe。
因为这些命令不是windows自己的命令，所以要使用就得进行路径配置。
win10系统:  
1. 右键"计算机"->"高级系统设置"->"高级"->"环境变量"
2. 新建->变量名"JAVA_HOME"，变量值"C:\Java\jdk1.8.0_05"（即JDK的安装路径） 
3. 编辑->变量名"Path"，在原变量值的最后面加上“;%JAVA_HOME%\bin;%JAVA_HOME%\jre\bin” 
4. `新建->变量名"CLASSPATH",变量值".;%JAVA_HOME%\lib;%JAVA_HOME%\lib\dt.jar;%JAVA_HOME%\lib\tools.jar"`
5. 变量可以添加在用户变量里，也可以添加在系统变量中(后者全用户都可以用)。
![](https://github.com/yuhongjing/img-folder/raw/master/img/hjbl.png)
### 三、确认环境是否正确
在控制台分别输入java,javac,java -version命令，出现如下信息说明成功
java命令:
![](https://github.com/yuhongjing/img-folder/raw/master/img/java.png)  
javac命令:
![](https://github.com/yuhongjing/img-folder/raw/master/img/javac.png)  
java -version命令:
![](https://github.com/yuhongjing/img-folder/raw/master/img/java_version.png)  
### 四、在控制器写下一个java程序
```
    public class Test {
        public static void main(String[] args) {    
        System.out.println("Hello Java");
        }
    }
```
用记事本写好保存,文件名为Test，将后缀改为.java。  
首先使用 javac Test.java编译文件
再使用java Test运行程序  
打印结果为"hello Java"  
至此恭喜你Java环境配置完成，当然你也可以使用一些IDE例如:eclipse，就可以
不用配置环境也可以编程。

ps:JRE和JDK不能再同一级目录，否则环境变量会出错。。。本人在此就踩坑了。JRE可以和JDK各自
存放在一个文件夹，也可以放在另一个子文件夹，但切不可放在同一个文件夹！！不过最好不用选择
Public JRE直接配置就Ok了！



