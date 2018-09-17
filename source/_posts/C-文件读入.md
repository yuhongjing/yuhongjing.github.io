---
title: C++文件读入
date: 2017-12-18 10:48:37
tags: C++
keywords: C,C++,文件读入,文件流出
categories: "算法"
---
### 前言
C++文件流入流出，iostream流，fstream流。
<!--more-->

### 单行文件读入
```
using namespace std;
 
int main()
{
    int cnt=0;
    int i;
    ifstream fin;
    ofstream fout;
    
	fin.open("D:\\homework--net\\test.txt", ios::in);
    fout.open("D:\\homework--net\\test1.txt", ios::app);
    
    if(!fin){
        printf("The file is not exist!");
        return -1;
    }
    while(!fin.eof())
    {
        fin >> i;
        int sum = i;
        fout<<sum<<"\n";

    }
    fin.close();
    fout.close();
    return 0;
}
```

### 多行文件流出
```
#include <iostream>
#include <fstream>
 
using namespace std;
 
int main()
{
    int cnt=0;
    int a[20][3];
    ifstream fin;
    ofstream fout;
    
	fin.open("D:\\test.txt", ios::in);
    fout.open("D:\\test1.txt", ios::app);
    
    if(!fin){
        printf("The file is not exist!");
        return -1;
    }
    while(!fin.eof())
    {
        fin >> a[cnt][0]>>a[cnt][1]>>a[cnt][2];
        int sum = a[cnt][0] + a[cnt][1] + a[cnt][2];
        fout<<sum<<"\n";
        cnt++;
    }
    fin.close();
    fout.close();
    return 0;
}
```