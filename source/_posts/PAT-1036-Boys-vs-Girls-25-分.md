title: PAT 1036 Boys vs Girls (25 分)
tags:
  - PAT
categories:
  - 刷题
date: 2019-07-21 18:05:00
author:
---
#### PAT 1036 Boys vs Girls (25 分)
[题目链接](https://pintia.cn/problem-sets/994805342720868352/problems/994805453203030016)  
水题
```c++
#include<bits/stdc++.h>
using namespace std;
struct student
{
    string name;
    char sex;
    string id;
    int grade;
};
bool cmp(student a,student b)
{
    return a.grade>b.grade;
}
    vector<student> boy;
    vector<student> girl;
int main()
{
  int n;
    student temp;
    cin>>n;
        for(int i=0;i<n;i++)
    {
        cin>>temp.name>>temp.sex>>temp.id>>temp.grade;
        if(temp.sex == 'F')
            girl.push_back(temp);
        else
            boy.push_back(temp);
    }
    sort(boy.begin(),boy.end(),cmp);
    sort(girl.begin(),girl.end(),cmp);
    if(girl.size()==0)
        cout<<"Absent"<<endl;
    else
        cout<<girl[0].name<<' '<<girl[0].id<<endl;
    if(boy.size()==0)
        cout<<"Absent"<<endl;
    else
        cout<<boy[boy.size()-1].name<<' '<<boy[boy.size()-1].id<<endl;
    if(girl.size() == 0 || boy.size() == 0)
        cout<<"NA"<<endl;
    else
        cout<<abs(boy[boy.size() -1].grade - girl[0].grade)<<endl;
    return 0;
}

```