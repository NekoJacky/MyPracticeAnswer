给你一个字符串 s，找到 s 中最长的回文子串。

如果字符串的反序与原始字符串相同，则该字符串称为回文字符串。

 

示例 1：

输入：s = "babad"
输出："bab"
解释："aba" 同样是符合题意的答案。
示例 2：

输入：s = "cbbd"
输出："bb"
 

提示：

1 <= s.length <= 1000
s 仅由数字和英文字母组成

来源：力扣（LeetCode）
链接：https://leetcode.cn/problems/longest-palindromic-substring
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

```C++
class Solution {
public:
    string longestPalindrome(string s) {
        int slen = s.length();
        if(slen < 2) return s;
        int dp[slen+5][slen+5];
        int len, l, r, ansr;
        int ansl = 0;
        int maxlen = 1;
        for(int i = 0; i < slen; i++)
        {
            for(int j = 0; j < slen; j++)
            {
                dp[i][j] = 0;
            }
        }
        for(int i = 0; i < slen; i++) dp[i][i] = 1;
        for(len = 2; len <= slen; len++)
        {
            for(l = 0; l < slen - len + 1; l++)
            {
                r = l + len - 1;
                if(s[l] != s[r]) dp[l][r] = 0;
                else if(r-l < 2) dp[l][r] = 1;
                else if(dp[l+1][r-1])
                {
                    dp[l][r] = 1;
                }
                if(dp[l][r])
                {
                    if(len > maxlen)
                    {
                        ansl = l;
                        ansr = r;
                        maxlen = len;
                    }
                }
            }
        }
        string ans(s, ansl, maxlen);
        return ans;
    }
};
```
