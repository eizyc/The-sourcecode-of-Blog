title: PAT 1096 Consecutive Factors (20 分)
tags:
  - PAT
categories:
  - 刷题
date: 2019-08-03 16:06:00
author:
---
#### PAT 1096 Consecutive Factors (20 分)
[题目链接](https://pintia.cn/problem-sets/994805342720868352/problems/994805370650738688)  
以为是水题，结果还想了一下，最后暴力解

```c++
#include<bits/stdc++.h>
using namespace std;
int n,sqrtt,first,Maxlen;
int main()
{
cin>>n;
sqrtt = (int)sqrt(n);
for(int i = 2; i<= sqrtt; i++){
    int temp = 1,j=i;
    while(1){
         temp *= j;
        if(n%temp!=0) break;

    if(j-i+1>Maxlen){
        first = i;
        Maxlen = j - i + 1;
    }
    j++;
    }
}

   if(Maxlen == 0) {
        printf("1\n%d", n);
    } else {
        printf("%d\n", Maxlen);
        for(int i = 0; i < Maxlen; i++) {
            printf("%d", first + i);
            if(i < Maxlen - 1) {
                printf("*");
            }
        }
    }
	return 0;
}


```
Tips：
1. 其实一开始挺没思路的，然后仔细想了想，就这样了