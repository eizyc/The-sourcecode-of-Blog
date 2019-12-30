title: PAT 1046 Shortest Distance (20 分)
tags:
  - PAT
categories:
  - 刷题
date: 2019-07-22 12:05:00
author:
---
#### PAT 1046 Shortest Distance (20 分)
[题目链接](https://pintia.cn/problem-sets/994805342720868352/problems/994805435700199424)  
我以为只是一个简单的水题，直到我第三个测试用例过不去QAQ

![upload successful](/images/pasted-179.png)
看来直接暴力是解不出的  
所以我求逆向距离的时候，又改成sum-正向距离，但是还是超时  
最后用前缀和

```c++
#include<bits/stdc++.h>
using namespace std;
    int n,m,Max,Min,sumA,sum=0,temp;
int main()
{
    cin>>n;
int arr[n];//前缀和
arr[0]=0;
for(int i=1;i<=n;i++){
        scanf("%d",&temp);
        sum +=temp;
        arr[i]=sum;
}
cin>>m;
for(int i=0;i<m;i++){
    sumA=0;
    scanf("%d %d",&Max,&Min);
if(Max<Min) swap(Max,Min);
    sumA=arr[Max-1]-arr[Min-1];
    cout<<min(sumA,sum-sumA)<<endl;
}
    return 0;
}

```
Tips：
1. 求最大最小的时候，别用max和min了，一点都不帅气，直接判断swap一下
2. scanf比cin快
3. 注意下标index，写出来就清楚了