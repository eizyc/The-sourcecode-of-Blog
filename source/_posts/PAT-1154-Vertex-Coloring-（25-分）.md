title: PAT 1154 Vertex Coloring （25 分）
tags:
  - PAT
categories:
  - 刷题
date: 2019-06-21 21:47:00
author:
---
[题目链接](https://pintia.cn/problem-sets/994805342720868352/problems/1071785301894295552)

### 1154 Vertex Coloring (25 分)

```c++

#include <bits/stdc++.h>
using namespace std;
struct node {int t1, t2;};
int m,n,k;
int main()
{
cin>>n>>m;
vector<node> v(m);
for(int i=0;i<m;i++){
 scanf("%d %d", &v[i].t1, &v[i].t2);
}
cin>>k;
while(k--){
        int a[10005]={0};
        set<int> se;
        bool flag = true;
    for(int i=0;i<n;i++){
        scanf("%d",&a[i]);
        se.insert(a[i]);
    }
for(int i=0;i<m;i++){
    if(a[v[i].t1]==a[v[i].t2]){
        flag=false;
        break;
    }
}
if (flag)
            printf("%d-coloring\n", se.size());
        else
            printf("No\n");
}

    return 0;
}

```
Tips:
1. 也没啥，对自己写出cin>>n,m;这种智障错误已经无话可说
2. set的应用,不存重复的值，而且只有键，或者说它的值就是键，map是有键值。所以set可以用于计算种类个数。
3. struct node {int t1, t2;};最后的分号别忘记了