---
layout: post
title: 树状数组
categories: OI 知识 树状数组 数据结构
description: 树状数组的各种应用
keywords: 树状数组 线段树 区间
---

<span id = "mdgototop"></span>

# 树状数组

---

## 一维树状数组

### 单点更改，区间求和

[回到顶部](#mdgototop)

```cpp
#include <iostream> 
#define MX 500010
#define lowbit(x) (x&(-x)) 
using namespace std;
int n;
int c[1000],a[1000];
void add(int x,int y){//对于节点x加上y
	for(;x<=n;x+=(lowbit(x))){
		c[x]+=y;
	}
}
int sum(int x){//计算1..x的求和，类似于前缀和
	int ans=0;
	for(;x>=1;x-=lowbit(x)){
		ans+=c[x];
	}
	return ans;
}
int query(int left,int right){//区间查询，就是利用前缀和的思想
	return sum(right)-sum(left-1);
}
int main(){
	cin>>n;
	for(int i=1;i<=n;i++){
		cin>>a[i];
		update(i,a[i]);
	}
	int l,r;
	while(1){
		cin>>l>>r;
		cout<<query(l,r);
	}
}
```

### 区间修改，单点求值

[回到顶部](#mdgototop)

```cpp
#include <iostream>
#define MX 500010
#define lowbit(x) (x&(-x))
using namespace std;
int n,m,a[1000],c[1000];
void add(int x,int k){
    for(;x<=n;x+=lowbit(x)){
        c[x]+=k;
    };
}
int sum(int x){
    int ans=0;
    for(x;x>=1;x-=lowbit(x)){
        ans+=c[x];
    }
    return ans;
}
int main(){
    cin>>n>>m;
    for(int i=1;i<=n;i++){
        cin>>a[i];
    }
    int q,w,e;
    for(int i=1;i<=m;i++){
        cin>>q;
        if(q==1){
            cin>>q>>w>>e;
            add(q,e);   
            add(w+1,-e);
        }else{
            cin>>q;
            cout<<a[q]+sum(q)<<endl;
        }
    }
}
```

### 高级应用：区间修改&区间求值

![image_1citbhvdu1p131tviepd1vscr6t1p.png-24.2kB][1]

如图，上面是线段树，下面是树状数组。

在区间加法和查询明显代码量以及时空效率都优于线段树。

当然如果要支持最大最小什么的可能只能用线段树了。

```cpp
#include <iostream>
#define lowbit(x) (x&(-x))
#define MX 100010
#define LL long long 
using namespace std;
LL n,m,q,c1[MX],c2[MX],a[MX];
void add(LL *r,LL x,LL k){//采用LL *r传递每次要修改的数组
    for(;x<=n;x+=lowbit(x)){
        r[x]+=k;
    }
}
LL sum(LL *r,LL x){
    LL ans=0;
    for(;x>=1;x-=lowbit(x)){
        ans+=r[x];
    }
    return ans;
}
int main()
{
    LL sum1,sum2;
    cin>>n>>m;
    for(int i=1;i<=n;i++){
        cin>>a[i];
        add(c1,i,a[i]-a[i-1]);
        add(c2,i,(i-1)*(a[i]-a[i-1]));
    }
    int q,l,r,k;
    for(int i=1;i<=m;i++){
        cin>>q;
        if(q==1){
            cin>>l>>r>>k;
            add(c1,l,k);
            add(c1,r+1,-k);
            add(c2,l,(l-1)*k);
            add(c2,r+1,-r*k);
        }else{
            cin>>l>>r;
            sum1=(l-1)*sum(c1,l-1)-sum(c2,l-1);
            sum2=r*sum(c1,r)-sum(c2,r);
            cout<<(sum2-sum1)<<endl;
        }
    }
    return 0;
}
```

## 二维树状数组

等待填坑

[回到顶部](#mdgototop)


  [1]: http://static.zybuluo.com/zhshh/4in1i4epvvf13esrr05agv40/image_1citbhvdu1p131tviepd1vscr6t1p.png