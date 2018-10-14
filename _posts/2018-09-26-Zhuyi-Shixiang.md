---
layout: post
title: 考前注意事项
categories: trick
description: 考前注意事项
keywords: 考前注意事项 warnings
tags: 考试技巧
show: true
---

# 注意事项

---

## 库文件

1.不要`#include<bits/stdc++.h>`

2.记住memset是在头文件`cstring`声明的

3.随机函数是`cstdlib`，包括`srand(int seed)` `rand(int x)`两个

4.时钟做种子时，头文件有`ctime`，函数是`time(0)`，更新是1s一个值

5.例如`memset`，`strlen`，`strstr`等和字符串处理相关的函数在库`<cstring>`中；`abs`在`<cstdlib>`中；`fabs`，`sin`，`sqrt`等数学函数在`<cmath>`中(来自 [提交时G++、C++的区别](https://blog.csdn.net/disparity_cjk/article/details/53261160)）

6.一些库文件有特殊的变量名，比如`time`（`time.h`里面的`time()`），`nan` `y0` `y1`等等都在`cmath`库里面定义了变量等。cmath:`x1` `y1` others:`count` `max` `min` `round` `distance`

>如果记不住例外情况，那么可以用拼音，而不是单词命名。而且如果把元音删掉也会少不少。比如（`next`->`nxt`）以及缩写（`distance`->`dis`）

## 变量

### 1.空间适度

大的定义到主程序否则会爆栈，比如这个，在子程序会爆，然而主程序没事

比如在开始的时候写`memset(xx,-1,sizeof(xx));//xx是内存占用大的变量。`之后`while(1)`，然后看任务管理器内存多大。（不要忘了删掉，因为memset在这里既占时间也没啥用**（在这里仅仅是一个调试）**）

对于下面代码
```cpp
#define MX 1000010

void dijkstra(int bgn){
    int vis[MX]={0};
    int dis[MX];
    cout<<"***";
    int vis[MX]={0};
    int dis[MX];
    ////////////////////////
}
```

这样连第一个都不会执行（`cout<<"***"`）

2.RE崩溃的话一定是`return 非零`，这个如果不测试返回值，很难发现。(dev cpp 会自动显示的，这里指命令行编译)

RE情况很多，比如数组越界，变量太大，递归太深，`scanf`不`&`等等

出现情况是返回不为0。

3.初始化

根据测试（一般电脑、评测机）

`a[10010]={0}`\<`memset(a,0,sizeof(a))`\<`for(int i=0;i<10010;i++)a[i]=0;`

如果需要赋值非零的，`memset`是字节填充，也就是说INF最大是`0x7f7f7f7f`（`memset` `0x7f`），如果是有相加操作，最大是`0x3f3f3f3f`），即填充（`0x3f`）

**如果WER没有Disabled，才会弹出停止运行警告！**

返回值在cmd里面是`%errorlevel%`，比如输出是`echo %errorlevel%`

## 调试

### 1.**注释/删除相关调试代码！**

可以有的做法：

1.注释掉代码（推荐！）

2.宏定义（`#ifdef`）

详见：[C/C++预处理指令#define,#ifdef,#ifndef,#endif…](https://www.cnblogs.com/zi-xing/p/4550246.html)

这个可以直接放到devc++里面的预编译指令。（不会，，而且我没用过）

```cpp
#define STR

#ifdef STR
    printf(STR(VCK));
#endif
```

3.宏定义（`#define D if(1)`）

```cpp
#define D if(1)
//不需要DEBUG的话，直接把if(1)换成if(0)即可
int main(){
D    printf("DEBUG MESSAGE");
}
```

4.标准错误流

除了常用的标准输入`stdin`（`scanf` `cin`），标准输出流`stdout`（`printf` `cout`），还有标准错误流`stderr`（似乎要`fprintf(stderr,"%d",a)`，没找到相关的C函数，或者C++的`cerr`）

对于平常的`freopen`，`stdin` `stdout`来说，`cerr`直接输出到屏幕，所以更方便。

**评测是否考虑错误流未知！务必删掉以避免错误**

### 暴力

暴力一定写。如果正解写不出来，直接交暴力，如果写出来了，暴力用来对拍。

## 文件操作

### 1.文件夹目录

只能是如下格式（如果我没记错）

```
NOIP
    HE-111
        question1
            question1.cpp
        question2
            question2.pas
        question3
            question2.cpp
    HE-111.zip
```

压缩包带密码（具体怎么办到时候会说）

另外允许一个题交多个语言，但是测同一个题个不一定，不同的题没事。。

### 2.文件读写

如果用就记准优化模板。是不是需要处理负号，字符等等。

`cin,cout` > `scanf,printf` > `getchar,putchar` 或者 `fread`？（不会）

**关闭文件同步流 `std::ios::sync_with_stdio(false);` 和 `fclose()` 不能同时用，否则无输出！！**

### 其他IO操作

1.读入换行符！

Windows的是`\n\r`，linux是`\n`，在输出的时候，直接写`printf("\n")`，Windows会自动补上`\r`，但是读入的时候不会。也就是说如果要读入（跳过换行符），必须要`getchar()`两个
```cpp
for(int i=1;i<=n;i++){
    for(int j=1;j<=m;j++){
        a[i][j]=getchar();
    }
    getchar();
    getchar();//如果是Linux数据，写一个，Windows数据写2个！
}
```

换行符还有一个问题，就是Windows记事本`notepad.exe`不支持（最新的win10 1809才支持），也就是说Linux下面如下的数据
```
1 2 3
4 5
```
在记事本上是
```
1 2 34 5
```
（当然如果直接读入到程序没有问题。。使用任何非记事本的程序都行）

我印象河北有dev,code::blocks,gvim等等，此外，`write.exe`写字板也支持。

### 关于数据

1.闪退不一定是因为崩溃（崩溃如果是dev普通运行会结束到返回值界面），很有可能是因为读入少了（个别版本有问题）

2.在Dev下，F10运行调用的是dev目录下的`consolepauser.exe yours.exe`，因此大部分情况不会出现闪退，而是自身结束，然后留到consolepauser程序界面（就是最后显示运行时间和返回的）。而F5调用的是gdb，如果不确定在哪出问题，可以试试F5单步调试。**（不要依赖，因为dev很悬。。各种BUG，还有的不支持调试）**


# 未完待续！

```
UPD:2018-10-06-23-14
```