###10. Regular Expression Matching

给你一个字符串 s 和一个字符规律 p，请你来实现一个支持 '.' 和 '*' 的正则表达式匹配。

'.' 匹配任意单个字符
'*' 匹配零个或多个前面的那一个元素
所谓匹配，是要涵盖 整个 字符串 s的，而不是部分字符串。

说明:
```
s 可能为空，且只包含从 a-z 的小写字母。
p 可能为空，且只包含从 a-z 的小写字母，以及字符 . 和 *。
```

示例 1:
```
输入:
s = "aa"
p = "a"
输出: false
解释: "a" 无法匹配 "aa" 整个字符串。
```
示例 2:
```
输入:
s = "aa"
p = "a*"
输出: true
解释: 因为 '*' 代表可以匹配零个或多个前面的那一个元素, 在这里前面的元素就是 'a'。因此，字符串 "aa" 可被视为 'a' 重复了一次。
```
示例 3:
```
输入:
s = "ab"
p = ".*"
输出: true
解释: ".*" 表示可匹配零个或多个（'*'）任意字符（'.'）。
```
示例 4:
```
输入:
s = "aab"
p = "c*a*b"
输出: true
解释: 因为 '*' 表示零个或多个，这里 'c' 为 0 个, 'a' 被重复一次。因此可以匹配字符串 "aab"。
```
示例 5:
```
输入:
s = "mississippi"
p = "mis*is*p*."
输出: false
```



### 解法1：带备忘录的递归

为什么效果很差？

执行用时 :24 ms, 在所有 cpp 提交中击败了**52.13%**的用户

内存消耗 :24.1 MB, 在所有 cpp 提交中击败了**5.18%**的用户


```cpp
class Solution {
public:
    bool isCharMatch(char a, char b) {
        if(a=='.' || b=='.') return true;
        else return a==b;
    }
    bool isStrMatch(map<pair<int, int>, bool>& memo, string s, string p, int i, int j) {
        pair<int, int> index = make_pair(i, j);
        if(j>=p.length()) return i>=s.length();
        else if(i>=s.length()) {
            memo[index] = (j+1)<p.length() && p[j+1]=='*' && isStrMatch(memo, s, p, i, j+2);
            return memo[index];
        }
        else if (memo.find(index)!=memo.end()) {
            return memo[index];
        }
        else if(j+1==p.length()) {
            memo[index] = isCharMatch(p[j],s[i]) && isStrMatch(memo, s, p, i+1, j+1);
            return memo[index];
        }
        else if(p[j+1]!='*') {
            memo[index] = isCharMatch(p[j],s[i]) && isStrMatch(memo, s, p, i+1, j+1);
            return memo[index];
        }
        else {
            memo[index] = isStrMatch(memo, s, p, i, j+2) || (isCharMatch(p[j],s[i]) && isStrMatch(memo, s, p, i+1, j));
            return memo[index];
        }
    }
    bool isMatch(string s, string p) {
        map<pair<int, int>, bool> memo;
        return isStrMatch(memo,s,p,0,0);
    }
};
```

