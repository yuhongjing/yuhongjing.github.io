---
title: hexo常用命令
date: 2017-11-20 19:45:25
tags: hexo
keywords: hexo,hexo命令
categories: "技术"
---
### hexo配置命令
```html
1. npm install hexo -g #安装  
2. npm update hexo -g  #升级  
3. hexo init           #初始化
```

<!--more-->

### hexo基础命令
```html
1. hexo new "文章名" == hexo n "文章名" #新建文章
2. hexo generate == hexo g    #生成本地静态文件
3. hexo server == hexo s #启动服务预览
4. hexo deploy == hexo d #部署
5. hexo clean #清除缓存
```
### hexo模板
```html
1. hexo new "文章名" #新建文章
2. hexo new page "pageName" #新建页面
```
### 推送到服务器
```html
1. hexo n #写文章
2. hexo g #生成静态文件
3. hexo d #部署  可与hexo g合并为 hexo d -g
```

