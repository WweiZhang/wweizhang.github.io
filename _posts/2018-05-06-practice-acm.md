---
layout: post
title: '贪心'
date: 2018-05-06
author: wweizhang
cover: '/assets/img/girl.jpg'
tags: algorithm
---

> 日常比赛

**这是今天比赛的题目，来自第四届福建程序设计大赛**

[题目链接](http://acm.fzu.edu.cn/problem.php?pid=2141)

#### 大概意思是说有t组样例，然后n个点（从1-n），m条边，再给出m条边的两边的点，组成一个无向图。要将这些点分为两个组，构成二分图，保证二分图的边至少m/2条边。

####  思考：对于第i个点，假设前i-1个点已经成为一个二分图，就查看与i相连的点是在二分图左边多还是在二分图右边多，哪边少i点就往哪放。先用一个二维数组grp[][]来保存两个点之间是否有连线，color[]来记录点分到哪个组了,没有任何连线点默认分到第一组。最后注意所有变量在每一组数据输入之前都应该初始化，特别是全局变量！

#### 这是一组样例

##### Sample Input
    3 1
    1 0 
    2 1
    1 2
    3 3
    1 2
    2 3
    1 3
 ##### Sample Output
    1 1
    0
    1 1
    1 2
    2 1 2
    1 3
#### 附上代码


```clike
#include <iostream>
#include <string>
#include <algorithm>
#include <cmath>
#include <cstdio>
#include <iomanip>
#include <cstdlib>
using namespace std;
int color[105];
bool grp[105][105];
int n,m;
int a[105],b[105];
int ca=0,cb=0;
int f(int u){
	int sum1=0;
	int sum2=0;
	for(int i=1;i<=n;i++){
		if(grp[u][i]){
			if(color[i]==1){
				sum1++;
			}
			else{
				sum2++;
			}
		}	
	}
	if(sum1>sum2){
		color[u]=1;
		b[cb++]=u;
	}
	else{
		color[u]=1;
		a[ca++]=u;
	}

} 
int main(){
	int t;
	cin>>t;
	while(t--){
		memset(grp, false, sizeof(grp)); 
		memset(color, 0, sizeof(color)); 
		ca=cb=0;
		cin>>n>>m;
		for(int i=0;i<m;i++){
			int v,u;
			cin>>u>>v;
			grp[u][v]=grp[v][u]=true;
		}
		for(int i=1;i<=n;i++){
			f(i);
		}
		cout<<ca<<" ";
		for(int i=0;i<ca;i++){
			cout<<a[i]<<" ";
		}
	
		cout<<endl<<cb<<" ";
		for(int i=0;i<cb;i++){
		cout<<b[i]<<" ";
		}
		cout<<endl;
	}
	return 0;
}

```

### over