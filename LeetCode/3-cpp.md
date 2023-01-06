给定一个字符串 s ，请你找出其中不含有重复字符的 最长子串 的长度。

示例 1:

    输入: s = "abcabcbb"
    输出: 3 
    解释: 因为无重复字符的最长子串是 "abc"，所以其长度为 3。

示例 2:

    输入: s = "bbbbb"
    输出: 1
    解释: 因为无重复字符的最长子串是 "b"，所以其长度为 1。

示例 3:

    输入: s = "pwwkew"
    输出: 3
    解释: 因为无重复字符的最长子串是 "wke"，所以其长度为 3。

请注意，你的答案必须是 子串 的长度，"pwke" 是一个子序列，不是子串。


提示：

0 <= s.length <= 5 * 104
s 由英文字母、数字、符号和空格组成

来源：力扣（LeetCode）
链接：https://leetcode.cn/problems/longest-substring-without-repeating-characters
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

# 麻了，一个这么简单的二分写了半天

```C++
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        int ans = 1;
        int flag = 0;
        int l, r, m, len;
        int i, j;
        len = s.length();
        if(!len)
            return 0;
        l = 1; r = len;
        while(l <= r)
        {
            m = (l+r)/2;
            for(i = 0; i <= len-m; i++)
            {
                int cnum[128];
                for(j = 0; j < 128; j++)
                    cnum[j] = 0;
                for(j = 0; j <= m; j++)
                {
                    if(cnum[s[i+j]] == 0)
                    {
                        cnum[s[i+j]]++;
                        if(j == m-1)
                            flag = 1;
                    }
                    else
                    {
                        break;
                    }
                }
                if(flag)
                    break;
            }
            if(flag)
            {
                ans = m;
                l = m + 1;
                flag = 0;
            }
            else
            {
                r = m - 1;
            }
        }
        return ans;
    }
};
```