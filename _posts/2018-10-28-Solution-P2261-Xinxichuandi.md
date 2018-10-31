---
layout: post
title: 【题解】Luogu P2261 信息传递
categories: solution 
description: 【题解】Luogu P2261 信息传递。采用染色+标记的方法找到环并根据做的标记得到环长度
keywords: 
tags: 模拟 搜索
show: true
---

采用染色的方法。从每一个点开始染色，因为出边有且只有1条，所以染色的时候如果有环的话一定能染完这个环。

如果起始在环里面，那么继续染色，正好转一圈。（因为出度都是1，如果成环那只能循环）

如果在环外的链上染色，那么一定能染到环里面，然后又是上面的情况。

详见代码

```cpp
#include <iostream>
#include <cstdio>
using namespace std;
int a[200010];
int mark[200010];
int col[200010];
int n;
void init(){
    cin>>n;
    for(int i=1;i<=n;i++){
        // cin>>a[i];
        scanf("%d",&a[i]);
    }
}
int workone(int x){//对点x进行操作
    int sz=0;//已经染色的长度
    int i=x;//类似于前向星
    for(i=x;mark[i]==0;i=a[i]){
        //不断染色直到已经染过色的，由于可能会和别的环染色相交
        //所以标记上（如果很多个链都能到一个环，那么这个环是这些链唯一的公共的环）
        //因为如果成环了，这些节点只能指向下一个，因此有进无出。
        sz++;
        mark[i]=sz;
        col[i]=x;
    }
    if(mark[i]!=0 && col[i]!=x){//如果和别的环冲突了，那么也就是环的大小已经返回过了。忽略
        return 0x3f3f3f3f;
    }
    return sz-mark[i]+1;//返回环的大小（总染色长度-进入环及之前的长度+1）
}
void work(){
    int ans=0x7fffffff;
    for(int i=1;i<=n;i++){
        if(!mark[i]){
            ans=min(ans,workone(i));
        }
    }
    cout<<ans;
}
int main(){
    init();
    work();
}
```