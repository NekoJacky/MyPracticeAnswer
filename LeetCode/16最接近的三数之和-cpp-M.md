# 16 最接近的三数之和

给你一个长度为 `n` 的整数数组 `nums` 和 一个目标值 `target`。请你从 `nums` 中选出三个整数，使它们的和与 `target` 最接近。

返回这三个数的和。

假定每组输入只存在恰好一个解。

 

示例 1：

    输入：nums = [-1,2,1,-4], target = 1
    输出：2

解释：与 target 最接近的和是 2 (-1 + 2 + 1 = 2) 。
示例 2：

    输入：nums = [0,0,0], target = 1
    输出：0
 

提示：

- `3 <= nums.length <= 1000`
- `-1000 <= nums[i] <= 1000`
- `-104 <= target <= 104`

```cpp
class Solution {
public:
    int threeSumClosest(vector<int>& nums, int target) {
        sort(nums.begin(), nums.end());
        int size = nums.size();
        int ans = nums[0]+nums[1]+nums[2];
        int d = target-ans > 0 ? target-ans : ans-target;
        for(int pfirst = 0; pfirst < size - 2; pfirst++) {
            int tmp = target - nums[pfirst];
            int psecond = pfirst + 1;
            int pthird = size - 1;
            while(psecond < pthird) {
                int dif = target-nums[pfirst]-nums[psecond]-nums[pthird];
                dif = dif > 0 ? dif : -dif;
                if(dif < d) {
                    d = dif;
                    ans = nums[pfirst]+nums[psecond]+nums[pthird];
                }
                if(nums[psecond] + nums[pthird] < tmp)
                    psecond++;
                else
                    pthird--;
            }
        }
        return ans;
    }
};
```
