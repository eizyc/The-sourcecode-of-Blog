title: PAT 1088 Rational Arithmetic (20 分)
tags:
  - PAT
categories:
  - 刷题
date: 2019-08-06 09:53:00
author:
---
#### PAT 1088 Rational Arithmetic (20 分)
[题目链接](https://pintia.cn/problem-sets/994805342720868352/problems/994805378443755520)  

  
[参考博客](https://blog.csdn.net/u014646950/article/details/47754579)
```c++
#include<bits/stdc++.h>
using namespace std;
long int gcd(long int beichushu, long int chushu)
{
  return chushu == 0 ?  beichushu: gcd(chushu, beichushu%chushu);
}
void GaiBianXingShi(long int &a, long int &b)
{
  int G = gcd(b, a);
  a /= G;
  b /= G;
}
void shuchuyige(long int a, long int b)
{
  if (b == 0)cout << "Inf";
  else
  {
      if (b < 0){ a = -a; b = -b; }
    bool parentheses = false;
    if (a < 0)parentheses = true;
    if (parentheses)cout << "(";
    if (a%b == 0)cout << a / b;
    else
    {
      if (a / b != 0)
      {
        cout << a / b << " ";
        if (a%b < 0)a = -a%b;
      }
      cout << a%b<<"/"<<b;
    }
    if (parentheses)cout << ")";
  }
}
void JiaFa(long int*a, long int *b,long int G)
{
  b[2] = b[1] * b[0] / G;
  a[2] = a[0] * b[1] / G + a[1] * b[0] / G;
  G = gcd(b[2], a[2]);
  a[2] /= G;
  b[2] /= G;
  shuchuyige(a[0], b[0]);
  cout << " + ";
  shuchuyige(a[1], b[1]);
  cout << " = ";
  shuchuyige(a[2], b[2]);
  cout << endl;
}
void JianFa(long int*a, long int *b, long int G)
{
  b[2] = b[1] * b[0] / G;
  a[2] = a[0] * b[1] / G - a[1] * b[0] / G;
  G = gcd(b[2], a[2]);
  a[2] /= G;
  b[2] /= G;
  shuchuyige(a[0], b[0]);
  cout << " - ";
  shuchuyige(a[1], b[1]);
  cout << " = ";
  shuchuyige(a[2], b[2]);
  cout << endl;
}
void ChengFa(long int*a, long int *b, long int G)
{
  b[2] = b[1] * b[0] ;
  a[2] = a[0] * a[1] ;
  G = gcd(b[2], a[2]);
  a[2] /= G;
  b[2] /= G;
  shuchuyige(a[0], b[0]);
  cout << " * ";
  shuchuyige(a[1], b[1]);
  cout << " = ";
  shuchuyige(a[2], b[2]);
  cout << endl;
}
void ChuFa(long int*a, long int *b, long int G)
{
  b[2] = b[0] * a[1];
  a[2] = b[1] * a[0];
  G = gcd(b[2], a[2]);
  a[2] /= G;
  b[2] /= G;
  shuchuyige(a[0], b[0]);
  cout << " / ";
  shuchuyige(a[1], b[1]);
  cout << " = ";
  shuchuyige(a[2], b[2]);
  cout << endl;
}
int main()
{
  long int a[3], b[3],Gmax;
  char ctemp;
  cin >> a[0]>> ctemp >> b[0]>> a[1] >> ctemp >> b[1];
  if (0 == b[0] || 0 == b[1])cout << "Inf" << endl;
  else
  {
    GaiBianXingShi(a[0], b[0]);
    GaiBianXingShi(a[1], b[1]);
    Gmax = gcd(b[0], b[1]);
    JiaFa(a, b, Gmax);
    JianFa(a, b, Gmax);
    ChengFa(a, b, Gmax);
    ChuFa(a, b, Gmax);
  }
  return 0;
}

```
Tips：
1. 数组作为函数参数用指针传参
2. gcd求最大公约数（greatest common divisor），《算法笔记》有