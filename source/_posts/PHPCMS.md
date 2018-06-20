---
title: PHPCMS
date: 2018-06-12 21:37:00
tags:  PHPCMS
keywords: PHP,CMS
categories: "技术"
---
### PHPCMS与Thinkphp框架有何不同
之前也接触过，类似织梦CMS，帝国CMS。但是从来没有系统的了解过，这种几年前火遍大江南北的CMS和现在的框架有何不同。  
好吧，现在简单的说一下。CMS是一个已经制作完毕的程序，所有的功能已经齐全可以直接使用，当然我们也可以替换模板二次开发。  
而现在的框架，只是把一些功能，库封装好了，我们还需要直接编写功能，逻辑等。  
所以说，CMS是已经完成了80%的程序，而Thinkphp只是搭了一个架构。  
<!--more-->
### 几乎不需要编写代码的CMS
CMS可以直接安装好，然后替换模板即可使用。几乎无需直接编写代码。  
### 层次分类
phpcms并非标准的MVC架构。其工作层次如下。  
model连接数据库，配置数据库，但是不能书写业务逻辑，仅仅是一个连接配置。  
modules就是控制器，处理调用数据。  
templates就是视图，负责渲染前端。  
MVC最主要的就是model，而phpcms中的model却不能处理业务，这也就是phpcms为什么不是标准的mvc的原因。  
phpcms是完全通过源码书写的，没有什么框架，所以内核相对繁杂。
### 目录架构
```php
|-----api  接口文件目录  
|-----caches 缓存文件目录  
    |-----configs 系统配置文件目录  
        |-----database.php  数据库配置文件  
        |-----route.php     路由配置文件  
        |-----system.php    系统配置文件  
        |-----cache.php     缓存配置文件  
    |-----configs_*         系统缓存文件目录  
        |-----configs_commons/caches_data   主要用来存放后台设置的配置信息  
            |-----category_content.cache.php栏目与站点映射所对应的配置文件  
            |-----category_content_1.cache.php站点1下所有栏目的详细配置信息  
            |-----category_item_1.cache.php 文章模型下各栏目所对应的数据量  
            |-----category_item_2.cache.php 下载模型下各栏目所对应的数据量  
            |-----category_item_3.cache.php 图片模型下各栏目所对应的数据量  
            |-----keylink.cache.php     关联链接配置缓存文件  
            |-----model.cache.php       三大模型配置缓存文件  
            |-----mood_program.cache.php    表情配置缓存文件  
            |-----position.cache.php    推荐位配置缓存文件  
            |-----poster_template_1.cache.php广告位模板配置缓存文件  
            |-----sitelist.cache.php    站点列表配置文件，主要缓存所有站点的基本配置信息  
            |-----type_content.cache.php    多个站点下的类别配置信息  
            |-----type_content_1.cache.php  当前站点下类别配置信息缓存文件  
            |-----urlrules.cache.php    url规则配置信息缓存文件  
            |-----urlrules_detail.cache.php url规则详细配置信息缓存文件  
            |-----special.cache.php     专题配置信息缓存文件  
            |-----role.cache.php        角色配置缓存文件  
            |-----link.cache.php        友情链接缓存文件  
        |-----configs_model/caches_data  
            |-----content_form.class.php    生成表单的类库缓存文件  
            |-----content_input.class.php   入库时，对表单数据进行验证的类库缓存文件  
            |-----content_output.class.php  对从数据表中查询出来的数据进行处理的函数  
            |-----content_update.class.php  对要更新的数据进行有效性验证的函数  
            |-----model_field_1.cache.php   文章模型所有模型字段的缓存信息  
            |-----model_field_2.cache.php   下载模型所有模型字段的缓存信息  
            |-----model_field_3.cache.php   图片模型所有模型字段的缓存信息  

|-----phpcms                        phpcms框架主目录  
       |-----languages                  框架语言包目录  
       |-----libs                   框架主类库、主函数库目录  
       |-----classes  
            |-----form.class.php    表单生成类库文件  
            |-----application.class.php 应用程序类库文件  
            |-----image.class.php       图片处理类库文件  
            |-----attachment.class.php  附件处理类库文件  
            |-----param.class.php       URL参数处理类库文件  
       |-----functions  
            |-----global.func.php       公共函数库文件  
            |-----extension.class.php   扩展函数库文件  
       |-----model                  框架数据库模型目录  
       |-----content_model.class.php       内容模型文件  
       |-----admin_model.class.php     管理员模型文件  
       |-----attachment_model.class.php    附件模型文件  
       |-----modules                    框架模块目录  
       |-----admin             admin模块   
            |-----index.php         index.php控制器文件  
       |-----content               content模块  
            |-----classes           content模块通用类库  
            |-----fields            content模块模型字段  
            |-----functions         content模块通用函数库  
            |-----templates         content模块后台模板文件  
            |-----index.php         index.php控制器文件  
       |-----templates                  框架系统前台模板目录  
            |-----default               默认的模板风格  
                |-----content           content模块模板目录  
                    |-----category.html 频道页模板文件  
                    |-----list.html     列表页模板文件  
                    |-----show.html     内容页模板文件  
                |-----config.php        模板配置文件  
|-----phpsso_server                 phpsso主目录  
|-----statics                       网站素材文件目录  
    |-----css                                   css文件  
        |-----images                    images文件  
        |-----js                    js文件  
|-----uploadfile                    上传附件  
|-----admin.php                     后台入口文件  
|-----index.php                     前台入口文件  
```
### 模板文件与路由
http://域名/入口文件?m=模块名&c=控制器&a=方法名&catid=参数值    
频道页：category_*.html  
列表页：list_*.html  
内容页：show_*.html  
### 系统类库、函数库、模型文件及配置文件的加载 
pc_base::load_sys_class();//加载系统类库  
pc_base::load_sys_func();//加载系统函数库  
pc_base::load_model();//加载模型  
pc_base::load_config();//加载配置文件或配置选项信息  
pc_base::load_app_func();//加载应用程序函数库  
pc_base::load_app_class();//加载应用程序类库  
### 总结
因为CMS已经开发完毕，所以你需要添加自定义功能就特别的麻烦。而Thinkphp这样的框架自由度就更高了，这也就是为什么现在的CMS不那么火了的原因。