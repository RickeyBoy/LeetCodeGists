### 28. Implement strStr()

实现 strStr() 函数。

给定一个 haystack 字符串和一个 needle 字符串，在 haystack 字符串中找出 needle 字符串出现的第一个位置 (从0开始)。如果不存在，则返回  -1。

示例 1:
```
输入: haystack = "hello", needle = "ll"
输出: 2
```
示例 2:
```
输入: haystack = "aaaaa", needle = "bba"
输出: -1
```
说明:

当 needle 是空字符串时，我们应当返回什么值呢？这是一个在面试中很好的问题。

对于本题而言，当 needle 是空字符串时我们应当返回 0 。这与C语言的 strstr() 以及 Java的 indexOf() 定义相符。

### 解法

暴力搜索，注意 size() 返回的是 unsigned int。

```cpp
class Solution {
public:
    int strStr(string haystack, string needle) {
        if(needle.size()==0) return 0;
        // 注意 size() 返回的是 unsigned int，所以必须要先判断大小！！
        if(haystack.size()<needle.size()) return -1;
        int hp = 0, np = 0;
        while(hp<=haystack.size()-needle.size()) {
            bool compare = true;
            while(np<needle.size()) {
                if(haystack[hp+np]!=needle[np]) {compare=false;break;}
                np++;
            }
            if(compare) return hp;
            hp++;
            np=0;
        }
        return -1;
    }
};
```

### 优化

KMP 算法
