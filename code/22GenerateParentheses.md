### 22. Generate Parentheses

给出 n 代表生成括号的对数，请你写出一个函数，使其能够生成所有可能的并且有效的括号组合。

例如，给出 n = 3，生成结果为：
```
[
  "((()))",
  "(()())",
  "(())()",
  "()(())",
  "()()()"
]
```

### 解法：回溯法

递归调用

```cpp
class Solution {
public:
    void pushBracket(vector<string>& res, string cur, int open, int close, int n) {
        if(close==n)  res.push_back(cur);
        else if(open==n) {
            pushBracket(res, cur+')', open, close+1, n);
        }
        else if(open==close) {
            pushBracket(res, cur+'(', open+1, close, n);
        } else {
            pushBracket(res, cur+'(', open+1, close, n);
            pushBracket(res, cur+')', open, close+1, n);
        }
    }
    vector<string> generateParenthesis(int n) {
        vector<string> res;
        pushBracket(res, "", 0, 0, n);
        return res;
    }
};
```

### 复杂度计算：第 n 个卡塔兰数

时间复杂度：$O(\dfrac{4^n}{\sqrt{n}})$，在回溯过程中，每个有效序列最多需要 n 步。

空间复杂度：$O(\dfrac{4^n}{\sqrt{n}})$，如上所述，并使用 O(n) 的空间来存储序列。




