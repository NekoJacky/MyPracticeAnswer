# [NOIP2004 提高组] 合唱队形

## 题目描述

$n$ 位同学站成一排，音乐老师要请其中的 $n-k$ 位同学出列，使得剩下的 $k$ 位同学排成合唱队形。

合唱队形是指这样的一种队形：设 $k$ 位同学从左到右依次编号为 $1,2,$ … $,k$，他们的身高分别为 $t_1,t_2,$ … $,t_k$，则他们的身高满足 $t_1< \cdots <t_i>t_{i+1}>$ … $>t_k(1\le i\le k)$。

你的任务是，已知所有 $n$ 位同学的身高，计算最少需要几位同学出列，可以使得剩下的同学排成合唱队形。

## 输入格式

共二行。

第一行是一个整数 $n$（$2\le n\le100$），表示同学的总数。

第二行有 $n$ 个整数，用空格分隔，第 $i$ 个整数 $t_i$（$130\le t_i\le230$）是第 $i$ 位同学的身高（厘米）。

## 输出格式

一个整数，最少需要几位同学出列。

## 样例 #1

### 样例输入 #1

```
8
186 186 150 200 160 130 197 220
```

### 样例输出 #1

```
4
```

## 提示

对于 $50\%$ 的数据，保证有 $n \le 20$。

对于全部的数据，保证有 $n \le 100$。

```cpp
#include <iostream>

#define MAXN 105

using namespace std;

int main()
{
    int h[MAXN];
    int tohigh[MAXN], tolow[MAXN];
    int n, i, j;
    int ans = 0;
    cin >> n;
    for(i = 0; i < n; i++) cin >> h[i];
    for(i = 0; i < n; i++)
    {
        tohigh[i] = 1;
        tolow[i] = 1;
    }
    for(i = 0; i < n; i++)
    {
        for(j = 0; j < i; j++)
        {
            if(h[j] < h[i] && tohigh[i] <= tohigh[j])
            {
                tohigh[i] = tohigh[j]+1;
            }
        }
    }
    for(i = n-1; i >= 0; i--)
    {
        for(j = n-1; j > i; j--)
        {
            if(h[j] < h[i] && tolow[i] <= tolow[j])
            {
                tolow[i] = tolow[j]+1;
            }
        }
    }
    for(i = 0; i < n; i++)
    {
        if(tohigh[i] + tolow[i] - 1 > ans)
            ans = tohigh[i] + tolow[i] - 1;
    }
    cout << n - ans << endl;
    return 0;
}
```
