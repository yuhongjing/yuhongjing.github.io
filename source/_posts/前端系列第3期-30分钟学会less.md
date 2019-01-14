---
title: 前端系列第3期-30分钟学会less
date: 2018-11-26 19:21:21
tags: less
keywords: less基础
categories: "前端系列"
---
### 前序
Less的出现是为了解决CSS中过于呆板的写法。
总结为：Less = 变量＋混合＋函数。  
<!--more-->
### Less初体验
#### 安装Less
使用Npm全局安装Less
```
    npm install less -g
```
#### 一个小demo
创建一个空文件夹，命名为：learn-less  

在根目录下创建index.html文件，复制内容如下：
```html
    <!doctype html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>初识 Less</title>
        <link href="./main.css" rel="stylesheet">
    </head>
    <body>
        <div class="container">1</div>
        <div class="container2">2</div>
        <div class="container3">3</div>
    </body>
    </html>
```
在根目录下创建main.less文件，复制内容如下：
```less
    // main.less
    @width: 100%;
    @height: 100px;
    @color: red;

    .container{
    width: @width;
    height: @height;
    background-color: @color;
    margin-bottom: 5px;
    }

    .container2{
    width: @width;
    height: @height;
    background-color: @color;
    margin-bottom: 5px;
    }

    .container3{
    width: @width;
    height: @height;
    background-color: @color;
    margin-bottom: 5px;
    }
```
现在打开浏览器看一下，会发现并没有加载样式。这是因为 index.html 中引入的样式文件是 main.css 而不是 main.less。  
所以接下来，我们需要将 main.less 转换为 main.css，不用担心，这一步骤并不需要你手动操作，仅仅是运行一条命令就会自动完成转换。
```
    lessc main.less > main.css
```
操作完以上步骤就会发现在根目录下生成了一个 main.css 文件，此时再打开浏览器看看，样式已经出现了。  
  
main.css 转义内容为：
```css
.container {
  width: 100%;
  height: 100px;
  background-color: red;
  margin-bottom: 5px;
}
.container2 {
  width: 100%;
  height: 100px;
  background-color: red;
  margin-bottom: 5px;
}
.container3 {
  width: 100%;
  height: 100px;
  background-color: red;
  margin-bottom: 5px;
}
```
### 感受Less的便利
#### 变量
前面的demo已经使用了"变量"的概念，是不是感觉和js很像，事实上less就是用js的语法来写css。
  
总结一下就是：使用@符号定义变量，使用@符号获取变量，仅仅将`@变量名`看成一个字符串。
```less
    @classname: main;
    @color: red;

    .@classname{
        background-color: @color;
    }
```
从上面例子中可以看到,变量不仅仅可以作为样式属性值:background-color:@color;  
还可以作为类名:.@classname表示的就是.main。这也就是为什么说仅仅将@变量名看成是一个字符串。
#### 混合
mixin在js中是一种非常非常常见的用法。   
  
先看看一个example.css文件：
```css
    #menu a {
        color: #111;
        border-top: dotted 1px black;
        border-bottom: solid 2px black;
    }

    #menu span {
        height: 16px;
        border-top: dotted 1px black;
        border-bottom: solid 2px black;
    }

    #menu p {
        color: red;
        border-top: dotted 1px black;
        border-bottom: solid 2px black;
    }
```
可以看到上面三个样式中都有border-top和border-bottom两个属性，并且内容完全相同；
在传统CSS写法中只能这样一遍有一遍的去书写重复的内容，  
在Less中通过将公共属性抽取出来作为一个公共类的方式规避这一点。
```less
// example2.less
.bordered {
    border-top: dotted 1px black;
    border-bottom: solid 2px black;
}

#menu a {
    color: #111;
    .bordered;
}

#menu span {
    height: 16px;
    .bordered;
}

#menu p {
    color: red;
    .bordered();
}
```
将以上example2.less进行转译成example2.css文件为：
```css
    .bordered {
        border-top: dotted 1px black;
        border-bottom: solid 2px black;
    }
    #menu a {
        color: #111;
        border-top: dotted 1px black;
        border-bottom: solid 2px black;
    }
    #menu span {
        height: 16px;
        border-top: dotted 1px black;
        border-bottom: solid 2px black;
    }
    #menu p {
        color: red;
        border-top: dotted 1px black;
        border-bottom: solid 2px black;
    }
```
可以看到examle2.css与example.css很相似,只是多了一个.bordered样式。

