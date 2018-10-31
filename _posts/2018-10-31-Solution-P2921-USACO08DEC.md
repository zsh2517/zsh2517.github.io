---
layout: post
title: P2921 [USACO08DEC]在农场万圣节Trick or Treat on the Farm
categories: solution
description: P2921 [USACO08DEC]在农场万圣节Trick or Treat on the Farm，题目和信息传递类似，不同的是这个题要求出每个点的长度。方法一样，标记+染色。
keywords: 
tags: 模拟 搜索
show: true
---

题目链接[P2921 [USACO08DEC]在农场万圣节Trick or Treat on the Farm](https://www.luogu.org/problemnew/show/P2921)

题目和信息传递类似，不同的是这个题要求出每个点的长度。方法一样，标记+染色。

```
#include <iostream>
#include <stack>
#include <cstdio>
using namespace std;
int n;
int a[100010];
int col[100010];
int mark[100010];
int cir[100010];
int ans[100010];
void init(){
    cin>>n;
    for(int i=1;i<=n;i++){
        scanf("%d",&a[i]);
    }
}
void workone(int x){
    int i=x;
    stack<int>s;
    int sz=0;
    for(i=x;col[i]==0;i=a[i]){//往后走  
        sz++;
        mark[i]=sz;
        col[i]=x;
        s.push(i);
    }
    if(col[i]!=x){//走到别的圈上了,往回走然后赋值 
        // 显然，如果和别的链相交，那么后面的路都一样，因此接着这个往回走就行。
        // s.pop();
        int qwq=0;
        while(!s.empty()){
            qwq++;
            ans[s.top()]=qwq+ans[i];
            s.pop();
        }
    }else{//走到了自己的圈上 
    //如果这条链和别的没有相交，等到链自己循环的时候，这个圈上面距离都一样是cirsz
        int cirsz=sz-mark[i]+1;
        int markqwq=1;
        for(int j=i;j!=i || markqwq;j=a[j]){//把这一个圈上的点弄了。
            //（markqwq是因为不管怎样都要有j=i。。但是不满足）
        	markqwq=0;
            ans[j]=cirsz;
            s.pop();
        }
        int qwq=0;
        while(!s.empty()){//倒着标记一条链上的。
            qwq++;
            ans[s.top()]=qwq+ans[i];
            s.pop();
        }
    }
    return ;
}
void work(){
    for(int i=1;i<=n;i++){
        if(col[i]==0){
            workone(i);
        }
    }
    for(int i=1;i<=n;i++){
        // cout<<ans[i]<<endl;
        printf("%d\n",ans[i]);
    }
}
int main(){
    init();
    work();

    return 0;
}
```