title: PAT 1081 Rational Sum (20 分)
tags:
  - PAT
categories:
  - 刷题
date: 2019-08-06 10:51:00
author:
---
#### PAT 1081 Rational Sum (20 分)
[题目链接](https://pintia.cn/problem-sets/994805342720868352/problems/994805386161274880)  

  
[参考博客](https://www.jianshu.com/p/acb9889e95ad)
```c++
#include<bits/stdc++.h>
using namespace std;
int gcd(int a,int b) {
    return b==0?a:gcd(b,a%b);
}
int main(){
    int n;
    cin>>n;
    int a,b;
    scanf("%d/%d",&a,&b);
    int t=gcd(a,b);
    a=a/t,b=b/t;
    for(int i=1;i<n;i++){
        int c,d;
        scanf("%d/%d",&c,&d);
        a=a*d+b*c;
        b=b*d;
        int t=gcd(a,b);
        a=a/t,b=b/t;
    }
    if(a%b==0) printf("%d",a/b);
    else{
        if(abs(a)>abs(b)){
            if(a>0) printf("%d %d/%d",a/b,a-a/b*b,b);
            else{
                a=-a;
                printf("-%d %d/%d",a/b,a-a/b*b,b);
            }
        }else printf("%d/%d",a,b);
    }
    return 0;
}
```
Tips：
1. 写好gcd函数，水题