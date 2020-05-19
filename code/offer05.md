### 面试题05. 替换空格

请实现一个函数，把字符串 s 中的每个空格替换成"%20"。

 

示例 1：
```
输入：s = "We are happy."
输出："We%20are%20happy."
 ```

限制：
```
0 <= s 的长度 <= 10000
```

### 解法 正则表达式
``` cpp
class Solution {
public:
    string replaceSpace(string s) {
        regex pattern(" ");	
        s = regex_replace(s, pattern, "%20");
        return s;
    }
};
```