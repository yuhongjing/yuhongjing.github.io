---
title: 一个简单版的mvvm
date: 2018-08-06 21:31:22
tags: Vue
keywords: mvvm,Vue
categories: "研究"
---
### 优雅的双向绑定
想当初，只接触过jquery的我，第一次遇见vue，它的双向绑定功能就深深的吸引住了我。  
所以现在就研究一下这样魔法般的功能是如何实现的。
<!--more-->
### Object.defineproperty
vue的双向绑定是基于属性拦截器实现的，设计是基于订阅/发布模式开发的。  
该API是双向绑定的核心，通过重写数据的get，set方法。从而实现双向绑定。
### 实现思路
1. 实现数据监听器Observer,用Object.defineproperty重写数据的set和get，值更新就通知订阅者更新数据。
2. 模板编译Complie，深度遍历dom树，对每一个元素节点文本节点进行替换数据和订阅数据。
3. 使用watch连接Observer和Complie，订阅每一个元素的属性变动，执行指令绑定的回调函数从而更新视图。
4. mvvm的入口函数，整合以上。

### 流程图
![](https://github.com/yuhongjing/img-folder/raw/master/img/mvvm.jpg)
### 源码
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