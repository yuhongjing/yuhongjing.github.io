---
title: js实现八大排序
date: 2018-08-29 14:12:30
tags: 算法
keywords: JS排序
categories: "算法"
---
### 前言
现在的面试啊，唉动不动就是手写算法。不容易啊，不容易。  
笔试一遍一遍的跪。哎。  
<!--more-->
### 冒泡排序
冒泡排序解析:  
比较相邻的两个数,若前面的比后面的元素大(小),就交换   
第一轮比较完毕，最大的数字肯定在最后。  
比较n-1轮即可，因为最后一个数字不需要比较了。  
**代码如下**
```
    function sort(arr) {
		if(arr.length <= 1) { return arr; }

        let len = arr.length;
		for(let i=0; i<len-1; i++){
			for(let j=0; j<len-1-i; j++){
				if(arr[j] > arr[j+1]) {
					[arr[j], arr[j+1]] = [arr[j+1], arr[j]];
				}
			}
		}
		return arr;
	}
```
### 简单选择排序
选择排序解析:  
每一轮,选择第n小的数，放在第n个位置。  
例如第一轮选择最小的数放在第一个位置。  
**代码如下**
```
    function sort(arr) {
		if(arr.length <= 1) { return arr; }

        let len = arr.length;
		for(let i=0; i<len-1; i++){
			let min = arr[i];
			let pos = i;
			for(let j=i+1; j<len; j++){
				if(min > arr[j]) {
					min = arr[j];
					pos = j;
				}
			}
			[arr[i], arr[pos]] = [min, arr[i]];
		}
		return arr;
	}    
```
### 快速排序
快速排序解析:  
选出一个基准值(一般是中间)  
遍历数组，小的放基准值左边，大的放基准值右边
递归(两边都快速排序)  
**代码如下**
```
    function quickSort(arr){
        if(arr.length<=1){ return arr; }

        let pivotIndex=Math.floor(arr.length/2);
        let pivot=arr.splice(pivotIndex,1)[0];
        let left=[];
        let right=[];

        let len = arr.length;
        for(let i=0;i<len;i++){
            if(arr[i]<=pivot){
                left.push(arr[i]);
            }
            else{
                right.push(arr[i]);
            }
        }
        return quickSort(left).concat([pivot],quickSort(right));
    }                
```
### 直接插入排序
直接插入排序解析:   
每一步将一个待排序的记录，插入到前面已经排好序的有序序列中去。   
直到插完所有元素为止。    
**代码如下**
```
    function sort(arr) {
		if(arr.length <= 1) { return arr; }

		let len = arr.length;
		for(let i=1; i<len; i++) {
			let key = arr[i];
			let pos = i-1;
			while(pos>=0 && arr[pos] > key) {
				arr[pos+1] = arr[pos];
				pos--;
			}
			arr[pos+1] = key;
		}
		return arr;
	}
```
### 希尔排序
希尔排序解析:   
将数组分为若干个子序列分别插入排序。  
然后合一次插入所有的序列。  
**代码如下**
```
    function shellsort(arr) {
		if(arr.length <=1) { return arr; }

		let len = arr.length;
		let temp;
		let count = 0;
		let increment = len;
		do
		{
			increment = Math.floor(increment / 3) + 1;
			for(var i = increment; i<len; i++) {
				if(arr[i] < arr[i - increment]) {
					temp = arr[i];
					for(var j=i-increment; j>=0 && temp < arr[j]; j-=increment) {
						arr[j+increment] = arr[j];
					}
					arr[j + increment] = temp;
				}
			}
		}
		while (increment > 1);
		return arr;
	}    
```
### 堆排序 
### 桶排序
### 归并排序
### 基数排序
### 总结
剩下的慢慢补全，努力吧。秋招伤人心。唉。唉。唉。
