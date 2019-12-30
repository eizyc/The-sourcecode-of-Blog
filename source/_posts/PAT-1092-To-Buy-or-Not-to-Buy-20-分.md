title: PAT 1092 To Buy or Not to Buy (20 分)
tags:
  - PAT
categories:
  - 刷题
date: 2019-08-03 15:03:00
author:
---
#### PAT 1046 Shortest Distance (20 分)
[题目链接](https://pintia.cn/problem-sets/994805342720868352/problems/994805374509498368)  
sorry 我又写了一道水题

```c++
#include<bits/stdc++.h>
using namespace std;
map<char,int>map1,map2;
int main()
{
	string s1,s2;
	cin>>s1>>s2;
    int cnt = 0;
	for(int i = 0 ;i < s1.size();i++) map1[s1[i]]++;
	for(int i = 0 ;i < s2.size();i++) map2[s2[i]]++;
	map<char,int>::iterator it = map2.begin();
	while(it!=map2.end())
	{
		if(map1[it->first] < it->second)
			cnt+=it->second - map1[it->first];
		it++;
	}
	if(cnt == 0)
		printf("Yes %d\n",s1.size() - s2.size());
	else
		printf("No %d\n",cnt);
	return 0;
}

```
Tips：
1. 看柳神用数组写的，但是其实思路都差不多，还是用map方便。水题