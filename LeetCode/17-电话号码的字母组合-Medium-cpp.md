# 17 电话号码的字母组合

给定一个仅包含数字 `2-9` 的字符串，返回所有它能表示的字母组合。答案可以按 **任意顺序** 返回。

给出数字到字母的映射如下（与电话按键相同）。注意 `1` 不对应任何字母。
 
![Leetcode17](../Src/image/Leetcode17.png)

示例 1：

    输入：digits = "23"
    输出：["ad","ae","af","bd","be","bf","cd","ce","cf"]
    
示例 2：

    输入：digits = ""
    输出：[]

示例 3：

    输入：digits = "2"
    输出：["a","b","c"]
 

提示：

- `0 <= digits.length <= 4`
- `digits[i]` 是范围 `['2', '9']` 的一个数字。

```cpp
class Solution {
public:
    vector<string> letterCombinations(string digits) {
        const vector<vector<string>> s {
            {""}, {""}, {"a", "b", "c"}, {"d", "e", "f"},
            {"g", "h", "i"}, {"j", "k", "l"}, {"m", "n", "o"},
            {"p", "q", "r", "s"}, {"t", "u", "v"}, {"w", "x", "y", "z"}
        };
        vector<string> ans {};
        int l = digits.length();
        int n[4] {0};
        if(l == 0)
            return ans;
        for(int i = 0; i < l; i++) {
            n[i] = digits[i] - '0';
        }
        for(auto s1: s[n[0]]) {
            for(auto s2: s[n[1]]) {
                for(auto s3: s[n[2]]) {
                    for(auto s4: s[n[3]]){
                        ans.push_back(s1+s2+s3+s4);
                    }
                }
            }
        }
        return ans;
    }
};
```
