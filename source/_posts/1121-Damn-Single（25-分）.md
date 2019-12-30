title: ' 1121 Damn Single（25 分）'
date: 2019-07-01 22:22:27
tags:
author:
---
[题目链接](https://pintia.cn/problem-sets/994805342720868352/problems/994805352359378944)

### 1121 Damn Single (25 分)

```c++
#include "map"
#include "iostream"
#include "set"
#include "cstdio"
using namespace std;
int n,m;
int main(){
	scanf("%d",&n);
	map<int,int> couples;
	for (int i=0;i<n;i++)
	{
		int a,b;
		scanf("%d %d",&a,&b);
		couples[a]=b;
		couples[b]=a;
	}
	scanf("%d",&m);
	set<int> attend,single;
	for (int i=0;i<m;i++)
	{
		int a;
		scanf("%d",&a);
		attend.insert(a);
	}
	for (auto it=attend.begin();it!=attend.end();it++)
	{
		int couple=couples[(*it)];
		auto res=attend.find(couple);
		if (res==attend.end())single.insert((*it));
	}
	printf("%d\n",single.size());
	for (auto it=single.begin();it!=single.end();it++)
	{
		if (it!=single.begin())printf(" ");
		printf("%05d",*it);
	}
	return 0;
}

```
Tips
1. 这题很简单，看懂题我就知道怎么写了。所以直接看了别人的代码
2. 看了别人的代码学会了[auto](https://blog.csdn.net/lwgkzl/article/details/82110068)
3. 代码来自[来源](https://blog.csdn.net/ysq96/article/details/81513883)