---
layout: post
title: template page
categories: 
description: 
keywords: 
tags: 
show: false
---

[P2296 寻找道路](https://www.luogu.org/problemnew/show/P2296)

## 題目描述

在有向图 G 中，每条边的长度均为 1，现给定起点和终点，请你在图中找一条从起点到终点的路径，该路径满足以下条件：

路径上的所有点的出边所指向的点都直接或间接与终点连通。
在满足条件 1的情况下使路径最短。
注意：图 G 中可能存在重边和自环，题目保证终点没有出边。

请你输出符合条件的路径的长度。

## 題目思路

双向存图。首先反向扫描一遍找到所有可以到达目标终点的，然后因为路径上的点的出点都要间接或者直接连通终点。也就是说凡是**不连通**或者**指向不连通**的都不满足要求，相当于**所有不连通的点和他们的父节点去掉**。（即单独标记出来符合要求的点），之后再BFS（或者说类似SPFA）即可。

```cpp
#include <iostream>
#include <cstring>
#include <cstdio>
#include <cstdlib>
#include <queue>
using namespace std;
struct node{
    int u,v,nxt,pre;
}edge[200010];
int head[10010],tail[10010];
int tot=0;
int n,m;
int f,t;
void add(int u,int v){
    tot++;
    edge[tot].u=u;
    edge[tot].v=v;
    edge[tot].nxt=head[u];
    edge[tot].pre=tail[v];
    head[u]=tot;
    tail[v]=tot;
}
void init(){
    memset(head,-1,sizeof(head));
    memset(tail,-1,sizeof(tail));
    cin>>n>>m;
    int a,b;
    for(int i=1;i<=m;i++){
        cin>>a>>b;
        add(a,b);
    }
    cin>>f>>t;
}
void work(){
    int vis[10010]={};
    int use[10010]={};
    queue<int>q;
    q.push(t);
    while(!q.empty()){//先扫描一遍找到可以到目标节点的
    	int qwq=q.size(); 
        int x=q.front();
        q.pop();
        vis[x]=1;
        for(int i=tail[x];i!=-1;i=edge[i].pre){
            int p=edge[i].u;
            if(!vis[p]){
                vis[p]=1;
                q.push(p);
            }
        }
    }
    for(int i=1;i<=n;i++){//去掉不连通的
        use[i]=1-vis[i];
    }
    for(int i=1;i<=n;i++){//去掉指向不连通的点的点
        if(!vis[i]){
            for(int j=tail[i];j!=-1;j=edge[j].pre){
                use[edge[j].u]=1;
            }
        }
    }
    q.push(f);
    int d=1;
    int dis[10010];
    dis[f]=0;
    while(!q.empty()){//走一个最短路
        int x=q.front();
        q.pop();
        if(x==t){
            cout<<dis[t]<<endl;
            exit(0);
        }
        for(int i=head[x];i!=-1;i=edge[i].nxt){
        	int p=edge[i].v;
            if(!use[p]){
                use[p]=1;
                dis[p]=dis[x]+1;
                q.push(p);
            }
        }
    }
    cout<<-1<<endl;
}
int main(){
    init();
    work();

    return 0;
}
```