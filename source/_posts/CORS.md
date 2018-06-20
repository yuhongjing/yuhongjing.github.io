---
title: CORS
date: 2018-06-13 10:03:47
tags:  CORS
keywords: 跨源资源共享,跨域资源共享,CORS
categories: "技术"
---
### 你不得不解决的跨域问题
跨域是前后端传输数据不能逃避的问题，详情百度跨域，跨源，不过你肯定遇见过。     
前面写过一篇文章，jsonp就是解决跨域的一种方式，但是这样的方式并不理想。  
所以W3C出了一个CORS`(Cross-Origin Resource Sharing,跨源资源共享)`的标准。  
其思想是自定义HTTP头部让浏览器与服务器沟通。  
所以要使用这种方式的前提是：我们能够设置服务器。   
<!--more-->
### 我的配置以及代码
本人是使用apache的集成环境，搭建的本地虚拟服务器。  
代码以Thinkphp为例,代码如下。  
```php
//行为文件
<?php
namespace app\api\behavior;
class CORS
{
    public function appInit(&$params)
    {
        header('Access-Control-Allow-Origin: *');
        header("Access-Control-Allow-Headers: token,Origin, X-Requested-With, Content-Type, Accept");
        header('Access-Control-Allow-Methods: POST,GET');
        if(request()->isOptions()){
            exit();
        }
    }
}

//tag文件
<?php
/**
 * app_init CORS跨域
 *
 */
// 应用行为扩展定义文件
return [
    // 应用初始化
    'app_init'     => [
        'app\\api\\behavior\\CORS'
    ],
    // 应用开始
    'app_begin'    => [],
    // 模块初始化
    'module_init'  => [],
    // 操作开始执行
    'action_begin' => [],
    // 视图内容过滤
    'view_filter'  => [],
    // 日志写入
    'log_write'    => [],
    // 应用结束
    'app_end'      => [],
];
```
从而对每一次的HTTP请求进行处理，完成CORS跨域的功能。
### 最后
CORS只是一种标准，代码的写法有成千上万种，但是核心即header，也就是http的响应头。   
如果不知道，百度一下http的相关知识，学习WEB不知道这些最基础的知识可不行。  