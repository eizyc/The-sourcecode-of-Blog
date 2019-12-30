title: PAT 1094 The Largest Generation (25 分)
tags:
  - PAT
categories:
  - 刷题
date: 2019-08-03 16:24:00
author:
---
#### PAT 1096 Consecutive Factors (20 分)
[题目链接](https://pintia.cn/problem-sets/994805342720868352/problems/994805372601090048)  


```c++
#include<bits/stdc++.h>
using namespace std;
const int maxn = 110;
vector<int> node[maxn];
int hashTable[maxn] = {0};
void dfs(int index, int level) {
    hashTable[level]++;
    for(int j = 0; j < node[index].size(); j++) {
        dfs(node[index][j], level + 1);
    }
}
int main()
{
 int n, m, parent, k, child;
    scanf("%d%d", &n, &m);
    for(int i = 0; i < m; i++) {
        scanf("%d%d", &parent, &k);
        for(int j = 0; j < k; j++) {
            scanf("%d", &child);
            node[parent].push_back(child);
        }
    }
    dfs(1, 1);
    int maxLevel = -1, maxValue = 0;
    for(int i = 1; i < maxn; i++) {
        if(hashTable[i] > maxValue) {
            maxValue = hashTable[i];
            maxLevel = i;
        }
    }
    printf("%d %d\n", maxValue, maxLevel);
	return 0;
}


```
Tips：
1. 就是二叉树的遍历。可以参考 [这位老哥的代码](https://blog.csdn.net/hy971216/article/details/81808483)