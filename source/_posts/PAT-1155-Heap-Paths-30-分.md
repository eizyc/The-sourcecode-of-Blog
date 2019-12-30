title: PAT 1155 Heap Paths (30 分)
tags:
  - PAT
categories:
  - 刷题
date: 2019-06-21 21:22:00
author:
---
[题目链接](https://pintia.cn/problem-
sets/994805342720868352/problems/1071785408849047552)

### 1155 Heap Paths (30 分)

```c++
#include <iostream>
#include <vector>
#include <bits/stdc++.h>
using namespace std;

vector<int> v;
int a[1009],n,Ismax=1,Ismin=1;
void dfs(int index) {
if(index*2>n&&index*2+1>n){
      if (index <= n) {
            for (int i = 0; i < v.size(); i++)
                printf("%d%s", v[i], i != v.size() - 1 ? " " : "\n");
        }
}else{

        v.push_back(a[index*2+1]);
    dfs(index*2+1);
    v.pop_back();
    v.push_back(a[index*2]);
    dfs(index*2);
    v.pop_back();
}

}
int main()
{
    cin>>n;
    for(int i=1;i<=n;i++){
        scanf("%d",&a[i]);
    }
    v.push_back(a[1]);
    dfs(1);
    for(int i=2;i<=n;i++){
        if(a[i/2]>a[i]) Ismin=0;
        if(a[i/2]<a[i]) Ismax=0;
    }
    if (Ismin == 1)
        printf("Min Heap");
    else
        printf("%s", Ismax == 1 ? "Max Heap" : "Not Heap");
    return 0;
}


```

Tips:
1.  printf("%d%s", v[i], i != v.size() - 1 ? " " : 学到了
2. dfs里的if (index <= n)不要漏，是为了判断只存在一个右孩子的情况
3. 堆运算一般从index=1开始，父亲/2,孩子*2，*2+1