---
layout: post
title: 最小生成树
categories: OI 图论 最小生成树 知识 算法
description: 最小生成树 相关的算法那
keywords: 最小生成树 prim kruskal
---

<span id = "mdgototop"></span>

# 图论-最小生成树

---

存图就不说了。。

最小树模板题目[P3366 【模板】最小生成树](https://www.luogu.org/problemnew/show/P3366)

# 算法

## kruskal

### 思路

排序，用并查集维护树，使得在同一棵树上的两个节点不会自己相连。（树1和树2可以相连？这就相当于是把两个树合并了）

### 代码

```cpp
#include <iostream>
#include <algorithm>
#define MX 1000010
using namespace std;
struct node{
	int p1,p2,w;
}a[MX];
int fa[MX];
int find(int x){
	return fa[x]==x?x:fa[x]=find(fa[x]);
}
void un(int x,int y){
	fa[find(x)]=find(y);
} 
int operator<(node a,node b){
	return a.w<b.w;
}
int n,m;
void init(){
	cin>>n>>m;
	for(int i=1;i<=m;i++){
		cin>>a[i].p1>>a[i].p2>>a[i].w;
	}
	for(int i=1;i<=n;i++){
		fa[i]=i;
	}
}
void work(){
	sort(a+1,a+m+1); 
	int ans=0,tot=0;
	for(int i=1;i<=m;i++){
		if(find(a[i].p1)!=find(a[i].p2)){
			un(a[i].p1,a[i].p2);
			ans+=a[i].w;
			tot++;
		}
		if(tot==n-1)break;
	}
	if(tot==n-1){
		cout<<ans<<endl;
	}else{
		cout<<"orz";
	}
}
int main(){
	init();
	work();
}
```

## prim

[回到顶部](#mdgototop)

这个和dijkstra形似。。详见最短路文对比

### 思路

n次循环，每次都选择当前最小dis的minj扩展这棵树。之后把与minj相连的所有节点更新为<font color="red">距离树最近</font>的dis

由于kruskal是基于边权的排序，所以没有方向，而prim是有明确起点终点的前向星存图，所以必须要正反存图

### 代码

```cpp
#include <iostream>
#include <cstdio>
#include <cstring>
#define INF 0x3f3f3f3f
#define MX 1000010
using namespace std;
struct node{
    int nxt;
    int v;
    int w;
}edge[MX];
int tot,ans,n,m;
int head[MX];
int dis[MX];
int vis[MX]={0};
void add(int u,int v,int w){
    tot++;
    edge[tot].v=v;
    edge[tot].w=w;
    edge[tot].nxt=head[u];
    head[u]=tot;
}
void init(){
    memset(head,-1,sizeof(head));
    cin>>n>>m;
    int a,b,c;
    for(int i=1;i<=m;i++){
        cin>>a>>b>>c;
        add(a,b,c);//正反存图
        add(b,a,c);
    }
}
void prim(){
    memset(dis,0x3f,sizeof(dis));
    dis[1]=0;
    int minj,mindis;
    for(int i=1;i<=n;i++){
        minj=-1;
        mindis=INF;
        for(int j=1;j<=n;j++){//循环每个节点，从而找到dis最小的节点（稍后说明dis）
            if(!vis[j] && dis[j]<mindis){
                minj=j;
                mindis=dis[j];
            }
        }
        if(minj==-1){//正常情况下（连通图）应该是n次恰好找完n个节点。如果是-1，没找完。。说明有不连通
			cout<<"orz"<<endl;
            return ;
        }
        vis[minj]=1;//上面选择的最优节点。登记vis，记录ans
        ans+=dis[minj];
        for(int j=head[minj];j!=-1;j=edge[j].nxt){//依次更新和minj这个节点相连的所有节点
             int v=edge[j].v;
             if(!vis[v] && dis[v]>edge[j].w){//由于树内等价，所以这里更新为距离树的最小距离，其中!vis[v]写不写都行
                 dis[v]=edge[j].w;//和树的距离，因为minj在树上，因此更新为min(dis[v],edge[j].w)
             }//区别于dijkstra，由于要看从起点开始的最短路，因此动态更新为最短距离
        }
    }
    cout<<ans;
}
void work(){
    prim();
}
int main(){
    init();
    work();
}
```

# 题目

[回到顶部](#mdgototop)

