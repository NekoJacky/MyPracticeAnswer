给定两个大小分别为 m 和 n 的正序（从小到大）数组 nums1 和 nums2。请你找出并返回这两个正序数组的 中位数 。

算法的时间复杂度应该为 O(log (m+n)) 。

 

示例 1：

输入：nums1 = [1,3], nums2 = [2]
输出：2.00000
解释：合并数组 = [1,2,3] ，中位数 2
示例 2：

输入：nums1 = [1,2], nums2 = [3,4]
输出：2.50000
解释：合并数组 = [1,2,3,4] ，中位数 (2 + 3) / 2 = 2.5
 

 

提示：

nums1.length == m
nums2.length == n
0 <= m <= 1000
0 <= n <= 1000
1 <= m + n <= 2000
-106 <= nums1[i], nums2[i] <= 106

来源：力扣（LeetCode）
链接：https://leetcode.cn/problems/median-of-two-sorted-arrays
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

```C++
class Solution {
public:
    double findMedianSortedArrays(vector<int>& nums1, vector<int>& nums2) {
        double ans = 0;
        int tmp;
        int s, size, size1, size2;
        size1 = nums1.size();
        size2 = nums2.size();
        size = size1 + size2;
        s = size / 2;
        int flag = size % 2 ? 1 : 0;
        int i = 0, j = 0, k = 0;
        while(i < size)
        {
            if(j < size1 && k < size2)
            {
                if(nums1[j] < nums2[k])
                    tmp = nums1[j++];
                else
                    tmp = nums2[k++];
                if(i == s || (!flag && i == s-1))
                    ans += tmp;
            }
            else if(j >= size1)
            {
                tmp = nums2[k++];
                if(i == s || (!flag && i == s-1))
                    ans += tmp;
            }
            else if(k >= size2)
            {
                tmp = nums1[j++];
                if(i == s || (!flag && i == s-1))
                    ans += tmp;
            }
            if(i == s)
                break;
            i++;
        }
        if(flag)
            return ans;
        else
            return ans / 2;
    }
};
```
