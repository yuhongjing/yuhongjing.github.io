---
title: vue路由懒加载
date: 2019-03-11 14:47:33
tags: Vue
keywords: Vue路由懒加载
categories: "环境配置"
---
### 路由懒加载
当打包构建应用时，Javascript 包会变得非常大，影响页面加载。如果我们能把不同路由对应的组件分割成不同的代码块，然后当路由被访问的时候才加载对应组件，这样就更加高效了。

结合 Vue 的异步组件和 Webpack 的代码分割功能，轻松实现路由组件的懒加载。
<!--more-->
### 异步组件
实现异步组件的方式如下:
```js
// 原本的引入方式
import Home from '@/components/Home'

// 现在修改如下
const Home = () => import(/* webpackChunkName: "Home" */ '@/components/Home')

// 路由中的组件引入方式不改变
{
    path: '/',
    name: 'Home',
    component: Home
},
```
修改成功后,`npm run dev`时可能会直接报错。  
[官网解释](https://router.vuejs.org/zh/guide/advanced/lazy-loading.html#%E6%8A%8A%E7%BB%84%E4%BB%B6%E6%8C%89%E7%BB%84%E5%88%86%E5%9D%97): 使用Babel时,需要安装`syntax-dynamic-import`插件来正确解析语法。

### 配置插件
首先安装:
```cmd
npm install --save-dev @babel/plugin-syntax-dynamic-import
```
然后修改`webpack.base.config.js`文件中的代码:
```js
{
    test: /\.js$/,
    loader: 'babel-loader',
    // 添加Plugins 引入插件
    options: {
        plugins: ['syntax-dynamic-import']
    },
    include: [resolve('src'), resolve('test'), resolve('node_modules/webpack-dev-server/client')]
},
```
现在页面能够正常运行了。  
### chunk组件打包
不过打包的时候chunk包的名字都是乱的,如果需要指定命名需要如下设置:
```js
// 这里的 /* webpackChunkName: "Home" */属于(魔法注释)
// 当ChunkName相同时,webpack会将他们识别为一组,打包到同一个文件中
const Home = () => import(/* webpackChunkName: "Home" */ '@/components/Home')
const Test = () => import(/* webpackChunkName: "Home" */ '@/components/Test')
```
但是仅做完上面这些步骤还是不够的,我们还需要修改`webpack.prod.conf.js`文件:
```js
output: {
    path: config.build.assetsRoot,
    filename: utils.assetsPath('js/[name].[chunkhash].js'),
    // 这是原本的代码
    // chunkFilename: utils.assetsPath('js/[id].[chunkhash].js')
    // 新增以下两句,其中的name就是魔术注释里面的name
    chunkFilename:utils.assetsPath('js/[name]-[chunkhash:8].js'),
    publicPath:'./' // 如果打包后出现文件引入报错问题一般都是这个
  },
```
现在就可以实现本地预览和打包后都异步加载路由的功能了。