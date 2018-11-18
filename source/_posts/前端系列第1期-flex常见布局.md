---
title: 前端系列第1期-flex常见布局
date: 2018-11-14 12:08:19
tags: flex
keywords: flex布局
categories: "前端系列"
---
### Sticky Footer
经典的上-中-下布局。
<!--more-->  
   
当页面内容高度小于可视区域高度时,footer吸附在底部;当页面内容高度大于可视区域高度时footer被撑开排在content下方。
  
![image](https://github.com/yuhongjing/img-folder/raw/master/img/flex/StickyFooter.png)

```html
    <body>
        <header>HEADER</header>
        <article>CONTENT</article>
        <footer>FOOTER</footer>
    </body>
```

```css
    body {
        min-height: 100vh;
        display: flex;
        flex-direction: column;
    }
    article {
        flex: auto;
    }
```

### Fixed-Width Sidebar
在上-中-下布局的基础上,加了左侧定宽sidebar。
  
![image](https://github.com/yuhongjing/img-folder/raw/master/img/flex/FixedWidthSidebar.png)  

```html
    <body>
        <header>HEADER</header>
        <div class="content">
            <aside>ASIDE</aside>
            <article>CONTENT</article>
        </div>
        <footer>FOOTER</footer>
    </body>
```

```css
    body {
        min-height: 100vh;
        display: flex;
        flex-direction: column;
    }
    .content {
        flex: auto;
        display: flex;
    }
    .content article {
        flex: auto;
    }
```

### Sidebar
左边的定宽sidebar, 右边是上-中-下布局。
  
![image](https://github.com/yuhongjing/img-folder/raw/master/img/flex/Sidebar.png)

```html
    <body>
        <aside>ASIDE</aside>
        <div class="content">
            <header>HEADER</header>
            <article>CONTENT</article>
            <footer>FOOTER</footer>
        </div>
    </body>
```

```css
    body {
        min-height: 100vh;
        display: flex;
    }
    aside {
        flex: none;
    }
    .content {
        flex: auto;
        display: flex;
        flex-direction: column;
    }
    .content article {
        flex: auto;
    }
```

### Sticky Header
上-中-下布局，区别是header固定在顶部，不会随页面滚动。
  
![image](https://github.com/yuhongjing/img-folder/raw/master/img/flex/StickyHeader.png)
  
```html
    <body>
        <header>HEADER</header>
        <article>CONTENT</article>
        <footer>FOOTER</footer>
    </body>
```

```css
    body {
        min-height: 100vh;
        display: flex;
        flex-direction: column;
        padding-top: 60px;
    }
    header {
        height: 60px;
        position: fixed;
        top: 0;
        left: 0;
        right: 0;
        padding: 0;
    }
    article {
        flex: auto;
        height: 1000px;
    }
```

### Sticky Sidebar
左侧sidebar固定在左侧与视窗同高,当内容超出视窗高度时,在sidebar内部出现滚动条。左右两侧滚动条互相独立。
  
![image](https://github.com/yuhongjing/img-folder/raw/master/img/flex/StickySidebar.png)
  
```html
    <body>
        <aside>
            ASIDE
            <p>item</p>
            <!-- many items -->
            <p>item</p>
        </aside>
        <div class="content">
            <header>HEADER</header>
            <article>CONTENT</article>
            <footer>FOOTER</footer>
        </div>
    </body>
```

```css
    body {
        height: 100vh;
        display: flex;
    }
    aside {
        flex: none;
        width: 200px;
        overflow-y: auto;
        display: block;
    }
    .content {
        flex: auto;
        display: flex;
        flex-direction: column;
        overflow-y: auto;
    }
    .content article {
        flex: auto;
    }
```