title: PAT 1065 A+B and C (64bit) (20 分)
tags:
  - PAT
categories:
  - 刷题
date: 2019-08-28 14:54:00
author:
---
#### 1065 A+B and C (64bit) (20 分)
[题目链接](https://pintia.cn/problem-sets/994805342720868352/problems/994805406352654336)  
对不起智商秀逗了，20分的题写了一个小时，为什么呢？因为刚刚好整理了大整数运算的笔记，就觉得一定是用算法笔记里的大整数运算。结果，有一个测试样例过不去...  
![upload successful](/images/pasted-210.png)
而且看过算法笔记大整数运算的都知道那个代码其实也不短...后面才看到可以用long long。不想说了。  
[参考博客](https://blog.csdn.net/kakitgogogo/article/details/51954542)
```c++
#include<bits/stdc++.h>
using namespace std;
int main()
{
int n;
	scanf("%d",&n);
	for(int i=1;i<=n;i++)
	{
		long long a,b,c;
		scanf("%lld %lld %lld",&a,&b,&c);
		bool istrue;
		long long res=a+b;
		if(a>0&&b>0&&res<=0) istrue=true;
		else if(a<0&&b<0&&res>=0) istrue=false;
		else if(res>c) istrue=true;
		else istrue=false;
		printf("Case #%d: %s\n",i,istrue?"true":"false");
}
return 0;
}

```
Tips:
1. c里的异或没有像&&和||的符号，所以建议不用bool，用int，然后用按位异或的^符号，但是用bool的话！可以直接取反，比较方便。
2. 可以参考这篇博客 [C语言的整型溢出问题 int、long、long long取值范围 最大最小值]()