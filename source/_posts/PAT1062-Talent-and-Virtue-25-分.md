title: PAT 1062 Talent and Virtue (25 分)
tags:
  - PAT
categories:
  - 刷题
date: 2019-08-06 12:11:00
author:
---
#### 1062 Talent and Virtue (25 分)
[题目链接](https://pintia.cn/problem-sets/994805342720868352/problems/994805410555346944)  
这题也居然25分...  
[参考博客](https://blog.csdn.net/mayuejike/article/details/86552440)
```c++
#include<bits/stdc++.h>
using namespace std;
const int MAX = 100010;
struct student
{
    char id[10];
    int de,cai,sum;
    int flag;
} stu[MAX];

bool cmp(student a,student b)
{
    if(a.flag!=b.flag)
        return a.flag<b.flag;
    else if(a.sum!=b.sum)
        return a.sum>b.sum;
    else if(a.de!=b.de)
        return a.de>b.de;
    else
        return strcmp(a.id,b.id)<0;
}


int main()
{
    int N,L,H;
    scanf("%d%d%d",&N,&L,&H);
    int m=N;
    for(int i=0; i<N; i++)
    {
        scanf("%s%d%d",stu[i].id,&stu[i].de,&stu[i].cai);
        stu[i].sum=stu[i].de+stu[i].cai;
        if(stu[i].de<L||stu[i].cai<L)
        {
            stu[i].flag=5;
            m--;
        }
        else if(stu[i].de>=H&&stu[i].cai>=H)
            stu[i].flag=1;
        else if(stu[i].de>=H&&stu[i].cai<H)
            stu[i].flag=2;
        else if(stu[i].de<H&&stu[i].cai<H&&stu[i].de>=stu[i].cai)
            stu[i].flag=3;
        else
            stu[i].flag=4;
    }
    sort(stu,stu+N,cmp);
    printf("%d\n",m);
    for(int i=0; i<m; i++)
    {
        printf("%s %d %d\n",stu[i].id,stu[i].de,stu[i].cai);
    }
    return 0;
}


```
Tips：
1. 排序题