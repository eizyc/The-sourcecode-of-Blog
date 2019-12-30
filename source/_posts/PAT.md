title: PAT—字符串
tags:
  - PAT
categories:
  - 刷题
date: 2019-03-18 22:03:00
author:
---
###### 1.c++中使用string ,长度为xx.size(),可以通过xx[i],遍历

###### 2.取一个字符串的长度xx.length()<!--more-->

###### 3.substr  

 start   必选。所需的子字符串的起始位置。字符串中第一个字符的索引为 0  

 length
　可选项。返回的子字符串中包含的字符数。  
 
 备注:
  如果 length 为 0 或负数，将返回一个空字符串。如果没有指定该参数，则子字符串将延续到字符串的结尾。

###### 4.atoi、stoi、strtoi区别

  首先atoi和strtol都是c里面的函数，他们都可以将字符串转为int，它们的参数都是const char*，因此在用string时，必须调c_str()方法将其转为char*的字符串。或者atof，strtod将字符串转为double，它们都从字符串开始寻找数字或者正负号或者小数点，然后遇到非法字符终止，不会报异常.
但是对于stoi就不是这样了，atoi是string库中的函数，他的参数是string。
[atoi、stoi、strtoi区别](https://www.cnblogs.com/wzxwhd/p/6030083.html)

###### 5."#include<bits/stdc++.h>"

###### 6.cin 不能输入包含嵌入空格的字符串
为了解决这个问题，可以使用一个叫做 getline 的 C++ 函数。此函数可读取整行，包括前导和嵌入的空格，并将其存储在字符串对象中。getline(cin, inputLine);

###### 7.string中find()
string中find()返回值是字母在母串中的位置（下标记录），如果没有找到，那么会返回一个特别的标记npos,<font color="red">可以用-1判断</font>。（返回值可以看成是一个int型的数）。还可以寻找这个字符第一次出现和最后一次出现的位置s.find_first_of(flag);s.find_last_of(flag);
[C++ string中的find()函数](https://www.cnblogs.com/wkfvawl/p/9429128.html)

###### 8.printf和sprintf和fprintf  
  1. printf，是把格式字符串输出到标准输出（一般是屏幕，可以重定向）。
  2. sprintf，是把格式字符串输出到指定字符串中，所以参数比printf多一个char*。那就是目标字符串地址。
```c++
#include <stdio.h>
#include <math.h>
int main()
{
   char str[80];
   sprintf(str, "Pi 的值 = %f", M_PI);
   puts(str);
   return(0);
}
  ```
  3. fprintf， 是把格式字符串输出到指定文件设备中，所以参数笔printf多一个文件指针FILE*。
  
###### 9.sscanf 和scanf  
  C 库函数 int sscanf(const char *str, const char *format, ...) 从字符串读取格式化输入
```c++
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
int main()
{
   int day, year;
   char weekday[20], month[20], dtm[100];
   strcpy( dtm, "Saturday March 25 1989" );
   sscanf( dtm, "%s %s %d  %d", weekday, month, &day, &year );
   printf("%s %d, %d = %s\n", month, day, year, weekday );
   return(0);
}
```

###### 10.C语言中的字符串
```c++
int main()
{
 char c[81], u[30][30];
 memset(u, ' ', sizeof(u));
 scanf("%s",c);
 int n=strlen(c)+2;
 }
```
