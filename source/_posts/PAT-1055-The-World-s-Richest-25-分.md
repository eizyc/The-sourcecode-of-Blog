title: PAT 1055 The World's Richest (25 分)
tags:
  - PAT
categories:
  - 刷题
date: 2019-08-06 11:59:00
author:
---
#### 1055 The World's Richest (25 分)
[题目链接](https://pintia.cn/problem-sets/994805342720868352/problems/994805421066272768)  
这题也居然25分...  
[参考博客](https://blog.csdn.net/chenyutingdaima/article/details/82254217)
```c++
#include<bits/stdc++.h>
using namespace std;
const int maxn=2550;
vector<string>course[maxn];

int main(){
    int n,k;
    scanf("%d%d",&n,&k);
    for(int i=1;i<=n;i++){
        string name;
        int c,x;
        cin>>name>>c;
        for(int j=0;j<c;j++){
            scanf("%d",&x);
            course[x].push_back(name) ;
        }
    }
    for(int i=1;i<=k;i++){
        printf("%d %d\n",i,course[i].size() );
        sort(course[i].begin() ,course[i].end() );
        for(int j=0;j<course[i].size() ;j++){
           printf("%s\n",course[i][j].c_str());
        }
    }
    return 0;
}

```
Tips：
1. 排序题