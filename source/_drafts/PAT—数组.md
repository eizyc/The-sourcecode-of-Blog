title: PAT—数组
date: 2019-07-22 12:15:40
tags:
author:
---
#### PAT—数组
1. 求数组长度没有length，方法如下，begin()返回指向数组首元素的指针，end()返回指向尾元素的下一位置的指针。
```c++
int a[] = { 1,2,3 };
cout << sizeof(a)/sizeof(a[0])<<endl;
cout << end(a) - begin(a)<<endl;
```