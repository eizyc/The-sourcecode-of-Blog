title: PAT 1031 Hello World for U (20 分)
tags:
  - PAT
categories:
  - 刷题
date: 2019-08-26 11:02:00
author:
---
#### 1031 Hello World for U (20 分)
[题目链接](https://pintia.cn/problem-sets/994805342720868352/problems/994805462535356416)  .  
[参考博客](https://blog.csdn.net/liuchuo/article/details/52119867)
```c++
#include<bits/stdc++.h>
using namespace std;
int main()
{
    char c[81], u[30][30];
    memset(u, ' ', sizeof(u));
    scanf("%s",c);
    int n=strlen(c)+2;
    int n2 = n / 3;
    int n1 = n  ;
    int index = 0;
    for(int i = 0; i < n1; i++)
        u[i][0] = c[index++];
    for(int i = 1; i <= n2 - 2; i++)
        u[n1-1][i] = c[index++];
    for(int i = n1 - 1; i >= 0; i--)
        u[i][n2-1] = c[index++];
    for(int i = 0; i < n1; i++)
    {
        for(int j = 0; j < n2; j++)
            printf("%c", u[i][j]);
        printf("\n");
    }
    return 0;
}
```
Tips：
1. 不加 2 也能解，n（不加2的）n/3是两个竖着的减一,n/3+n%3横着的
2. 不过柳神的代码更清晰易懂啦