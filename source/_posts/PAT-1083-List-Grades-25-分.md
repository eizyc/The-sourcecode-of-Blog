title: PAT 1083 List Grades (25 分)
tags:
  - PAT
categories:
  - 刷题
date: 2019-08-06 10:34:00
author:
---
#### PAT 1083 List Grades (25 分)
[题目链接](https://pintia.cn/problem-sets/994805342720868352/problems/994805383929905152)  
这题居然25分...
  
[参考博客](https://blog.csdn.net/weixin_35093872/article/details/86563215)
```c++
#include<bits/stdc++.h>
using namespace std;
const int maxn = 50;
struct Student{
  char name[11];
  char id[11];
  int grade;
}stu[maxn];
bool cmp(Student a, Student b){
  return a.grade > b.grade;
}

int main(){
  int n, left, right;
  scanf("%d", &n);
  for(int i = 0; i < n; i++){
    scanf("%s %s %d", stu[i].name, stu[i].id, &stu[i].grade);
  }
  scanf("%d %d", &left, &right);
  sort(stu, stu + n, cmp);
  bool flag = false;
  for(int i = 0; i < n; i++){
    if(stu[i].grade >= left && stu[i].grade <= right){
      printf("%s %s\n", stu[i].name, stu[i].id);
      flag = true;
    }
  }
  if(flag == false)
    printf("NONE\n");
  return 0;
}


```
Tips：
1. 排序的题，写好cmp函数就行