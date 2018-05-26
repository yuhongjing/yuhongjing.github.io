---
title: vue项目总结
date: 2018-05-08 16:42:17
tags:  Vue
keywords: IE盒子模型,W3C盒子模型
categories: "技术"
---
# 项目介绍
本项目是一个翻新版本，第一版的记账本完全由Thinkphp完成（功能已经完善）。  
<!--more-->
本项目前端由Vue,Vue-cli,Vue-Router,axios完成,后端由Thinkphp5+Mysql+linux完成。  
本项目完成了一款基础的记账本功能，主要包括用户的资料修改，记账，查账。  
未完成的功能，用户注册，账本删除，种类新增等。  
# 项目结构
前端分为了3个模块:用户登录模块,主页模块,功能模块(主要)  
后端三个控制器对应三个模块:Login,Home,Index完成相应功能  
# 项目难点
前后端分离请求API跨域：因为我可以处理后台，所以直接从后台添加header即可，否则需要配置ngnix反向解析。  
```php
    public function _initialize(){  
        header('Access-Control-Allow-Origin:*'); 
        header('Access-Control-Allow-Methods:GET,POST,PATCH,PUT,OPTIONS');
        header('Access-Control-Allow-Headers:x-requested-with, content-type');
    }  
```
Centos文件权限777：因为云服务器的系统为linux，忘了设置文件权限777，导致无法写日志，出现code500的错误，困扰了我很久。唉。  
Thinkphp模型：一直使用Thinkphp的Db类，现在第一次接触模型来操作数据库，但是此次并没有使用模型的数据自动化和关联模型。  
Vue-build：用vue-cli打包出来的程序，如果直接build会导致图片的地址出现错误，需要手动改变。    
```js
    首先修改config文件下的index.js中的build方法
    assetsPublicPath: './'

    再修改build文件下的utils.js
    if (options.extract) {
      return ExtractTextPlugin.extract({
        use: loaders,
        publicPath:'../../',
        fallback: 'vue-style-loader'
      })
    } else {
      return ['vue-style-loader'].concat(loaders)
    }
  }
```
vue图片位置:如果图片放入assets中，会被编译打包，所以不能通过地址的方式动态引入，如果放在static中，不会被打包，但是必须通过data的方法引入才能显示。  
vue全局变量的几种方法: vuex，新建一个js然后export出来引入main.js(全局注入)，也可以按需import进入,变量为webpack的global方式，当然还可以更改原型链`Vue.prototype.XXX = XXX`  
vue引入一些组件或UI：main.js中直接全局引入在Vue.use使用即可，css也是如此。也可以在各个组件中单独引入。例如axios也是如此.  
vue安装插件:`npm install 插件名 -- save`不能在方便   
vueUI的样式打包失效:main.js将引入的uiCSS放在vue之前即可   
vue返回上一页:this.$router.back(-1)  
vue图片的引入:import图片地址然后放入data中  
后台用json方式传送数据到前端:因为json的键名和键值都是字符型，所以需要特别注意键值类型。  
filter管道:可以格式化一些特定的数据，例如日期格式化  
# 总结
多总结，多温习。