# [NOIP2001 普及组] 装箱问题

## 题目描述

有一个箱子容量为 $V$，同时有 $n$ 个物品，每个物品有一个体积。


现在从 $n$ 个物品中，任取若干个装入箱内（也可以不取），使箱子的剩余空间最小。输出这个最小值。

## 输入格式

第一行共一个整数 $V$，表示箱子容量。

第二行共一个整数 $n$，表示物品总数。

接下来 $n$ 行，每行有一个正整数，表示第 $i$ 个物品的体积。

## 输出格式

- 共一行一个整数，表示箱子最小剩余空间。

## 样例 #1

### 样例输入 #1

```
24
6
8
3
12
7
9
7
```

### 样例输出 #1

```
0
```

## 提示

对于 $100\%$ 数据，满足 $0<n \le 30$，$1 \le V \le 20000$。

**【题目来源】**

NOIP 2001 普及组第四题

二维dp
```cpp
// P1049
#include <iostream>

using namespace std;

const int maxn = 35;
const int maxv = 20005;
int chest[maxn][maxv] {};

int main()
{
    int v, n;
    int item[maxn] {};
    cin >> v >> n;
    for(int i = 1; i <= n; i++)
        cin >> item[i];
    for(int i = 1; i <= n; i++)
    {
        for(int j = 1; j <= v; j++)
        {
            chest[i][j] = chest[i-1][j];
            if(j-item[i] >= 0 && chest[i-1][j-item[i]]+item[i] <= v &&
               chest[i-1][j-item[i]]+item[i] > chest[i][j])
            {
                chest[i][j] = chest[i-1][j-item[i]]+item[i];
            }
        }
    }
    cout << v - chest[n][v];
    return 0;
}
```

一维dp
```cpp
// P1049
#include <iostream>

using namespace std;

int main()
{
    
    const int maxn = 35;
    const int maxv = 20005;
    int v, n;
    int item[maxn] {};
    int chest[maxv] {};
    cin >> v >> n;
    for(int i = 1; i <= n; i++)
        cin >> item[i];
    for(int i = 1; i <= n; i++)
    {
        for(int j = v; j >= 1; j--)
        {
            chest[j] = chest[j];
            if(j-item[i] >= 0 && chest[j-item[i]]+item[i] <= v &&
               chest[j-item[i]]+item[i] > chest[j])
            {
                chest[j] = chest[j-item[i]]+item[i];
            }
        }
    }
    cout << v - chest[v];
    return 0;
}
```
