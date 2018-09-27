---
layout: windows下对拍及其应用
title: template page
categories: OI windows 对拍
description: windows下面的对拍介绍
keywords: windows 对拍
---
# windows下对拍及其应用

---
<font color="#FF0000">**WARN!**</font>
`#include <bits/stdc++.h>`在OI等里面不一定能应用，下面只是为了减小长度而已
bits库实际上就是`#include <XXX>`了一堆而已

## 经典代码

对拍.bat

```batch
:loop
makedata.exe
K.exe
Kture.exe
fc a.out b.out
if %errorlevel%==0 goto loop
pause 
```

解释

```
:loop
```

创建叫做`loop`的标签

```
makedata.exe
K.exe
Kture.exe
```

运行makedata.exe，K.exe,Kture.exe

其中makedata输出到x.in，然后K.exe从x.in读入，输出到a.out,Ktrue.exe从x.in读入，输出到b.out

```batch
fc a.out b.out
if %errorlevel%==0 goto loop
pause 
```

比较a.out b.out

fc是windows下面一个程序，简单来说如果两个文件相同返回0，不同返回1

`%errorlevel%`是一个变量，意思是上一行代码的返回值

如果 返回==0 跳转到loop（第一行标签）

如果 返回不等于0 跳过这句话，执行pause(暂停)，然后程序结束

## 示例

### duipai.bat

```
:loop
echo %random%|data.exe
baoli.exe
mine.exe
fc mine.out baoli.out
if %errorlevel%==0 goto loop
pause 
```

### data.exe

输出测试数据到`in.in`

```cpp
#include <bits/stdc++.h>
using namespace std;
int main(){
	int rands;
	freopen("in.in","w",stdout); 
	cin>>rands;
	srand(rands);//随机数种子，一会再说 
	cout<<rand()<<" "<<rand();
	return 0;
}
```

由于windowsCPP的特性，`srand(time(0))`一秒只有一个种子，而自己的程序不会太慢，所以直接输入一个种子即可

在`echo %random%|data.exe`里面，是%random%是一个随机数（由`duipai.bat`解析器`cmd.exe`随机，每次都是随机的）

`|`是管道运算，把前面命令应该显示的东西作为标准输入给后面的，echo XXX是显示XXX

这句话意思是把`%random%`（叫做`random`的变量，在没有手动声明其值时，每次调用都是随机数）输入给`data.exe`
	
### baoli.exe

一个已知正解的程序，比如包括暴力求解程序，别人、网上的正解等

```cpp
#include <bits/stdc++.h>
using namespace std;
int main(){
    int q,w;
    freopen("in.in","r",stdin);
	freopen("baoli.out","w",stdout); 
    cin>>q>>w;
    int ans=0;
    if(q>0) {
        for(int i=1;i<=q;i++){
            ans++;
        }
    }else{
        for(int i=-1;i>=q;i--){
            ans--;
        }
    }
    if(w>0) {
        for(int i=1;i<=w;i++){
            ans++;
        }
    }else{
        for(int i=-1;i>=w;i--){
            ans--;
        }
    }
    cout<<ans;
    return 0;
}
```

### mine.exe

自己的程序或者测试的程序

为了显示功能，这里是随机出错。。

```
#include <bits/stdc++.h> 
using namespace std;
int main(){
    int q,w;
    freopen("in.in","r",stdin);
	freopen("mine.out","w",stdout); 
    cin>>q>>w;
    srand(time(0)); 
    int r=rand()%20; 
    if(r>=10){
    	cout<<q+w+1;
    }else{
    	cout<<q+w;
    }
    return 0;
}
```

最后双击`duipai.bat`即可看到效果