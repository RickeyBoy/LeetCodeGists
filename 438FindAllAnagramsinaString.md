### 438. 找到字符串中所有字母异位词
给定一个字符串 s 和一个非空字符串 p，找到 s 中所有是 p 的字母异位词的子串，返回这些子串的起始索引。

字符串只包含小写英文字母，并且字符串 s 和 p 的长度都不超过 20100。

说明：
```
字母异位词指字母相同，但排列不同的字符串。
不考虑答案输出的顺序。
```
示例 1:
```
输入:
s: "cbaebabacd" p: "abc"

输出:
[0, 6]

解释:
起始索引等于 0 的子串是 "cba", 它是 "abc" 的字母异位词。
起始索引等于 6 的子串是 "bac", 它是 "abc" 的字母异位词。
```
 示例 2:
```
输入:
s: "abab" p: "ab"

输出:
[0, 1, 2]

解释:
起始索引等于 0 的子串是 "ab", 它是 "ab" 的字母异位词。
起始索引等于 1 的子串是 "ba", 它是 "ab" 的字母异位词。
起始索引等于 2 的子串是 "ab", 它是 "ab" 的字母异位词。
```

### 解法：固定宽度的滑动窗口

```cpp
class Solution {
public:
    vector<int> findAnagrams(string s, string p) {
        vector<int> result = {};
        int width = p.size(); // 滑动窗口的宽度
        if (s.size()<width) return result;
        // 初始化
        vector<int> vec = vector(26,0); // s子串需要凑够的字母数
        int sameCount = 0; // 相同字母个数
        for (int i=0;i<p.size();i++) {
            vec[p[i]-'a']++;
        }
        output(vec);
        for (int i=0;i<width;i++) {
            vec[s[i]-'a']--;
        }
        output(vec);
        for (int i=0;i<26;i++) {
            if(vec[i]==0) sameCount++;
        }
        // 开始滑动
        int l=0,r=width;
        while(r<s.size()) {
            if(sameCount==26) result.push_back(l);
            // 移动左边
            if(vec[s[l]-'a']==0) sameCount--;
            vec[s[l]-'a']++;
            if(vec[s[l]-'a']==0) sameCount++;
            l++;
            // 移动右边
            if(r<s.size()&&vec[s[r]-'a']==0) sameCount--;
            vec[s[r]-'a']--;
            if(vec[s[r]-'a']==0) sameCount++;
            r++;
        }
        if(sameCount==26) result.push_back(l);
        return result;
    }
    void output(vector<int> v) {
        for (auto i : v) {
            printf("%d ",i);
        }
        printf("\n");
    }
};
```