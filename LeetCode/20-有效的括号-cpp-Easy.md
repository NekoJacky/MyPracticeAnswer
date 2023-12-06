# 20 有效的括号

给定一个只包括 `'('`，`')'`，`'{'`，`'}'`，`'['`，`']'` 的字符串 `s` ，判断字符串是否有效。

有效字符串需满足：

<ol>
<li>左括号必须用相同类型的右括号闭合。
<li>左括号必须以正确的顺序闭合。
<li>每个右括号都有一个对应的相同类型的左括号。
</ol>

示例 1：

    输入：s = "()"
    输出：true

示例 2：

    输入：s = "()[]{}"
    输出：true

示例 3：

    输入：s = "(]"
    输出：false
 

提示：

- `1 <= s.length <= 104`
- `s` 仅由括号 `'()[]{}'` 组成

```cpp
class Solution {
public:
    bool isValid(string s) {
        int length = s.length();
        stack<char> a {};
        for(int i = 0; i < length; i++) {
            if(s[i] == '(' || s[i] == '[' || s[i] == '{') a.push(s[i]);
            else if(!a.empty()){
                char tmp = a.top();
                if(s[i] == ')' && tmp == '(') a.pop();
                else if(s[i] == ']' && tmp == '[') a.pop();
                else if(s[i] == '}' && tmp == '{') a.pop();
                else return false;
            }
            else return false;
        }
        if(a.empty()) return true;
        else return false;
    }
};
```
