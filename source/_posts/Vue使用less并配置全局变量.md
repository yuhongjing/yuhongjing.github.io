---
title: Vue使用less并配置全局变量
date: 2019-03-08 16:27:36
tags: Vue
keywords: Vue,less,全局变量
categories: "环境配置"
---
### less
less可以让我们更好的高效的使用CSS。
<!--more-->
### 安装
命令行执行如下代码即可安装:
```cmd
npm install less less-loader --save-dev
```
### 配置
如果不需要配置全局less那么直接修改`webpack.base.conf.js`文件即可。
```js
{
    test: /\.less$/,
    loader: "style-loader!css-loader!less-loader",
}
```
不过不推荐这样使用,所以可以省略这一步。
### 全局配置
如果按照以下方法配置,我们可以制定某些样式文件作为全局共有的,从而实现全局less。
首先安装:  
```cmd
npm install sass-resources-loader --save-dev
```

在build的utils.js文件中,添加如下函数
```js
  function lessResourceLoader() {
    var loaders = [
      cssLoader,
      'less-loader',
      {
        loader: 'sass-resources-loader',
        options: {
          resources: [
            // 全局less
            path.resolve(__dirname, '../src/common/publicCss.less')  // 这里就是你的全局less文件
          ]
        }
      }
    ];
    if (options.extract) {
      return ExtractTextPlugin.extract({
        use: loaders,
        fallback: 'vue-style-loader'
      })
    }else{
      return ['vue-style-loader'].concat(loaders)
    }
  }
```
并将此文件下的return参数修改如下:
```js
return {
    css: generateLoaders(),
    postcss: generateLoaders(),
    // 原本
    // less: generateLoaders('less'),
    // 修改为
    less: lessResourceLoader(),
    sass: generateLoaders('sass', { indentedSyntax: true }),
    scss: generateLoaders('sass'),
    stylus: generateLoaders('stylus'),
    styl: generateLoaders('stylus')
  }
```
现在即可使用less,并配置全局变量了。
