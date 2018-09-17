---
title: js数组常用方法
date: 2018-04-21 10:20:31
tags: WEB
keywords: js,javascript,js数组
categories: "技术"
---
# js数组的一些常用方法
本文章记录了一些js数组经常使用的方法和使用说明。
<!--more-->
## 数组添加元素和删除元素
push()方法  
该方法可把一个元素或一组元素(数组)添加到当前数组的***末尾***并返回***新的数组长度***.  
语法:    
```
    arrayObject.push(newelement1,newelement2,....,newelementX)
```
unshift()方法  
该方法可把一个元素或更多元素添加到***数组的开头***并返回***新的数组长度***.  
语法:  
```
    arrayObject.unshift(newelement1,newelement2,....,newelementX)
```
pop()方法  
该方法可以删除并***返回***数组最后一个元素.  
语法:  
```
    arrayObject.pop()
```
shift()方法  
该方法可以删除数组第一个元素，并***返回***第一个元素.  
语法:  
```
    arrayObject.shift()
```
splice()方法  
***万金油方法***,可以从数组添加/删除若干个元素，然后***返回删除的元素***.  
语法:  
```
    arrayObject.splice(index,howmany,item1,.....,itemX)
```
注释:index表示添加/删除的起始位置,howmany表示删除的个数(可以为0),item表示添加的元素.  

## 数组的基本操作方法
reverse()方法  
该方法用于颠倒数组的顺序，***不会产生新的数组***.  
语法:  
```
    arrayObject.reverse()
```
concat()方法    
该方法可以连接两个个或多个数组，***产生新的数组不会改变现有的数组***.  
语法:  
```
    arrayObject.concat(arrayX,arrayX,......,arrayX)
```
join()方法  
该方法把所有的数组元素放进一个字符串，***按指定的字符进行分隔***。  
语法:  
```
    arrayObject.join(separator)
```
sort()方法  
该方法用于对数组的元素进行排序***默认升序***.  
语法:  
```
    arrayObject.sort(sortby)
```
注释:sortby为可选参数，规定函数的排序规则，必须是函数.  
slice()方法  
该方法可从已有的数组中返回选定的元素,返回了一个***新的数组***.  
语法:  
```
    arrayObject.slice(start,end)
```

## 数组元素的查找
indexOf()方法  
该方法可返回某个指定的字符串值在字符串中***首次***出现的位置。  
语法:  
```
    stringObject.indexOf(searchvalue,fromindex)
```
lastIndexOf()方法  
该方法返回一个指定的字符串值***最后***出现的位置，在一个字符串中的指定位置从后向前搜索。  
语法:  
```
    stringObject.lastIndexOf(searchvalue,fromindex)
```

## 数组的循环操作
forEach()方法  
该方法用于调用数组的每个元素，并将元素传递给回调函数,该方法***没有返回值***。  
语法:  
```
    array.forEach(function(currentValue, index, arr), thisValue)
```

## 数组的属性
length属性  
该属性可设置或返回数组中元素的数目。  
语法:  
```
    arrayObject.length
```

# 总结
学而时习之，可以为师矣。



