---
layout: w
title: 前端系列第4期-你只知道AJAX?
date: 2018-12-04 14:11:08
tags: flex
keywords: flex布局
categories: "前端系列"
---
### 前言
随着前端技术的发展，请求服务器数据的方法早已经不局限于ajax，jquery的ajax方法了。各种js库已经如雨后春笋一般，蓬勃发展，本文主要介绍axios和fetch。
<!--more--> 
### ajax
ajax(`Asynchronous JavaScript and XML--异步JavaScript 和 XML`),是一种客户端向服务器请求数据的方式，并且不需要去刷新整个页面；它依赖的是XMLHttpRequest对象。当然一般项目中我们不是直接使用原生的ajax，而是使用各种库，例如Jquery。不过随着前端技术的发展，XHR也有了替代的方案（fetch）。
### axios
是基于Promise的HTTP库，可以用在浏览器和nodejs中。  
  
随着vuejs作者尤雨溪发布消息，不再维护vue-resource，并推荐大家使用axios开始，axios就进入了很多人的目光。axios本质也是对原生的XHR的封装，不过它是Promise的实现版本，符合新的ES规范，axios的几条特征：
```
1. 从浏览器创建XHR
2. 从nodejs创建http请求
3. 支持Promise API
4. 客户端支持防御CSRF
5. 提供了一些并发请求的接口
```
  
#### 使用npm安装：
```
npm install axios
```
  
#### 示例--执行GET请求：
```
// axios
axios.get('/getData', {
    params: {
        ID: 1
    }
}).then(function (response) {
    console.log(response);
}).catch(function (error) {
    console.log(error);
});
```
#### axios的优点
体积较小、使用简单、还可以执行多个并发请求，并且可以直接得到返回结果，不会像fetch一样需要自己去转换。
### fetch
`fetch API`脱离了XHR，是基于Promise设计。旧浏览器不支持Promise，需要使用`polyfill es6-promise`。  
  
#### 使用npm安装：
```
npm install whatwg-fetch --save
```
  
#### 示例--执行GET请求：
```
// use 'whatwg-fetch'
import 'whatwg-fetch'

var result = fetch(url, {
    credentials: 'include', // 跨域请求带cookie
    header: { 'Accept': 'application/json, text/plain, */*' } // 设置http请求头
}).then(res => {
    return res.text(); // 返回数据转换为文本
    // return res.json(); // 返回数据转换为json 
}).then(text => {
    console.log(text);
}).catch(e => {
    throw(e);
})
```
可以在这个代码的基础上，继续添加一些操作，例如请求前数据检查等，非常的方便。  
    
#### fetch的优点以及需要注意的地方
fetch优点有如下几条：
```
1. 脱离XHR，是ES规范里新的实现方式，支持async/await。
2. 更加底层，提供了丰富的API（request， response）。
3. 符合关注分离，没有将输入、输出和用事件来跟踪的状态混杂在一个对象里。
4. 更好更方便的写法。
```
使用fetch需要注意的是：
```
1. 兼容性
2. 当服务器返回400、500等错误时并不会reject，
   只有网络错误等原因导致请求不能完成时，才会执行reject
3. fetch不支持abort，不支持超时控制，使用setTimeout及Promise.reject实现的
   超时控制，并不能阻止请求过程在后台进行，造成了流量的浪费。
4. fetch没有办法原生监测请求的进度，而XHR可以
5. fetch跨域请求时，默认不带cookie，需要自己指定credentials:’include’
```
### 小结
详细资料请访问MDN和WHATWG。