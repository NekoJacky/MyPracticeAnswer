# 1289 下降路径最小和 II

给你一个 `n x n` 整数矩阵 `grid` ，请你返回 非零偏移下降路径 数字和的最小值。

非零偏移下降路径 定义为：从 `grid` 数组中的每一行选择一个数字，且按顺序选出来的数字中，相邻数字不在原数组的同一列。

示例 1：

![1289](../Src/image/1289.jpg)

    输入：grid = [[1,2,3],[4,5,6],[7,8,9]]
    输出：13
    解释：
    所有非零偏移下降路径包括：
    [1,5,9], [1,5,7], [1,6,7], [1,6,8],
    [2,4,8], [2,4,9], [2,6,7], [2,6,8],
    [3,4,8], [3,4,9], [3,5,7], [3,5,9]
    下降路径中数字和最小的是 [1,5,7] ，所以答案是 13 。

示例 2：

    输入：grid = [[7]]
    输出：7
 

提示：

- `n == grid.length == grid[i].length`
- `1 <= n <= 200`
- `-99 <= grid[i][j] <= 99`

```cpp
class Solution {
public:
    int minFallingPathSum(vector<vector<int>>& grid) {
        struct min {
            int value;
            int y;
        };
        int n = grid.size();
        int a[205][205] {};
        int i, j, m;
        min min1, min2;
        for(i = 0; i < n; i++)
            a[0][i] = grid[0][i];
        for(i = 0; i < n-1; i++) {
            if(a[i][0] < a[i][1]) {
                min1.value = a[i][0];
                min1.y = 0;
                min2.value = a[i][1];
                min2.y = 1;
            }
            else {
                min1.value = a[i][1];
                min1.y = 1;
                min2.value = a[i][0];
                min2.y = 0;
            }
            for(j = 2; j < n; j++) {
                if(a[i][j] <= min1.value) {
                    min2 = min1;
                    min1.value = a[i][j];
                    min1.y = j;
                }
                else if(a[i][j] <= min2.value) {
                    min2.value = a[i][j];
                    min2.y = j;
                }
            }
            for(j = 0; j < n; j++) {
                if(j == min1.y) {
                    a[i+1][j] = grid[i+1][j] + min2.value;
                }
                else {
                    a[i+1][j] = grid[i+1][j] + min1.value;
                }
            }
        }
        m = a[n-1][0];
        for(i = 1; i < n; i++) {
            if(a[n-1][i] < m)
                m = a[n-1][i];
        }
        return m;
    }
};
```
