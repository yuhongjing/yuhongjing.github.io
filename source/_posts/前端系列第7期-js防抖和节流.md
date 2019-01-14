---
title: 前端系列第7期-js防抖和节流
date: 2019-01-02 21:14:08
tags: js
keywords: js防抖,js节流
categories: "前端系列"
---
### 前言
前端性能优化，必备知识防抖和节流。
<!--more-->
### 引子
首先举一个例子：
模拟在输入框输入后做ajax查询请求，没有加入防抖和节流的效果，这里附上完整可执行代码：
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <title>没有防抖</title>
    <style type="text/css"></style>
    <script type="text/javascript">
        window.onload = function () {
            //模拟ajax请求
            function ajax(content) {
                console.log('ajax request ' + content)
            }
            let inputNormal = document.getElementById('normal');

            inputNormal.addEventListener('keyup', function (e) {
                ajax(e.target.value)
            })
        }
    </script>
</head>

<body>
    <div>
        <!-- 1.没有防抖的输入：-->
        <input type="text" name="normal" id="normal">
    </div>
</body>

</html>
```
效果：在输入框里输入一个，就会触发一次“ajax请求”（此处是console）。

![image](https://ask.qcloudimg.com/draft/2221081/90pgtjky9q.png?imageView2/2/w/1620)
<center>没有防抖和节流</center>

缺点：浪费请求资源，可以加入防抖和节流来优化一下。

本文会分别介绍什么是防抖和节流，它们的应用场景，和实现方式。防抖和节流都是为了解决短时间内大量触发某函数而导致的性能问题，比如触发频率过高导致的响应速度跟不上触发频率，出现延迟，假死或卡顿的现象。但二者应对的业务需求不一样，所以实现的原理也不一样，下面具体来看看吧。

### 防抖
#### 什么是防抖
在事件被触发n秒后再执行回调函数，如果在这n秒内又被触发，则重新计时。
#### 应用场景
> 1. 用户在输入框中连续输入一串字符后，只会在输入完后去执行最后一次的查询ajax请求，这样可以有效减少请求次数，节约请求资源；

> 2. window的resize、scroll事件，不断地调整浏览器的窗口大小、或者滚动时会触发对应事件，防抖让其只触发一次；  

#### 实现
还是上述列子，这里加入防抖来优化一下，完整代码如下：
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <title>加入防抖</title>
    <style type="text/css"></style>
    <script type="text/javascript">
        window.onload = function () {
            //模拟ajax请求
            function ajax(content) {
                console.log('ajax request ' + content)
            }
            function debounce(fun, delay) {
                return function (args) {
                    //获取函数的作用域和变量
                    let that = this
                    let _args = args
                    //每次事件被触发，都会清除当前的timeer，然后重写设置超时调用
                    clearTimeout(fun.id)
                    fun.id = setTimeout(function () {
                        fun.call(that, _args)
                    }, delay)
                }
            }
            let inputDebounce = document.getElementById('debounce')
            let debounceAjax = debounce(ajax, 500)
            inputDebounce.addEventListener('keyup', function (e) {
                debounceAjax(e.target.value)
            })
        }
    </script>
</head>

<body>
    <div>
        <!-- 2.加入防抖后的输入： -->
        <input type="text" name="debounce" id="debounce">
    </div>
</body>

</html>
```
代码说明：

> 1. 每一次事件被触发，都会清除当前的 timer 然后重新设置超时调用，即重新计时。 
这就会导致每一次高频事件都会取消前一次的超时调用，导致事件处理程序不能被触发；

> 2. 只有当高频事件停止，最后一次事件触发的超时调用才能在delay时间后执行；

效果：

加入防抖后，当持续在输入框里输入时，并不会发送请求，只有当在指定时间间隔内没有再输入时，才会发送请求。如果先停止输入，但是在指定间隔内又输入，会重新触发计时。

![image](https://ask.qcloudimg.com/draft/2221081/43a9dksk91.png?imageView2/2/w/1620)
<center>加入防抖</center>

### 节流
#### 什么是节流
规定一个单位时间，在这个单位时间内，只能有一次触发事件的回调函数执行，如果在同一个单位时间内某事件被触发多次，只有一次能生效。
#### 应用场景
> 1. 鼠标连续不断地触发某事件（如点击），只在单位时间内只触发一次；

> 2. 在页面的无限加载场景下，需要用户在滚动页面时，每隔一段时间发一次 ajax 请求，而不是在用户停下滚动页面操作时才去请求数据；

> 3. 监听滚动事件，比如是否滑到底部自动加载更多，用throttle来判断；

#### 实现
还是上述列子，这里加入节流来优化一下，完整代码如下：
```html
    <!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <title>加入节流</title>
    <style type="text/css"></style>
    <script type="text/javascript">
        window.onload = function () {
            //模拟ajax请求
            function ajax(content) {
                console.log('ajax request ' + content)
            }

            function throttle(fun, delay) {
                let last, deferTimer
                return function (args) {
                    let that = this;
                    let _args = arguments;

                    let now = +new Date();
                    if (last && now < last + delay) {
                        clearTimeout(deferTimer);
                        deferTimer = setTimeout(function () {
                            last = now;
                            fun.apply(that, _args);
                        }, delay)
                    } else {
                        last = now;
                        fun.apply(that, _args);
                    }
                }
            }
            let throttleAjax = throttle(ajax, 1000)
            let inputThrottle = document.getElementById('throttle')
            inputThrottle.addEventListener('keyup', function (e) {
                throttleAjax(e.target.value)
            })
        }
    </script>
</head>

<body>
    <div>
        <!-- 3.加入节流后的输入： -->
        <input type="text" name="throttle" id="throttle">
    </div>
</body>

</html>
```
效果：实验可发现在持续输入时，会安装代码中的设定，每1秒执行一次ajax请求

![image](https://ask.qcloudimg.com/draft/2221081/3aohd1kgfp.png?imageView2/2/w/1620)
<center>加入节流</center>

### 小结
总结下防抖和节流的区别：

-- 效果：

函数防抖是某一段时间内只执行一次；而函数节流是间隔时间执行，不管事件触发有多频繁，都会保证在规定时间内一定会执行一次真正的事件处理函数。

-- 原理：

防抖是维护一个计时器，规定在delay时间后触发函数，但是在delay时间内再次触发的话，都会清除当前的 timer 然后重新设置超时调用，即重新计时。这样一来，只有最后一次操作能被触发。

节流是通过判断是否到达一定时间来触发函数，若没到规定时间则使用计时器延后，而下一次事件则会重新设定计时器。