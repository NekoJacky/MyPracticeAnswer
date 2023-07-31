# 11 盛最多水的容器

给定一个长度为 n 的整数数组 height 。有 n 条垂线，第 i 条线的两个端点是 (i, 0) 和 (i, height[i]) 。

找出其中的两条线，使得它们与 x 轴共同构成的容器可以容纳最多的水。

返回容器可以储存的最大水量。

说明：你不能倾斜容器。

 

示例 1：

![11](../Src/image/11.jpg "示例1")

    输入：[1,8,6,2,5,4,8,3,7]
    输出：49 
    解释：图中垂直线代表输入数组 [1,8,6,2,5,4,8,3,7]。在此情况下，容器能够容纳水（表示为蓝色部分）的最大值为 49。

示例 2：

    输入：height = [1,1]
    输出：1

提示：

n == height.length
2 <= n <= 105
0 <= height[i] <= 104

```cpp
class Solution {
public:
    int maxArea(vector<int>& height) {
        int l = 0, r = height.size()-1;
        int ans = 0;
        int cur = 0;
        while(l <= r)
        {
            cur = min(height[l], height[r])*(r-l);
            ans = max(ans, cur);
            if(height[l] <= height[r]) l++;
            else r--;
        }
        return ans;
    }
};
```

####证明正确性

解法使用了双指针作为容器边界范围。由于`ans = min(height[l], height[r]) * (r-l)`，在初始时刻，移动指向数字较大的指针，不管如何移动，得到的结果都会小于原结果。因此移动指向数字较小的指针。进而可以缩小问题范围。
