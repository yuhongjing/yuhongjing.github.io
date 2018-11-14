---
title: MVVM框架实现探究
date: 2018-08-06 21:31:22
tags: VUE
keywords: mvvm实现
categories: "JavaScript"
---
### 前摘
2018-11-01在原文基础上，新添加一些东西，随着之后的深入会添加更多的内容。
<!--more-->
### MVVM框架的要点
目前前端js框架三巨头是Vue.js, React, AngularJs。共同点都是以数据为中心，摆脱了操作Dom节点的困恼。  
因为我本人目前主要是以Vue.js为主,React为辅，所以目前的内容主要是以Vue.js设计模式和代码作为参考，React作为对比。
### 数据的双向绑定
说起Vue，值得一提的就是数据双向绑定了。  
其实现原理就是通过属性拦截器+订阅发布模式。  
前段时间Vue作者尤雨溪表示对Proxy很感兴趣，但是至少Vue3之前是通过Object.defineproperty实现的。  
其设计原理图如下:
![](https://github.com/yuhongjing/img-folder/raw/master/img/mvvm.jpg)
### 单页面应用
我们可以使用Vue-router来实现SPA(单页面web应用),其原理是通过H5的history和hash欺骗路由来实现的。  
单页面应用的优点在于，让用户在webapp能够感受到nativeapp的流畅，能够构建mvc的开发模式。  
但是其缺点也非常明显，首页加载缓慢，首屏数据无法被SEO检测，Ajax相关，所以一般还需要SSR(服务端渲染)来解决。  

### 小demo实现Vue.js数据双向绑定，自定义属性等。
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>mvvm模式</title>
    <script src="mvvm.js"></script>
</head>
<body>
    <div id="app">
        {{ test }}
        <input type="text" v-model="test">
        <button @click="reset">重置</button>
    </div>
</body>
<script>
    new Mvvm({
        el: 'app',
        data: {
            test: ''
        },
        methods: {
            reset() {
                this.test = ""
            }
        }
    }) 
</script>
</html>
```
```js
// 核心类
class Mvvm {
    constructor(options)  {
        const { el, data, methods } = options;
        this.methods = methods;
        this.target = null;
        // 初始化dispather
        this.observe(this, data);
        // 初始化watcher
        this.compile(document.getElementById(el));
    }

    observe(root, data) {
        for(const key in data) {
            this.defineReactive(root, key, data[key]);
        }
    }

    // 每个数据绑定订阅发布
    defineReactive(root, key, value) {
        if(typeof value == 'object') {
            return this.observe(value, value);
        }
        const dep = new Dispather();
        Object.defineProperty(root, key, {
            set(newValue) {
                if(value == newValue) {
                    return;
                }
                value = newValue;
                // 发布
                dep.notify(newValue);
            },
            get() {
                // 订阅
                dep.add(this.target);
                return value;
            }
        });
    }

    // 编译
    compile(dom) {
        const nodes = dom.childNodes;
        for(const node of nodes) {
            // 元素节点
            if(node.nodeType == 1) {
                const attrs = node.attributes;
                for(const attr of attrs) {
                    if(attr.name == 'v-model') {
                        const name = attr.value;
                        node.addEventListener('input', e => {
                            this[name] = e.target.value
                        });
                        this.target = new Watcher(node, 'input');
                        this[name];
                    }
                    if(attr.name == '@click') {
                        const name = attr.value;
                        node.addEventListener('click', this.methods[name].bind(this));
                    }
                }
            }
            // text节点
            if(node.nodeType == 3) {
                const reg = /\{\{(.*)\}\}/;
                const match = node.nodeValue.match(reg);
                if(match) {
                    const name = match[1].trim();
                    this.target = new Watcher(node, 'text');
                    this[name];
                }
            }
        }
    }
}

class Dispather {
    constructor() {
        this.watchers = [];
    }
    add(watcher) {
        this.watchers.push(watcher);
    }
    notify(value) {
        this.watchers.forEach(watcher => watcher.update(value));
    }
}

class Watcher {
    constructor(node, type) {
        this.node = node;
        this.type = type;
    }
    update(value) {
        if(this.type == 'input') {
            this.node.value = value;
        }
        if(this.type == 'text') {
            this.node.nodeValue = value;
        }
    }
}
```