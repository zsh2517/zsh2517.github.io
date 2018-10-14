---
layout: post
title: 二分三分题
categories: solution
description: 二分三分题
keywords: 二分答案 二分查找 三分算法
tags: 二分
show: true
---

<span id = "mdgototop"></span>

# 二分和三分题

---

# 二分

## 愤怒的牛（其他：跳石头，丢瓶盖）

[回到顶部](#mdgototop)

### 算法

二分答案区间，每次check，检查两个标记的距离，如果小于x，那么去掉。判断去掉的个数。

### 题目

>Farmer John建造了一个有N(2<=N<=100,000)个隔间的牛棚，这些隔间分布在一条直线上，坐标是x1,...,xN (0<=xi<=1,000,000,000)。
他的C(2<=C<=N)头牛不满于隔间的位置分布，它们为牛棚里其他的牛的存在而愤怒。为了防止牛之间的互相打斗，Farmer John想把这些牛安置在指定的隔间，所有牛中相邻两头的最近距离越大越好。那么，这个最大的最近距离是多少呢？

**输入格式：**

第1行：两个用空格隔开的数字N和C。

第2~N+1行：每行一个整数，表示每个隔间的坐标。

**输出格式：**

输出只有一行，即相邻两头牛最大的最近距离。

```cpp
#include <iostream>
#include <algorithm>
using namespace std;
int n,m;
int a[10000010];
int check(int x){
	int used=0;
	int last=-0x3f3f3f3f;
	for(int i=1;i<=n;i++){
		if(a[i]-last>=x){
			used++;
			last=a[i];
		}
	}
	if(used>=m)return true;
	return false;
}
int search(){
	int left=1;
	int right=a[n];
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
	return ans;
}
void init(){
	cin>>n>>m;
	for(int i=1;i<=n;i++){
			cin>>a[i];
	}
	sort(a+1,a+n+1);
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

# 三分

## 曲线求极值

[回到顶部](#mdgototop)

### 题目

>【题目描述】
明明做作业的时候遇到了n个二次函数Si(x)= ax2 + bx + c，他突发奇想设计了一个新的函数F(x) = max(Si(x)), i = 1...n.
明明现在想求这个函数在[0,1000]的最小值，要求精确到小数点后四位四舍五入。
【输入数据】
输入包含T 组数据 (T < 10) ，每组第一行一个整数 n(n ≤ 10000) ,之后n行，每行3个整数a (0 ≤ a ≤ 100), b (|b| ≤ 5000), c (|c| ≤ 5000) ，用来表示每个二次函数的3个系数，注意二次函数有可能退化成一次。
【输出数据】
每组数据一个输出，表示新函数F(x)的在区间[0,1000]上的最小值。精确到小数点后四位，四舍五入。

### 算法

易得很多二次函数凑到一块，然后取max，可以从轮廓上看出来一定是V型，只是有折点什么的，两边斜率不太一样。因此整体就构造一个`\( f(x)=max^{n}_{i=1}\{f(x)\} \)`，然后正常三分即可。

```cpp
// 代码丢了。。。
```

# 连续区间最大和

[回到顶部](#mdgototop)

### 1.不要求长度

从左往右累加，然后判断。

`\(sum=\Sigma^{r}_{i=l}a_i \)`，如果`\( sum>0 \)`那么 `\( a_i \)`的加入会比直接从`\( a_i \)`开始的值更大，那么加上。如果`\( sum≤0 \)`那么直接从`\( a_i \)`开始有更优解。此时`\( sum=a_i \)`

### 2.长度至少为L最大序列

二分结果，判定是否有一个长度不小于L的子序列，平均数不小于二分check()的值

对于这个check()条件（<font color="orange">注意，这里并不需要确保求出最大值，只是求一个合适的满足的解即可，求值是二分的事，这个不能弄混</font>）

这样如果这个子序列每个数都减去二分的值，那么就转化为了求最大连续子序列的长度能不能到长度为L，这个可以像上面那样说的用尺取法滚动取值。因为长度为L，那么[l,r]的r一定不小于L，所以r从L开始计算，利用前缀和快速计算长度。

```cpp
#include <cmath>
#include <cstdio>
#define eps 1e-6
#include <iostream>
#define MX 100010
using namespace std;
double a[MX],b[MX],c[MX];
int main(){
    int n,length;
    cin>>n>>length;
    for(int i=1;i<=n;i++){
//        cin>>a[i];
		scanf("%lf",&a[i]); 
    }
    double left=-1e+6;
    double right=+1e+6;
    double mid;
    while(left<=right && fabs(left-right)>eps){
        mid=(left+right)/2;
        //---------------check(mid)--------------------
        for(int i=1;i<=n;i++){//减去check的mid
            b[i]=a[i]-mid;
        }
        for(int i=1;i<=n;i++){//计算前缀和
            c[i]=c[i-1]+b[i];
        }
        double mval=1e+8;//充分大的cnt-l以及之前的最小值
        double ans=-1e+8;//充分小的ans，即记录符合条件长度的
        //一段区间，最大长度是多少
        for(int i=length;i<=n;i++){//下面确保了这段长度大于等于L
            mval=min(mval,c[i-length]);//val始终为i-l前面的最小值
            ans=max(ans,c[i]-mval);//长度大于等于L的区间最大和是？
        }
        //-----------------------------------------
        if(ans>0){//b[i]和大于零==>a[i]和大于avr*(r-l+1)，即sum
            left=mid;
        }else{
            right=mid;
        }
    }
    cout<<int(right*1000)<<endl;
    return 0;
}
```
