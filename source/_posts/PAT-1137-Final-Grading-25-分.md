title: PAT 1137 Final Grading (25 分)
tags:
  - PAT
categories:
  - 刷题
date: 2019-08-03 14:35:00
author:
---
#### PAT 1137 Final Grading (25 分)
[题目链接](https://pintia.cn/problem-sets/994805342720868352/problems/994805345401028608)  


```c++
#include<bits/stdc++.h>
using namespace std;
struct node {
    string name;
    int g_onine, g_mid, g_fin, g;
};
bool cmp(node a, node b) {
    return a.g != b.g ? a.g > b.g : a.name < b.name;
}
map<string, int> idx;
vector<node> v, ans;
int main()
{
    int p,m,n,score,cnt = 1;
    string s;
     cin >> p >> m >> n;
     for(int i=0;i<p;i++){
        cin >> s >> score;
        if (score >= 200) {
            v.push_back(node{s, score, -1, -1, 0});
            idx[s] = cnt++;
        }
     }
     for(int i=0;i<m;i++){
            cin >> s >> score;
        if (idx[s] != 0) v[idx[s] - 1].g_mid = score;
     }
     for(int i=0;i<n;i++){
            cin >> s >> score;
            if (idx[s] != 0) {
            int temp = idx[s] - 1;
            v[temp].g_fin = v[temp].g = score;
            if (v[temp].g_mid > v[temp].g_fin) v[temp].g = int(v[temp].g_mid * 0.4 + v[temp].g_fin * 0.6 + 0.5);
        }
     }
    for (int i = 0; i < v.size(); i++)
        if (v[i].g >= 60) ans.push_back(v[i]);
    sort(ans.begin(), ans.end(), cmp);
    for (int i = 0; i < ans.size(); i++)
        printf("%s %d %d %d %d\n", ans[i].name.c_str(), ans[i].g_onine, ans[i].g_mid, ans[i].g_fin, ans[i].g);
    return 0;
}

```
Tips：
1. 这种也是水题啦，拿一个，一个小技巧吧，用vector排序，用map记录，map的值对应vector的下标，键为string