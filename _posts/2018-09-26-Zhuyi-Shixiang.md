---
layout: post
title: 考前注意事项
categories: OI 实用
description: 考前注意事项
keywords: 考前注意事项 warnings
---

# 注意事项

---

## 库文件

1.不要`#include<bits/stdc++.h>`

2.记住memset是在头文件`cstring` `string.h`声明的

3.随机函数是`cstdlib`，包括`srand(int seed)` `rand(int x)`两个

4.时钟做种子时，头文件有`ctime`，函数是`time(0)`，更新是1s一个值

5.例如`memset`，`strlen`，`strstr`等和字符串处理相关的函数在库`<cstring>`中；`abs`在`<cstdlib>`中；`fabs`，`sin`，`sqrt`等数学函数在`<cmath>`中(来自 [提交时G++、C++的区别](https://blog.csdn.net/disparity_cjk/article/details/53261160)）

## 子程序

1.不能开的太大，会爆栈，比如这个，在子程序会爆，然而主程序没事

```cpp
#define MX 1000010

int vis[MX]={0};
int dis[MX];
```
对于下面代码
```
void dijkstra(int bgn){
    cout<<"***";
    int vis[MX]={0};
    int dis[MX];
    ////////////////////////
}
```

这样连第一个都不会执行（`cout<<"***"`）
