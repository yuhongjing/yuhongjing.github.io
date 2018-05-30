---
title: W3c盒子模型
date: 2018-03-15 16:42:21
tags:  WEB
keywords: IE盒子模型,W3C盒子模型
categories: "技术"
---
# 两种盒子模型
一种是IE的怪异盒子模型，一种是W3C的标准盒子模型。两种盒子模型的计算方式不同。目前IE高版本的浏览器已经放弃了怪异盒子模型。在此之前的前端开发者，深受此兼容困扰！庆幸我现在已经不用处理那么多的兼容。
<!--more-->
# W3C盒子模型
![](https://github.com/yuhongjing/img-folder/raw/master/img/W3C_box.jpg)
标准盒子的计算方式为:width=border+padding+margin+content,其中content不包含其他。
# IE盒子模型
![](https://github.com/yuhongjing/img-folder/raw/master/img/IE_box.jpg)
IE盒子模型又称为"怪异盒子模型",计算方式为width=margin+content,其中content包含border+padding+content。
# 选择哪种盒子模型？
目前主流的都是选择标准盒子模型，在页头加入DCOTYPE声明即可！
# 总结
一些基础的必备知识！努力学习，努力积累，日积跬步，能至千里。

