### 409. 最长回文串

给定一个包含大写字母和小写字母的字符串，找到通过这些字母构造成的最长的回文串。

在构造过程中，请注意区分大小写。比如 "Aa" 不能当做一个回文字符串。

注意:
假设字符串的长度不会超过 1010。

示例 1:
```
输入:
"abccccdd"

输出:
7

解释:
我们可以构造的最长的回文串是"dccaccd", 它的长度是 7。
```

### 解法：

```cpp
class Solution {
public:
    int longestPalindrome(string s) {
        vector<int> vec = vector(52,0);
        int res = 0;
        int singles = 0; // 未成对的元素个数
        for (auto c : s) {
            int idx = getIdx(c);
            if (vec[idx]==0) {
                vec[idx]++;
                singles++;
            } else {
                // 凑成一对
                vec[idx]=0;
                res+=2;
                singles--;
            }
        }
        return singles > 0 ? res + 1 : res;
    }
    int getIdx(char c) {
        if (c>='a') return c-'a'+26;
        else return c-'A';
    }
};
```
