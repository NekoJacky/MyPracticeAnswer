# 填涂颜色

## 题目描述

由数字 $0$ 组成的方阵中，有一任意形状闭合圈，闭合圈由数字 $1$ 构成，围圈时只走上下左右 $4$ 个方向。现要求把闭合圈内的所有空间都填写成 $2$。例如：$6\times 6$ 的方阵（$n=6$），涂色前和涂色后的方阵如下：

```plain
0 0 0 0 0 0
0 0 1 1 1 1
0 1 1 0 0 1
1 1 0 0 0 1
1 0 0 0 0 1
1 1 1 1 1 1
```
```plain
0 0 0 0 0 0
0 0 1 1 1 1
0 1 1 2 2 1
1 1 2 2 2 1
1 2 2 2 2 1
1 1 1 1 1 1
```

## 输入格式

每组测试数据第一行一个整数 $n(1 \le n \le 30)$。

接下来 $n$ 行，由 $0$ 和 $1$ 组成的 $n \times n$ 的方阵。

方阵内只有一个闭合圈，圈内至少有一个 $0$。

//感谢黄小U饮品指出本题数据和数据格式不一样. 已修改(输入格式)

## 输出格式

已经填好数字 $2$ 的完整方阵。

## 样例 #1

### 样例输入 #1

```
6
0 0 0 0 0 0
0 0 1 1 1 1
0 1 1 0 0 1
1 1 0 0 0 1
1 0 0 0 0 1
1 1 1 1 1 1
```

### 样例输出 #1

```
0 0 0 0 0 0
0 0 1 1 1 1
0 1 1 2 2 1
1 1 2 2 2 1
1 2 2 2 2 1
1 1 1 1 1 1
```

## 提示

对于 $100\%$ 的数据，$1 \le n \le 30$。


```C++
#include <iostream>
#include <queue>

using namespace std;

#define MAXN 35

int n;
int map[MAXN][MAXN];
queue<int> qx;
queue<int> qy;

void bfs(int x, int y)
{
    qx.push(x);
    qy.push(y);
    while(!qx.empty())
    {
        x = qx.front();
        y = qy.front();
        map[x][y] = 2;
        qx.pop();
        qy.pop();
        if(!map[x-1][y])
        {
            qx.push(x-1);
            qy.push(y);
            map[x-1][y] = 1;
        }
        if(!map[x][y-1])
        {
            qx.push(x);
            qy.push(y-1);
            map[x][y-1] = 1;
        }
        if(!map[x+1][y])
        {
            qx.push(x+1);
            qy.push(y);
            map[x+1][y] = 1;
        }
        if(!map[x][y+1])
        {
            qx.push(x);
            qy.push(y+1);
            map[x][y+1] = 1;
        }
    }
}

int main()
{
    int i, j;
    cin >> n;
    for(i = 1; i <= n; i++)
    {
        for(j = 1; j <= n; j++)
        {
            cin >> map[i][j];
        }
    }
    for(i = 2; i < n; i++)
    {
        for(j = 2; j < n; j++)
        {
            if(!map[i][j])
            {
                if(map[i-1][j]&&map[i][j-1])
                {
                    bfs(i, j);
                    goto seg1;
                }
            }
        }
    }
    seg1: ;
    for(i = 1; i <= n; i++)
    {
        for(j = 1; j <= n; j++)
        {
            cout << map[i][j] << ' ';
        }
        cout << '\n';
    }
    return 0;
}
```