### [301. 删除无效的括号](https://leetcode-cn.com/problems/remove-invalid-parentheses/)

给你一个由若干括号和字母组成的字符串 s ，删除最小数量的无效括号，使得输入的字符串有效。

返回所有可能的结果。答案可以按 任意顺序 返回。

 

示例 1：
```
输入：s = "()())()"
输出：["(())()","()()()"]
```
示例 2：
```
输入：s = "(a)())()"
输出：["(a())()","(a)()()"]
```
示例 3：
```
输入：s = ")("
输出：[""]
```

### 解法：DFS

- 可以剪枝

```cpp
class Solution {
private:
    unordered_set<string> result;
    int totalLeft = 0; // 所有左括号数目
public:
    // curIdx = 当前该遍历的 idx， resStr = 当前已组成的字符串，leftCount = 已有左括号个数
    void dfs(int curIdx, string resStr, string s,int leftCount, int leftToDelete, int rightToDelete) {
        if (curIdx >= s.size()) {
            // 遍历到头，加入结果
            if (leftToDelete == 0 && rightToDelete == 0 && !result.count(resStr)) {
                result.insert(resStr);
            }
            return;
        }
        if (s[curIdx] == '(') {
            if (leftToDelete > 0) {
                // 左括号，方案 1：可删除，则尝试删除
                dfs(curIdx+1, resStr, s, leftCount, leftToDelete-1, rightToDelete);
            }
            if (leftToDelete + leftCount < totalLeft) { // 不是剩下所有都得删除
                // 左括号，方案 2：不删除
                resStr.push_back('(');
                dfs(curIdx+1, resStr, s, leftCount+1, leftToDelete, rightToDelete);
            }
        } else if (s[curIdx] == ')') {
            if (rightToDelete > 0) {
                // 右括号，方案 1：可删除，或者左括号个数为 0 必须删除，则尝试删除
                dfs(curIdx+1, resStr, s, leftCount, leftToDelete, rightToDelete-1);
            }
            if (leftCount > 0) {
                // 右括号，方案 2：不删除，抵消一个左括号
                resStr.push_back(')');
                dfs(curIdx+1, resStr, s, leftCount-1, leftToDelete, rightToDelete);
            }
        } else {
            // 字符，不删除
            resStr.push_back(s[curIdx]);
            dfs(curIdx+1, resStr, s, leftCount, leftToDelete, rightToDelete);
        }
    }
    vector<string> removeInvalidParentheses(string s) {
        result = {};
        // 1. 统计需要删除的左右括号数目
        int leftToDelete = 0;
        int rightToDelete = 0;
        for (int i=0;i<s.size();i++) {
            if (s[i]=='(') {
                leftToDelete++;
                totalLeft++;
            } 
            else if (s[i]==')') {
                if (leftToDelete>0) leftToDelete--; // 匹配上了
                else rightToDelete++; // 右括号需要删除
            }
        }
        printf("leftToDelete = %d, rightToDelete = %d \n", leftToDelete, rightToDelete);
        // 开始递归 DFS
        dfs(0,"",s,0,leftToDelete,rightToDelete);
        // 转换结果到指定个数
        vector<string> vector = {};
        for (const auto& elem: result) {
            vector.push_back(elem);
        }
        return vector;
    }
};
```
