给你一个 32 位的有符号整数 x ，返回将 x 中的数字部分反转后的结果。

如果反转后整数超过 32 位的有符号整数的范围 [−231,  231 − 1] ，就返回 0。

假设环境不允许存储 64 位整数（有符号或无符号）。
 

示例 1：

    输入：x = 123
    输出：321

示例 2：

    输入：x = -123
    输出：-321

示例 3：

    输入：x = 120
    输出：21

示例 4：

    输入：x = 0
    输出：0
 

提示：

    -231 <= x <= 231 - 1

来源：力扣（LeetCode）
链接：https://leetcode.cn/problems/reverse-integer
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

## 这个题有一个问题，是关于包含负数的取模运算的结果的，不同的语言结果可能不一样，需要学习。

```C++
class Solution {
public:
    int reverse(int x) {
        if(!x)
            return 0;
        int tmp;
        int ans = 0;
        while(x)
        {
            if(ans > INT_MAX / 10 || ans < INT_MIN / 10)
                return 0;
            tmp = x % 10;
            x /= 10;
            ans = ans * 10 + tmp;
        }
        return ans;
    }
};
```