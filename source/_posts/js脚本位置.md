---
title: js脚本位置
date: 2017-10-29 16:09:55
tags: WEB
keywords: javascript脚本位置区别
categories: "技术"
---
# javascript代码应该放置何处
## 如何使用js代码
一般来说使用js代码可以通过两种方式  
    1.通过外部js文件引入  
    2.html页面上直接写入脚本
## 在哪里放置js代码
通常情况下，js代码是和html代码一起使用，可以将js代码放入html文档中的任何地方。
但是放置的地方会对js的正常执行产生不同的反应和影响。具体如下。  
**放置于```<head></head>```之间**  
将js代码放置于html文档的head之间是比较常见的做法。因为html文档是由浏览器从上至下
依次载入。这样即可确保脚本是在内容加载之前载入。
代码如下:
```html
    <html>
        <head>
            <script type="text/javascript">
            ....
            javaScript代码
            ....
            </script>
        </head>
        <body>
            .... 
        </body>      
    </html>
```   
**放置于```<body></body>```之间**  
也有部分情况下，需将js代码放于body之间，例如当js代码需要操作一个元素，而html文档
是从上往下依次载入，所以此时元素未加载，便会报错。所以这种情况下，我们需将js的代码
放在元素的后面，待元素加载完毕时，才使用js代码。代码如下。  
```html
    <html>
        <head>
            ....
        </head>
        <body>
            <div id="div1"></div>
            <script type="text/javascript">
               document.getElementById('div1').innerHTML = "test";
            </script>
        </body>
    </html>
```
**放置于```<html><body></body>js代码</html>```之间  
js代码放在body之后有一个好处就是可以dom的生成就不会因为长时间执行script脚本而延迟阻塞，
从而加快了页面的加载速度。但是又不能将所有的script放在body之后，因为有一些页面的效果的
实现，是需要预先动态的加载一些js脚本。所以需依情况而定。代码如下。
```html
    <html>
        <head>
            ....
        </head>
        <body>
            .... 
        </body>    
        <script type="text/javascript">
                    ....
                    javaScript 代码
                    ....
        </script>
    </html>
```   
**放置于```<html></html>```之外**  
虽然js代码可以放置在html之外。但通常情况下，我们不建议将javascript的代码写到html之外。
```html
    <html>
        <head>
            ....
        </head>
        <body>
            .... 
        </body>    
    </html>
     <script type="text/javascript">
            ....
            javaScript 代码  
            ....
     </script>
```   
**放置于```<head></head>js代码<body></body>```之间**
一般来说“页面效果实现类的js应该放在body之前”而“动作，交互，事件驱动，需要访问dom属性的js都可以放在body之后”。
这样就既不会导致网页加载时间过长，也不会出现dom元素未加载，所以这种放置的方法还算比较科学。不过还是得依情况而定。
具体代码如下。
```html
    <html>
        <head>
            ....
        </head>
        <script type="text/javascript">
             ....
             javaScript 代码  
             .....
        </script>
        <body>
            .... 
        </body>    
    </html> 
```   
## 注意事项
当你的js文件代码引用了其他jquery文件时，一定要将被引用的文件放在你的代码或者文件之前,否则会报错！
例如:
```html
    <script src="jq文件"></script>
    <script src="你的文件">
        你的js代码中有引用jq的代码时，jq的文件必须在你的文件之前加载
        否则提示不能找到！！！
    </script>
```

##  总结
我个人喜欢将js的代码写入body之后，为了速度快。当然还是得依情况而定。
