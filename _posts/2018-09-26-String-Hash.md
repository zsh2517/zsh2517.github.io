---
layout: post
title: 字符串和hash
categories: OI 知识 字符串 hash 算法
description: 字符串和字符串hash
keywords: 字符串 hash

---

<span id = "mdgototop"></span>

# 字符串-哈希

```cpp
#include <iostream>
using namespace std;
int main(){
	string a;
	long long hash;
	int mul,mod;
	//cout<<"INPUT STRING:";
	cin>>a;
	//cout<<"INPUT mul   mod:";
	cin>>mul>>mod;
	for(int i=0;i<a.length();i++){
		hash=((hash+a[i]*mul)%mod+mod)%mod;
	}
	cout<<hash;
}
```

将字符串转化为mul进制，之后对mod取模

字符串匹配数目案例

```cpp
#include <iostream>
#include <cmath> 
using namespace std;
int main(){
	string a,b;
	a="qwq";
	b="Someonewhoalwayssayqwqwqisaqwqer";
	long long hash=0;
	long long mod=233;
	long long mul=67;
	long long mulx=int(pow(67,a.length()))%mod;
	long long ha=0,hb[10010]={0};
	for(int i=0;i<a.length();i++){
		ha=(ha*mul+a[i])%mod;
	}
	cout<<ha<<endl;
	hb[0]=b[0];
	for(int i=1;i<b.length();i++){
		hb[i]=(hb[i-1]*mul+b[i])%mod;
		if(i>=a.length()){
			hash=((hb[i]-hb[i-a.length()]*mulx)%mod+mod)%mod;
			//hash为从b中前面a.length()个字符到b[i]的hash
			cout<<b[i]<<i<<" "<<hash<<(hash==ha?"***":"")<<endl;
		}
	}
}
```

`\[

`\( (x\%mod+mod)\%mod \)`

对x取mod的模并且一定得到一个正数

`\( x \% mod之后得到一个数 \)` 

大于`\( (-mod,0]\quad(x\in(-∞, 0]\large) \)`或者`\( [0,mod)\quad(x\in[0,+∞)) \)`

此时加上mod一定得到正数，之后取模即可

```cpp
#include <iostream>
#include <cstdio>
using namespace std;
unsigned int hasha;
unsigned int hash;
unsigned int h[1000010];
string a,b;
void init(){
	hasha=0;
	hash=0;
	memset(h,0,sizeof(h));
	cin>>a>>b;
//	scanf("%s%s",&a,&b); 
}
void work(){
	unsigned int mod=1;
	int ans=0;
	for(int i=0;i<a.length();i++){
		hasha=hasha*233333+a[i];
		mod*=233333; 
	}
	h[0]=b[0];
	for(int i=1;i<b.length();i++){
		h[i]=h[i-1]*233333+b[i];
		if(i>=a.length()-1){
			if((h[i]-h[i-a.length()]*mod)==hasha){
				ans++;
			}
		}
	}
	cout<<ans<<endl;
}
int main(){
//	freopen("test1.in","r",stdin); 
//	freopen("test.out","w",stdout); 
	int t;
	cin>>t;
	for(int i=1;i<=t;i++){
		init();
		work();
	}
}
```