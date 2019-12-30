title: PAT 1028 List Sorting (25 分)
tags:
  - PAT
categories:
  - 刷题
date: 2019-08-06 11:27:00
author:
---
#### PAT 1028 List Sorting (25 分)
[题目链接](https://pintia.cn/problem-sets/994805342720868352/problems/994805468327690240)  
这题居然25分...  
[参考博客](https://blog.csdn.net/hy971216/article/details/81164856)
```c++
#include<bits/stdc++.h>
using namespace std;
const int maxn = 100010;
struct Student {
    int id;
    char name[10];
    int score;
}stu[maxn];
bool cmp1(Student a, Student b) {
    return a.id < b.id;
}
bool cmp2(Student a, Student b) {
    int s = strcmp(a.name, b.name);
    if(s != 0) {
        return s < 0;
    } else {
        return a.id < b.id;
    }
}
bool cmp3(Student a, Student b) {
    if(a.score != b.score) {
        return a.score < b.score;
    } else {
        return a.id < b.id;
    }
}
int main() {
    int n, c;
    scanf("%d%d", &n, &c);
    for(int i = 0; i < n; i++) {
        scanf("%d %s %d", &stu[i].id, stu[i].name, &stu[i].score);
    }
    if(c == 1) {
        sort(stu, stu + n, cmp1);
    } else if(c == 2) {
        sort(stu, stu + n, cmp2);
    } else {
        sort(stu, stu + n, cmp3);
    }
    for(int i = 0; i < n; i++) {
        printf("%06d %s %d\n", stu[i].id, stu[i].name, stu[i].score);
    }
    return 0;
}

```
Tips：
1. 写好cmp函数，水题