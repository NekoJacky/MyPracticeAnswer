# 22 括号生成

数字 n 代表生成括号的对数，请你设计一个函数，用于能够生成所有可能的并且 有效的 括号组合。

示例 1：

    输入：n = 3
    输出：["((()))","(()())","(())()","()(())","()()()"]

示例 2：

    输入：n = 1
    输出：["()"]


提示：

    1 <= n <= 8

```cpp
class Solution {
private:
    void addSymbol(vector<string>& ans, string s, int n, int left, int right) {
        if(s.length() >= 2*n) {
            ans.push_back(s);
        }
        if(left < n) {
            s.push_back('(');
            addSymbol(ans, s, n, left+1, right);
            s.pop_back();
        }
        if(left > right) {
            s.push_back(')');
            addSymbol(ans, s, n, left, right+1);
            s.pop_back();
        }
    }
public:
    vector<string> generateParenthesis(int n) {
        vector<string> ans {};
        string s {};
        addSymbol(ans, s, n, 0, 0);
        return ans;
    }
};
```
