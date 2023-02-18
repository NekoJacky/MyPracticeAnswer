# 马的遍历

## 题目描述

有一个 $n \times m$ 的棋盘，在某个点 $(x, y)$ 上有一个马，要求你计算出马到达棋盘上任意一个点最少要走几步。

## 输入格式

输入只有一行四个整数，分别为 $n, m, x, y$。

## 输出格式

一个 $n \times m$ 的矩阵，代表马到达某个点最少要走几步（不能到达则输出 $-1$）。

## 样例 #1

### 样例输入 #1

```
3 3 1 1
```

### 样例输出 #1

```
0    3    2    
3    -1   1    
2    1    4
```

## 提示

### 数据规模与约定

对于全部的测试点，保证 $1 \leq x \leq n \leq 400$，$1 \leq y \leq m \leq 400$。

```C++
// P1443
#include <iostream>
#include <queue>

#define MAX 405

using namespace std;

int step_num = 0;
int step_n;
int m, n, x, y;
int map[MAX][MAX];
queue<int> qx;
queue<int> qy;
queue<int> qstep_num;

void bfs()
{
    while(!qx.empty())
    {
        x = qx.front();
        qx.pop();
        y = qy.front();
        qy.pop();
        step_n = qstep_num.front();
        qstep_num.pop();
        map[x][y] = step_n;
        if(x+2 <= n && y+1 <= m)
        {
            if(map[x+2][y+1] == -1)
            {
                qx.push(x+2);
                qy.push(y+1);
                qstep_num.push(step_n+1);
                map[x+2][y+1] = 0;
            }
        }
        if(x+2 <= n && y-1 > 0)
        {
            if(map[x+2][y-1] == -1)
            {
                qx.push(x+2);
                qy.push(y-1);
                qstep_num.push(step_n+1);
                map[x+2][y-1] = 0;
            }
        }
        if(x+1 <= n && y-2 > 0)
        {
            if(map[x+1][y-2] == -1)
            {
                qx.push(x+1);
                qy.push(y-2);
                qstep_num.push(step_n+1);
                map[x+1][y-2] = 0;
            }
        }
        if(x-1 > 0 && y-2 > 0)
        {
            if(map[x-1][y-2] == -1)
            {
                qx.push(x-1);
                qy.push(y-2);
                qstep_num.push(step_n+1);
                map[x-1][y-2] = 0;
            }
        }
        if(x-2 > 0 && y-1 > 0)
        {
            if(map[x-2][y-1] == -1)
            {
                qx.push(x-2);
                qy.push(y-1);
                qstep_num.push(step_n+1);
                map[x-2][y-1] = 0;
            }
        }
        if(x-2 > 0 && y+1 <= m)
        {
            if(map[x-2][y+1] == -1)
            {
                qx.push(x-2);
                qy.push(y+1);
                qstep_num.push(step_n+1);
                map[x-2][y+1] = 0;
            }
        }
        if(x-1 > 0 && y+2 <= m)
        {
            if(map[x-1][y+2] == -1)
            {
                qx.push(x-1);
                qy.push(y+2);
                qstep_num.push(step_n+1);
                map[x-1][y+2] = 0;
            }
        }
        if(x+1 <= n && y+2 <= m)
        {
            if(map[x+1][y+2] == -1)
            {
                qx.push(x+1);
                qy.push(y+2);
                qstep_num.push(step_n+1);
                map[x+1][y+2] = 0;
            }
        }
    }
}

int main()
{
    int i, j;
    cin >> n >> m >> x >> y;
    for(i = 1; i <= n; i++)
    {
        for(j = 1; j <=m; j++)
        {
            map[i][j] = -1;
        }
    }
    qx.push(x);
    qy.push(y);
    qstep_num.push(step_num);
    bfs();
    for(i = 1; i <= n; i++)
    {
        for(j = 1; j <= m; j++)
        {
            cout << map[i][j] << ' ';
        }
        cout << endl;
    }
    return 0;
}
```