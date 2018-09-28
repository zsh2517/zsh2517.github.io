---
layout: post
title: 区间DP
categories: DP 题解
description: some word here
keywords: DP 区间 动态规划
---

# 定义

在区间上进行的动态规划 ~~（废话）~~，通常的类型就是合并的问题，即按照线性或者环形相邻的可以（可能）合并成为1个，这样求最大最小值。

## [P3146 [USACO16OPEN]248](https://www.luogu.org/problemnew/show/P3146)

本题的优化版本 [P3147 [USACO16OPEN]262144](https://www.luogu.org/problemnew/show/P3147)

$$1*n$$的地图上进行248（类似于2048，区别是 不乘2而是加1，求最大能合并出多少。）

思路：

如果考虑`dp[l][r]`，假设在`k`的时候，`[l,k]`和`[k+1,r]`可以拼出。则区间条件首先就是`dp[l][k]==dp[k+1][r]`，这样的话，`dp[l][r]==dp[l][k]+1`，如果不能拼出，则`dp[l][r]=0`因为这样的话这个整体不能作为一个。

转移方程

$$
dp[l][r]=
\begin{cases}
dp[l][k]+1&{dp[l][k]=dp[k+1][r]}\\
0& dp[l][k]\neq dp[k+1][r]
\end{cases}
$$

代码

```cpp
#include <iostream>
using namespace std;
int n,a[255],dp[255][255];
void init(){
    cin>>n;
    for(int i=1;i<=n;i++){
        cin>>a[i];
    }
}
void work(){
    int len,l,r;
    int ans=0;
    for(int i=1;i<=n;i++){
        dp[i][i]=a[i];
    }
    for(len=2;len<=n;len++){
        for(l=1;l+len-1<=n;l++){
            r=l+len-1;
            for(int k=l;k<r;k++){
                if(dp[l][k]==dp[k+1][r]){
                    dp[l][r]=max(dp[l][r],dp[l][k]+1);
                    ans=max(dp[l][r],ans);
                }
            }
        }
    }
    cout<<ans;
}
int main(){
    init();
    work();
}
```

## [P2858 [USACO06FEB]奶牛零食Treats for the Cows](https://www.luogu.org/recordnew/show/11217069)

思路：依然是从小到大枚举。

**正着进行的最大值和反向进行的最大值相同。**，这样的话，反向对每个节点都初始化为`dp[i][i]=n*a[i]`，之后依然从`len=2`开始DP即可。

转移方程

$$
dp[l][r]=max(dp[l][r-1]+a[r]*(n-len+1),\\dp[l+1][r]+a[l]*(n-len+1))
$$

```cpp
#include <iostream>
using namespace std;
int n,a[2200],dp[2100][2100];
void init(){
    cin>>n;
    for(int i=1;i<=n;i++){
        cin>>a[i];
    }
}
void work(){
    int len,l,r,k;
    for(int i=1;i<=n;i++){
        dp[i][i]=a[i]*n;
    }
    for(len=2;len<=n;len++){
        for(l=1;l+len-1<=n;l++){
            r=l+len-1;
            dp[l][r]=max(dp[l][r-1]+a[r]*(n-len+1),dp[l+1][r]+a[l]*(n-len+1));
        }
    }
    cout<<dp[1][n];
}
int main(){
    init();
    work();

    return 0;
}
```

## [P1880 [NOI1995]石子合并](https://www.luogu.org/problemnew/show/P1880)

环形问题。

转移方程（以最大为例）

$$
dp[l][r]=max\{dp[l][k],dp[k+1][r]\}+sum(l,r)\ \ \ \ k\in{[l,r)}\\\text{(因为dp[l][r]表示的是[l,r]，因此k<r)}
$$

其中求和的方法是前缀和

拆环的方法是断环为链，然后为了得到断口处，长度扩大二倍。但此时仍限定`len<=n`这样`l = 1 -> n`就取完了所有情况，最后再扫描一遍。

```
#include <iostream>
#define INF 0x3f3f3f3f
using namespace std;
int a[250],mx[250][250],mn[250][250],n,sum[250];
void init(){
    cin>>n;
    for(int i=1;i<=n;i++){
        cin>>a[i];
        a[i+n]=a[i];
    }
    for(int i=1;i<=2*n;i++){
        sum[i]=sum[i-1]+a[i];
    }
}
void work(){
    int len,r,l,k;
    for(len=2;len<=n;len++){
        for(l=1;l+len-1<=2*n;l++){
            r=l+len-1;
            mx[l][r]=0;
            mn[l][r]=INF;
            for(k=l;k<r;k++){
                mx[l][r]=max(mx[l][k]+mx[k+1][r]+sum[r]-sum[l-1],mx[l][r]);
                mn[l][r]=min(mn[l][k]+mn[k+1][r]+sum[r]-sum[l-1],mn[l][r]);
            }
        }
    }
    int ansmn=INF,ansmx=0;
    for(l=1;l+n-1<=n*2;l++){
        ansmn=min(ansmn,mn[l][l+n-1]);
        ansmx=max(ansmx,mx[l][l+n-1]);
    }
    cout<<ansmn<<endl<<ansmx;
}
int main(){
    init();
    work();
}
```