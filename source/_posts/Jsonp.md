---
title: Jsonp
date: 2018-03-15 15:39:57
tags: WEB
keywords: Jsonp,Jsonp跨域,ajax跨域
categories: "技术"
---
# 什么是Jsonp
JSONP是应用于JSON的一种新方法,常用于服务器与客户端的跨源通信，在WEB服务中非常流行。
<!--more-->
# 同源政策
同源政策的本意是为了保护用户信息的安全，防止恶意的网站窃取数据，所以我们传统的AJAX技术就不能直接获取到协议不同，域名不同，端口不同的网站的数据。
# Jsonp是如何跨域获得数据的
虽然Ajax不能跨域，但是开发者发现script标签的src属性是可以跨域的，于是网页通过一个script元素向服务器请求JSON数据，而JSON正好被js支持(object)，服务器收到请求后，将数据放在一个指定的回调函数里传回来。
# 为什么叫做Jsonp?
当通过script元素调用数据时，响应内容必须用javascript函数名和圆括号包裹起来。而不是发送这样一段JSON数据，这就是JSONP中P的意义所在。 
# Jsonp与AJAX的区别?
1. ajax和jsonp本质上是不同的东西。
2. ajax的核心是通过XmlHttprequest获取**非本页**内容。
3. jsonp的核心是动态添加script标签来调用**服务器**的js脚本。   

# 一个小小的例子
文件:example.js  
代码:  
```
    alert('我是远程文件');
```
本地  
```
<script src="跨域服务器/remote.js"></script>
```
这就是直接引入一个js，页面弹出一个框，显示我是远程文件。  
# 结语
Jsonp是WEB人员经常使用的东西，但是对于原理可能不那么清楚！多学习，多积累吧!加油!

 