### 1071. 字符串的最大公因子

对于字符串 S 和 T，只有在 S = T + ... + T（T 与自身连接 1 次或多次）时，我们才认定 “T 能除尽 S”。

返回最长字符串 X，要求满足 X 能除尽 str1 且 X 能除尽 str2。

 

示例 1：
```
输入：str1 = "ABCABC", str2 = "ABC"
输出："ABC"
```
示例 2：
```
输入：str1 = "ABABAB", str2 = "ABAB"
输出："AB"
```
示例 3：
```
输入：str1 = "LEET", str2 = "CODE"
输出：""
``` 

提示：
```
1 <= str1.length <= 1000
1 <= str2.length <= 1000
str1[i] 和 str2[i] 为大写英文字母
```

### 解法：使用 __gcd 函数

```cpp
class Solution {
public:
    string gcdOfStrings(string str1, string str2) {
        int gcd = __gcd(str1.size(),str2.size()); // 最大公约数
        string pattern = str2.substr(0, gcd);
        if(match(str1,pattern) && match(str2,pattern)) {
            return pattern;
        } else {
            return "";
        }
    }
    // str 是否整除 pattern
    bool match(string str, string pattern) {
        int multi = str.size()/pattern.size();
        string s = "";
        for(int i=0;i<multi;i++) {
            s = s + pattern;
        }
        return str == s;
    }
};
```
