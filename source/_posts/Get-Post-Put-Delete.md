---
title: 'Get,Post,Put,Delete'
date: 2018-05-21 23:08:36
tags: Http
keywords: Http请求,GET,POST,DELETE,PUT
categories: "技术"
---
### Http请求
从客户端到服务器端的请求消息，被称为Http请求。  
它包括：消息首行中，对资源的请求方法、资源的标识符及使用的协议。  
一般我们都是用GET的方式和POST的方式去请求。  
然而，没想到除了GET和POST之外还有许多种请求方式，而且意义各不相同。。。。。
<!--more-->
### GET方式
GET并不安全，一般是向服务器索取信息。所以一般使用GET来执行一些查询的操作，也就是select的操作，例如查询用户资料。  
### POST方式
POST相对安全,一般是向服务器发送信息。所以可以用来执行update的操作，例如修改密码什么的。  
### PUT方式
PUT同POST,一般向服务器发送信息。一般用来执行insert的操作，例如增加用户，增加种类。　
### DELETE
DELETE，就是用来删除数据的。一般用来执行delete的操作，例如删除用户，删除内容等。

### 总结
Get为查询，Post为修改,Put为增加,Delete为删除。　　
其实还有许多其他的Http请求方式。我却还不知道，一直乱用，接触了RESTFul才了解到这些。　　
所以不学习新的东西，就永远不知道自己错在了哪里。
