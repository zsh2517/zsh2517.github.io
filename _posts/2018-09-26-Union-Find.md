---
layout: post
title: 并查集
categories: structure
description: 简化版本的并查集
keywords: 并查集 
tags: 并查集
---

# 并查集

---

 [洛谷 P3367 【模板】并查集](https://www.luogu.org/problemnew/show/P3367)

```cpp
#include <iostream>
#define MX 10010
using namespace std;
int fa[MX];
int n,m;
int find(const int x){
	return fa[x]==x?x:fa[x]=find(fa[x]);
}
void un(const int x,const int y){
	fa[find(x)]=find(y);
}
int main(){
	cin>>n>>m;
	int ope,x,y;
	for(int i=1;i<=n;i++){
		fa[i]=i;
	}
	for(int i=1;i<=m;i++){
		cin>>ope>>x>>y;
		if(ope==1){
			un(x,y);
		}else{
			cout<<"NY"[find(x)==find(y)]<<endl;
		}
	}
}
```

当然由于并查集肯定不可能专门去考（除了17年那种等等）

可以写到一个结构体/类（struct/class）方便应用。

```cpp
#include <iostream>
#include <cstdlib>
#include <cmath>
#include <cstring>
#include <cstdio>
using namespace std;
struct node{
	int x,y;
} a[55];
int n;
struct uf{//并查集 
	int fa[100];
	int find(int x){
		return fa[x]==x?x:fa[x]=find(fa[x]);
	}
	void un(int x,int y){
		fa[(find(x))]=find(y);
	}
	void init(){//初始化 
		for(int i=1;i<=n;i++){
			fa[i]=i;
		}
	}
	bool all(){//是否只有一个根节点，返回true时为只有一个 
		for(int i=1;i<=n;i++){
			if(find(1)!=find(i)){
				return false;
			}
		}
		return true;
	}
}f;
int operator *(node a,node b){//为了方便，定义一个两点距离公式。。。 
	return (abs(a.x-b.x)+abs(a.y-b.y)); 
}
int check(int x){
	f.init();
	for(int i=1;i<=n;i++) {
		for(int j=1;j<=n;j++){
			int dis= a[i]*a[j];
			if(dis<=x*2){
				f.un(i,j);
			}
		}
	}
	return !f.all() ;
}
int search(){
	int left=0;
	int right=0x7fffffff;
	int mid;
	int ans; 
	while(left<=right){
		mid=(left+right)/2;
		if(check(mid)){
			left=mid+1;
			ans=mid;
		}else{
			right=mid-1;
		}
	}
	return ans+1;
}
void init(){
	cin>>n;
	for(int i=1;i<=n;i++){
		scanf("%d%d",&a[i].x,&a[i].y);
	}
}
void work(){
	cout<<search();
}
int main(){
	init();
	work();
	return 0;
}
```