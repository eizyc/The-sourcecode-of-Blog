title: PAT 1138 Postorder Traversal (25 分)
tags:
  - PAT
categories:
  - 刷题
date: 2019-07-21 17:51:00
author:
---
[题目链接](https://pintia.cn/problem-sets/994805342720868352/problems/994805345078067200)

### 1138 Postorder Traversal (25 分)

```c++
#include<bits/stdc++.h>
using namespace std;
vector<int> pre, in;
bool flag = false;

void postOrder(int prel, int inl, int inr) {
    if (inl > inr || flag == true) return;
    int i = inl;
    while (in[i] != pre[prel]) i++;
    postOrder(prel+1, inl, i-1);
    postOrder(prel+i-inl+1, i+1, inr);
    if (flag == false) {
        printf("%d", in[i]);
        flag = true;
    }
}
int main()
{
 int n;
    scanf("%d", &n);
    pre.resize(n);
    in.resize(n);
    for (int i = 0; i < n; i++) scanf("%d", &pre[i]);
    for (int i = 0; i < n; i++) scanf("%d", &in[i]);
    postOrder(0, 0, n-1);
    return 0;

}

```

Tips:
1. 我居然有生之年...连曾经写过的前中序树如何转后序树都忘了...反正就是递归递归递归
2. 鄙人太菜最后还是看了[柳神的代码](https://blog.csdn.net/liuchuo/article/details/79064958)
3. 这篇文章写的挺好的 [根据二叉树的中序遍历和前序遍历，还原二叉树](https://www.cnblogs.com/schips/p/10646789.html)
4. 我上面粘的是柳神的代码，就说一个细节，inl > inr，不是>=。