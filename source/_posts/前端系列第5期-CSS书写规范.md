---
title: 前端系列第5期-CSS书写规范
date: 2018-12-18 20:42:40
tags: CSS规范
keywords: CSS规范
categories: "前端系列"
---
### 前言
本文内容部分参考自网易前端规范：[NEC](http://nec.netease.com/)
<!--more-->
### 样式属性顺序
单个样式规则下的属性在书写时，应该按以下规则书写。  
Positioning Model > Box Model > Typographic > Visual的顺序书写，提高代码的可读性。
1. Positioning Model 布局方式、位置，相关属性包括：position, top, z-index, display, float等
2. Box Model 盒模型，相关属性包括：width, height, padding, margin，border,overflow
3. Typographic 文本排版，相关属性包括：font, line-height, text-align
4. Visual 视觉外观，相关属性包括：color, background, list-style, transform, animation  

一个小例子
```css
    .box {
        // 先书写位置相关
        position: relative;
        top: 0;
        // 其次书写盒子相关
        width: 50%;
        margin: 0 auto;
        // 在书写文本相关
        font-size: 14px;
        line-height: 1.5;
        // 最后就是视觉外观
        color: red;
        transform: scale(1.2);
    }
```
### CSS选择器命名规则
分类式命名法（前端组件化）
1. 布局(grid)(.g-): 将页面分割为几个大块，通常有头部，主体，主栏等。
2. 模块(module)(.m-): 通常是一个语义化的可以重复的较大的整体。比如导航，登陆，注册等。
3. 元件(unit)(.u-): 通常是一个不可再分的较为小巧的个体，通常被重复用于各种模块,比如按钮,loading等。
4. 功能(function)(.f-): 一些常用样式，将使用频率高的样式剥离出来，按需使用，通常这些选择器具有固定样式表现，比如清楚浮动等。
5. 状态(.z-): 为状态类样式加入前缀，同一标示，方便识别，只能作为组合或者后代出现。
6. javascript(.j-): 专用于JS获取节点，请勿使用.j定义样式
  
不要使用"_"下划线来命名css  
id采用驼峰式命名(不要乱用id，最好不使用id，除非作为锚点)  
scss中的变量、函数、混合、placeholder采用驼峰式命名  
命名方式(BEM): 类-体(例如: g-head)、类-体-修饰符(例如: u-btn-active)  
### 最佳写法
```css
    /* 这是某个模块 */
    .m-nav{}/* 模块容器 */
    .m-nav li,.m-nav a{}/* 先共性  优化组合 */
    .m-nav li{}/* 后个性  语义化标签选择器 */
    .m-nav a{}/* 后个性中的共性 按结构顺序 */
    .m-nav a.a1{}/* 后个性中的个性 */
    .m-nav a.a2{}/* 后个性中的个性 */
    .m-nav .z-crt a{}/* 交互状态变化 */
    .m-nav .z-crt a.a1{}
    .m-nav .z-crt a.a2{}
    .m-nav .btn{}/* 典型后代选择器 */
    .m-nav .btn-1{}/* 典型后代选择器扩展 */
    .m-nav .btn-dis{}/* 典型后代选择器扩展（状态） */
    .m-nav .btn.z-dis{}/* 作用同上，请二选一（如果可以不兼容IE6时使用） */
    .m-nav .m-sch{}/* 控制内部其他模块位置 */
    .m-nav .u-sel{}/* 控制内部其他元件位置 */
    .m-nav-1{}/* 模块扩展 */
    .m-nav-1 li{}
    .m-nav-dis{}/* 模块扩展（状态） */
    .m-nav.z-dis{}/* 作用同上，请二选一（如果可以不兼容IE6时使用） */
```
### 统一语义理解和命名
**布局(.g-)**

语义|命名|简写
:--:|:--:|:--:
文档|doc|doc
头部|head|hd
主体|body|bd
尾部|foot|ft
主栏|main|mn
主栏子容器|mainc|mnc
侧栏|side|sd
侧栏子容器|sidec|sdc
盒容器|wrap/box|wrap/box

**模块(.m-)、元件(.u-)**

语义|命名|简写
:--:|:--:|:--:
导航|nav|nav
子导航|subnav|snav
面包屑|crumb|crm
菜单|menu|menu
选项卡|tab|tab
标题区|head/title|hd/tt
内容区|body/content|bd/ct
列表|list|lst
表格|table|tb
表单|form|fm
热点|hot|hot
排行|top|top
登录|login|log
标志|logo|logo
广告|advertise|ad
搜索|search|sch
幻灯|slide|sld
提示|tips|tips
帮助|help|help
新闻|news|news
下载|download|did
注册|regist|reg
投票|vote|vote
版权|vcopyright|cprt
结果|result|rst
标题|title|tt
按钮|button|btn
输入|input|ipt

**功能(.f-)**

语义|命名|简写
:--:|:--:|:--:
清楚浮动|clearboth|cb
左浮动|floatleft|fl
内联|inlineblock|ib
文本居中|textaligncenter|tac
垂直居中|verticalalignmiddle|vam
溢出隐藏|overflowhidden|oh
完全消失|displaynone|dn
字体大小|fontsize|fz
字体粗细|fontweight|fs

**皮肤(.s-)**

语义|命名|简写
:--:|:--:|:--:
字体颜色|fontcolor|fc
背景颜色|backgroundcolor|bgc
边框颜色|bordercolor|bdc

**状态(.z-)**

语义|命名|简写
:--:|:--:|:--:
选中|selected|sel
当前|current|crt
显示|show|show
隐藏|hide|hide
打开|open|open
关闭|close vclose|
出错|error|err
不可用|disabled|dis

### 注意事项
1. 一律小写，中划线
2. 尽量不用缩写
3. 不要随意使用id
4. 去掉小数点前面的0：0.9rem => .9rem
5. 使用简写：margin：0 1rem 3rem