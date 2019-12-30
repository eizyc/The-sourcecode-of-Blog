title: PAT 1108 Finding Average (20 分)
tags:
  - PAT
categories:
  - 刷题
date: 2019-08-03 17:04:00
author:
---
#### PAT 1096 Consecutive Factors (20 分)
[题目链接](https://pintia.cn/problem-sets/994805342720868352/problems/994805360777347072)  
题目是挺好懂的，但是把字符串转float我不想手写啊...肯定有函数可以用，还真找到了  
<font color="red">
sscanf() – 从一个字符串中读进与指定格式相符的数据  
sprintf() – 字符串格式化命令，主要功能是把格式化的数据写入某个字符串中
</font>  
[参考博客](https://blog.csdn.net/QQN19961117/article/details/82385766)
```c++
#include<bits/stdc++.h>
using namespace std;
int main()
 {
    int n, cnt = 0;
    char a[50], b[50];
    double temp, sum = 0.0;
    cin >> n;
    for(int i = 0; i < n; i++) {
        scanf("%s", a);
        sscanf(a, "%lf", &temp);
        sprintf(b, "%.2lf",temp);
        int flag = 0;
        for(int j = 0; j < strlen(a); j++) {
            if(a[j] != b[j]) {
                flag = 1;
            }
        }
        if(flag || temp < -1000 || temp > 1000) {
            printf("ERROR: %s is not a legal number\n", a);
            continue;
        } else {
            sum += temp;
            cnt++;
        }
    }
    if(cnt == 1)
        printf("The average of 1 number is %.2lf", sum);

    else if(cnt > 1)
        printf("The average of %d numbers is %.2lf", cnt, sum / cnt);

    else
        printf("The average of 0 numbers is Undefined");

    return 0;
}

```
Tips：
1. 字符串的题...如果函数用的好，可以少很多事