---
layout: post
title: "P9947 [USACO20JAN] Photoshoot B题解"
date:   2025-3-2
tags: [题解]
comments: true
author: qlqaq
---

### P9947 [USACO20JAN] Photoshoot B题解
纯模拟！

在 $a _ {1}$ 算出来之后，我们就可以通过 $b$ 数组可以求出以后 $a$ 数组的所有元素。

要判断是否为排列，我们可以使用一个 $vis$ 做桶，为了保证字典序最小，我们可以从 $1$ 开始枚举，每次枚举前要清空一下 $vis$ 数组，最后使用 check 函数判断一下是否为排列。

一旦找到正解，立马输出。

### 代码

```
#include<bits/stdc++.h>
using namespace std;
int n,b[1005],a[1005];
bool vis[1005],f;
bool check(){
	for(int i=1;i<=n;i++){
		if(!vis[i]){
			return false;
		}
	}
	return true;
}
int main(){
	cin>>n;
	for(int i=1;i<n;i++){
		cin>>b[i];
	}
	for(int i=1;i<b[1];i++){
		memset(vis,0,sizeof(vis));
		vis[i]=1;
		a[1]=i;
		f=1;
		for(int j=2;j<=n;j++){
			if(b[j-1]-a[j-1]<=0){
				f=0;
				break;
			}
			a[j]=b[j-1]-a[j-1];
			if(vis[a[j]]){
				f=0;
				break;
			}
			vis[a[j]]=1;
		}
		if(f&&check()){
			break;
		}
	}
	for(int i=1;i<=n;i++){
		cout<<a[i]<<" ";
	}
	return 0;
}
```
