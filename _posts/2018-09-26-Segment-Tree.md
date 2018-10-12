---
layout: post
title: 线段树模板
categories: structure algorithm
description: some word here
keywords: 线段树 区间 数据结构
tags: 线段树 区间
---

<span id = "mdgototop"></span>

# 线段树

---

# 模板

## 单标记（加、max、min）

[回到顶部](#mdgototop)

```cpp 
#include <iostream>
#include <cstdio>
#include <algorithm>
#define cnt tree[root]
#define lr (root<<1)
#define rr ((root<<1)|1)
#define lt tree[lr]
#define rt tree[rr]
#define MX (100010)
#define LL long long
using namespace std;
struct node{
    int left,right;
    LL add,val;
    node(){
        add=0;
    }
}tree[MX<<2];
LL a[MX];
int n;
void pushup(int root){
    cnt.val=lt.val+rt.val;//更新换成自己的操作
}
void pushdown(int root){
    if(cnt.add!=0){
        lt.val=lt.val+cnt.add*(lt.right-lt.left+1);
        lt.add=lt.add+cnt.add;
        rt.val=rt.val+cnt.add*(rt.right-rt.left+1);
        rt.add=rt.add+cnt.add;
        cnt.add=0;
    }
}
void add(int root,int left,int right,int c){
    if(left<=cnt.left && right>=cnt.right){
        cnt.add=cnt.add+c;
        cnt.val=(cnt.val+c*(cnt.right-cnt.left+1));
        return ;
    }
    pushdown(root);
    int mid=cnt.left+cnt.right>>1;
    if(left<=mid)add(lr,left,right,c);
    if(right>mid)add(rr,left,right,c);
    pushup(root);
    return ;
}
LL query(int root,int left,int right){
    if(left<=cnt.left && right>=cnt.right){
        return cnt.val;
    }
    pushdown(root);
    int mid=cnt.left+cnt.right>>1;
    LL ans=0;
    if(left<=mid)ans+=query(lr,left,right);
    if(right>mid)ans+=query(rr,left,right);
    return ans;
}
void build(int root,int left,int right){
    cnt.left=left;
    cnt.right=right;
    if(left==right){
        cnt.val=a[left];
        return ;
    }
    int mid=(cnt.left+cnt.right)>>1;
    build(lr,left,mid);
    build(rr,mid+1,right);
    pushup(root);
    return ;
}
int main(){
    int n,m;
    cin>>n>>m;
    for(int i=1;i<=n;i++){
        cin>>a[i];
    }
    build(1,1,n);
    int left,right,c;
    for(int i=1;i<=m;i++){
        cin>>c;
        if(c==1){
            cin>>left>>right>>c;
            add(1,left,right,c);
        }else{
            cin>>left>>right;
            cout<<query(1,left,right)<<endl;
        }
    }
    return 0;
}
```

## 双标记

[回到顶部](#mdgototop)

```cpp
#include <iostream>
#include <cstdio>
#include <algorithm>
#define cnt tree[root]
#define lr (root<<1)
#define rr ((root<<1)|1)
#define lt tree[lr]
#define rt tree[rr]
#define ci const int
#define MX (100010+10)
#define LL long long
using namespace std;
struct node{
    int left,right;
    LL add,mul,val;
    node(){
        mul=1;
        add=0;
    }
}tree[MX<<2];
LL a[MX];
int n;
LL mod;
void pushup(ci root){
    cnt.val=lt.val+rt.val;
}
void pushdown(ci root){
    if(cnt.mul!=1 || cnt.add!=0){
        lt.val=(lt.val*cnt.mul)%mod;
        lt.val=(lt.val+cnt.add*(lt.right-lt.left+1))%mod;
        lt.add=(lt.add*cnt.mul)%mod;
        lt.add=(lt.add+cnt.add)%mod;
        lt.mul=(lt.mul*cnt.mul)%mod;

        rt.val=(rt.val*cnt.mul)%mod;
        rt.val=(rt.val+cnt.add*(rt.right-rt.left+1))%mod;
        rt.add=(rt.add*cnt.mul)%mod;
        rt.add=(rt.add+cnt.add)%mod;
        rt.mul=(rt.mul*cnt.mul)%mod;

        cnt.mul=1;
        cnt.add=0;
    }
}
void mul(ci root,ci left,ci right,ci k){
    if(left<=cnt.left && right>=cnt.right){
        cnt.mul=(cnt.mul*k)%mod;
        cnt.add=(cnt.add*k)%mod;
        cnt.val=(cnt.val*k)%mod;
        return ;
    }
    pushdown(root);
    int mid=(cnt.left+cnt.right)>>1;
    if(left<=mid)mul(lr,left,right,k);
    if(right>mid)mul(rr,left,right,k);
    pushup(root);
}
void add(ci root,ci left,ci right,ci c){
    if(left<=cnt.left && right>=cnt.right){
        cnt.add=(cnt.add+c)%mod;
        cnt.val=(cnt.val+c*(cnt.right-cnt.left+1))%mod;
        return ;
    }
    pushdown(root);
    int mid=(cnt.left+cnt.right)>>1;
    if(left<=mid)add(lr,left,right,c);
    if(right>mid)add(rr,left,right,c);
    pushup(root);
    return ;
}
LL query(ci root,ci left,ci right){
    if(left<=cnt.left && right>=cnt.right){
        return cnt.val;
    }
    pushdown(root);
    int mid=(cnt.left+cnt.right)>>1;
    LL ans=0;
    if(left<=mid)ans=(ans+query(lr,left,right))%mod;
    if(right>mid)ans=(ans+query(rr,left,right))%mod;
    return ans;
}
void build(ci root,ci left,ci right){
    cnt.left=left;
    cnt.right=right;
    if(left==right){
        cnt.val=a[left];
        return ;
    }
    int mid=(cnt.left+cnt.right)>>1;
    build(lr,left,mid);
    build(rr,mid+1,right);
    pushup(root);
    return ;
}
void pr(){
    for(int i=1;i<=n;i++){
        printf("%3d%7d\n",i,query(1,i,i));
    }
    cout<<endl;
}
int main(){
//    freopen("in.txt","r",stdin);
    int m,t1,t2,t3;
    cin>>n>>m>>mod;
    for(int i=1;i<=n;i++){
        cin>>a[i];
        a[i]%=mod;
    }
    build(1,1,n);
    for(int i=1;i<=m;i++){
        cin>>t1;
        if(t1==1){
            cin>>t1>>t2>>t3;
            mul(1,t1,t2,t3);
        }else{
            if(t1==2){
                cin>>t1>>t2>>t3;
                add(1,t1,t2,t3);
            }else{
                cin>>t1>>t2;
                cout<<query(1,t1,t2)<<endl;
            }
        }
    }
//    pr(); 
}
```