修改example2.less,将.bordered写成.bordered(),此时在进行转译之后会看到example2.css和example.css文件就完全一样了,使用less书写更加简单。
```less
// example2.less
.bordered() {
    border-top: dotted 1px black;
    border-bottom: solid 2px black;
}

...
```
总结：

混合也是减少代码书写量的一个方法；

混合的类名在定义的时候加上小括弧()，那么在转译成css文件时就不会出现；

混合的类名在被调用的时候加上小括弧()和不加上小括弧()是一样的效果,看个人习,如：第三行和第八行转译成css是一样的。
```css
#menu span {
    height: 16px;
    .bordered;
}

#menu p {
    color: red;
    .bordered();
}
```
#### 函数
曾几何时，在书写呆板的css时有没有想过让类名动态化，根据不同的参数生成不同的样式。看下面的示例：
```less
// func.less
.border-radius(@radius) {
  -webkit-border-radius: @radius;
     -moz-border-radius: @radius;
          border-radius: @radius;
}

#header {
  .border-radius(4px);
}
.button {
  .border-radius(6px);
}
```
使用`$ lessc func.less`进行转译func.css文件内容如下：
```css
#header {
  -webkit-border-radius: 4px;
  -moz-border-radius: 4px;
  border-radius: 4px;
}
.button {
  -webkit-border-radius: 6px;
  -moz-border-radius: 6px;
  border-radius: 6px;
}
```
可以看到,这里就用到了函数的概念，在#header和.button中分别传入不同的参数，结果也就生成不同的代码。

关于 less 中函数的写法还有以下几种：
```less
/* 函数的参数设置默认值：*/
.border-radius(@radius: 5px) {
  -webkit-border-radius: @radius;
  -moz-border-radius: @radius;
  border-radius: @radius;
}

/* 函数有多个参数时用分号隔开 */
.mixin(@color; @padding:2) {
  color-2: @color;
  padding-2: @padding;
}

/* 函数如果没有参数，在转译成 css 时就不会被打印出来，详见上面混合中的示例 */
.wrap() {
  text-wrap: wrap;
}

/* 函数参数如果有默认，调用时就是通过变量名称，而不是位置 */
.mixin(@color: black; @margin: 10px; @padding: 20px) {
  color: @color;
  margin: @margin;
  padding: @padding;
}
.class1 {
  .mixin(@margin: 20px; @color: #33acfe);
}

/* 函数参数有个内置变量 @arguments，相当于 js 中的 arguments */
.box-shadow(@x: 0; @y: 0; @blur: 1px; @color: #000) {
  -webkit-box-shadow: @arguments;
     -moz-box-shadow: @arguments;
          box-shadow: @arguments;
}

/* 函数名允许相同，但参数不同，类似于 java 中多态的概念 */
.mixin(@color: black) {      
.mixin(@color: black; @margin: 10px) {
```
当然,上面是开发人员自定义的函数,Less也为我们定义了很多好用的内置函数。  
关于内置函数,如果掌握,可以在开发过程中节约很多时间,由于内置函数数量很多，这里就不一一介绍。
#### 父子元素的写法
在css中父子元素的写法通常如下：
```css
.container {
    padding: 0;
}
.container .article {
    background-color: red;
}
```
在Less写法如下，父子嵌套关系一目了然。
```less
.container {
    padding: 0;
    .article {
        background-color: red;
    }
}
```
当然,父子元素还要一种是伪类的写法,在css中写法如下：
```css
#header :after {
  content: " ";
  display: block;
  font-size: 0;
  height: 0;
  clear: both;
  visibility: hidden;
}
```
在less中写法如下,可以看到引入了新的符号&,以&来代替主类#header。
```less
#header {
  &:after {
    content: " ";
    display: block;
    font-size: 0;
    height: 0;
    clear: both;
    visibility: hidden;
  }
}
```
#### 神奇@import
在传统css文件中,每个文件都是独立的。在less中可以像js的模块那样在一个less文件中引入另一个less文件。
  
创建 one.less 文件：
```less
    .container {
        width: 100px;
        height: 200px;
    }
```
创建two.less文件：
```less
    @import "one";
```
使用`$ lessc two.less`转译成two.css文件,可以看到内容如下：
```css
.container {
  width: 100px;
  height: 200px;
}
```
@import的作用可以看成是将one.less的内容复制一份到当前.less文件中。