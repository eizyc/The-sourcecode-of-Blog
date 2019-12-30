title: PAT 1054 The Dominant Color (20 分)
tags:
  - PAT
categories:
  - 刷题
date: 2019-08-03 15:37:00
author:
---
#### PAT  1054 The Dominant Color (20 分)
[题目链接](https://pintia.cn/problem-sets/994805342720868352/problems/994805422639136768)  
sorry 我又又写了一道水题

```c++
#include<bits/stdc++.h>
using namespace std;
map<int, int> mp;
int main()
{
int m, n;
    scanf("%d %d", &m, &n);

    int half = m * n / 2;
    for(int i = 0; i < n; i++) {
        for(int j = 0; j < m; j++) {
            int temp;
            scanf("%d", &temp);
            mp[temp]++;
            if(mp[temp] > half) {
                printf("%d", temp);
                return 0;
            }
        }
    }
	return 0;
}


```
Tips：
1. 水题