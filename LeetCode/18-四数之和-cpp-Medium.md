# 18 四数之和

给你一个由 `n` 个整数组成的数组 `nums` ，和一个目标值 `target` 。请你找出并返回满足下述全部条件且不重复的四元组 `[nums[a], nums[b], nums[c], nums[d]]` （若两个四元组元素一一对应，则认为两个四元组重复）：

- `0 <= a, b, c, d < n`
- `a`、`b`、`c` 和 `d` **互不相同**
- `nums[a] + nums[b] + nums[c] + nums[d] == target`

你可以按 **任意顺序** 返回答案 。

 

示例 1：

    输入：nums = [1,0,-1,0,-2,2], target = 0
    输出：[[-2,-1,1,2],[-2,0,0,2],[-1,0,0,1]]

示例 2：

    输入：nums = [2,2,2,2,2], target = 8
    输出：[[2,2,2,2]]
 

提示：

- `1 <= nums.length <= 200`
- `-109 <= nums[i] <= 109`
- `-109 <= target <= 109`

#### 使用枚举 双指针将时间复杂度降到 $ O(n^3) $

```cpp
class Solution {
public:
    vector<vector<int>> fourSum(vector<int>& nums, int target) {
        sort(nums.begin(), nums.end());
        vector<vector<int>> ans {};
        if(nums.size() < 4)
            return ans;
        int size = nums.size();
        for(int a = 0; a < size - 3; a++)
        {
            for(int b = a + 1; b < size - 2; b++)
            {
                int c = b + 1;
                int d = size - 1;
                while(c < d)
                {
                    if((long long)nums[a]+nums[b]+nums[c]+nums[d] == target)
                    {
                        vector<int> temp {nums[a], nums[b], nums[c], nums[d]};
                        ans.push_back(temp);
                        while(nums[++c] == nums[c-1] && c < d) ;
                        while(nums[--d] == nums[d+1] && c < d) ;
                        continue;
                    }
                    if((long long)nums[a]+nums[b]+nums[c]+nums[d] < target)
                    {
                        while(nums[++c] == nums[c-1] && c < d) ;
                        continue;
                    }
                    if((long long)nums[a]+nums[b]+nums[c]+nums[d] > target)
                    {
                        while(nums[--d] == nums[d+1] && c < d) ;
                        continue;
                    }
                }
                while(nums[b] == nums[b+1] && b < size - 2) b++;
            }
            while(nums[a] == nums[a+1] && a < size - 3) a++;
        }
        return ans;
    }
};
```
