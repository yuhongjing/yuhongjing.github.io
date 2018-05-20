---
title: PHPstorm Xdebug工具安装
date: 2018-05-16 00:22:17
tags: PHP工具
keywords: Xdebug,PHP调试工具,PHPStorm工具安装
categories: "环境"
---
### Xdebug介绍
Xdebug是一个开放源代码的PHP程序调试器(即一个Debug工具)，可以用来跟踪，调试和分析PHP程序的运行状况。  
我们可以使用Xdebug对php代码进行断点调试，能够清楚的看清楚每个地方变量的值，不用再通过`echo`和`var_dump`来输出变量了。  
<!--more-->  
  
### 在PHPStorm下安装Xdebug工具
    1. 首先我们需要知道当前客户端的PHP版本，新建一个PHP文件，输入PHPINFO()函数即可。  
    2. 然后Ctrl + F搜索Xdebug，如果没有即表明的确没有安装Xdebug。  
    3. 浏览器输入Xdebug就能看见官网，点击Download，进入页面有一个Releases版本选项，点击进入。
    4. 然后回到php的info页面，点击查看源代码，全部复制进入Xdebug的文本框，即可看到当前PHP适应的Xdebug版本。  
    5. 根据出现的提示，将文件下载后，复制进目标文件内。  
    6. 然后在php.ini文件内添加如下信息，其中第一行复制于网站的代码  
    [xdebug]
    ;第一行需要复制网站上的代码
    zend_extension = D:\xampp\php\ext\php_xdebug-2.6.0-7.2-vc15.dll

    xdebug.remote_enable=1
    xdebug.remote_handler=dbgp
    xdebug.remote_mode=req
    xdebug.remote_host=localhost
    xdebug.remote_port=9000
    xdebug.idekey="PHPSTORM"
    7. 重新打开phpinfo文件，Ctrl+F搜索Xdebug如果存在，即表示安装成功。  
    8. 打开PHPStrom，点击右上角的下箭头，Edit Configurations进入配置需要调试的文件。  
    9. 配置里面的server，输入localhost即可。
    10. 点击爬虫图标即可，进行断点调试默认F8下一步。  
### 总结
调试工具对于寻找错误的效率有特别大的提示，因为编程从某种意义上来说，就是不断的发现错误。  

      
