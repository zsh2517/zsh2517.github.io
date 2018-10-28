---
layout: post
title: 贪心问题-喷水装置（区间最小完全覆盖）
categories: algorithm
description: 长度为L,宽度为W的草坪上有N个喷头。每个都在中心线(W/2)的位置。已知没个喷头的位置和喷洒半径，求完全喷洒最少多少喷头？
keywords: 贪心 喷水装置 区间最小完全覆盖
tags: 贪心
show: true
---

长度为L,宽度为W的草坪上有N个喷头。每个都在中心线(W/2)的位置。已知没个喷头的位置和喷洒半径，求完全喷洒最少多少喷头？

思路：在确保能够连续覆盖的情况下，可以直接按照左端排序，然后不断向右扩展。由于在每次扩展过程中，已经判断了左端点小于扩展长度的所有区间并且选择了最大值。因此在下一次判断的时候直接从上次的位置开始即可。

```cpp
#include <iostream>
#include <algorithm>
#include <cstdio>
#include <cmath>
using namespace std;
int n,l,w;
struct segment{
    double left,right,r;
    double pos;
}a[100100];
bool operator<(segment a,segment b){
    return a.left<b.left;
}
void init(){
    cin>>n>>l>>w;
    int temp;
    for(int i=1;i<=n;i++){
        cin>>a[i].pos>>temp;
        if(2*temp<w){
            a[i].left=-1;
            a[i].right=-1;
            continue;
        }
        a[i].r=sqrt(1.0*temp*temp-1.0*w*w/4);
        a[i].left=a[i].pos-a[i].r;
        a[i].right=a[i].pos+a[i].r;
    }
}
void work(){
    int ans=0;
    int lastpos=1; 
    double right=0;
    sort(a+1,a+n+1);
    while(right<l){
        double temp=0.0;
        for(int i=lastpos;i<=n && a[i].left<=right;i++){
            temp=max(temp,a[i].right-right);
            lastpos=i;
        }
        if(temp==0){
            break;
        }
        right+=temp;
        ans++;
    }
    if(right>l){
        cout<<ans<<endl;
    }else{
        cout<<0<<endl;
    }
}
int main(){
//    freopen("data.in","r",stdin);
//    freopen("data.out","w",stdout);
    int qwq;
    cin>>qwq;
    while(qwq>0){
        qwq--;
        init();
        work();
    }
}
```