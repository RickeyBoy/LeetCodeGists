#### [1662. 检查两个字符串数组是否相等](https://leetcode.cn/problems/check-if-two-string-arrays-are-equivalent/)

给你两个字符串数组 word1 和 word2 。如果两个数组表示的字符串相同，返回 true ；否则，返回 false 。

数组表示的字符串 是由数组中的所有元素 按顺序 连接形成的字符串。

 

示例 1：
```
输入：word1 = ["ab", "c"], word2 = ["a", "bc"]
输出：true
解释：
word1 表示的字符串为 "ab" + "c" -> "abc"
word2 表示的字符串为 "a" + "bc" -> "abc"
两个字符串相同，返回 true
```
示例 2：
```
输入：word1 = ["a", "cb"], word2 = ["ab", "c"]
输出：false
```
示例 3：
```
输入：word1  = ["abc", "d", "defg"], word2 = ["abcddefg"]
输出：true
```

提示：
```
1 <= word1.length, word2.length <= 103
1 <= word1[i].length, word2[i].length <= 103
1 <= sum(word1[i].length), sum(word2[i].length) <= 103
word1[i] 和 word2[i] 由小写字母组成
```

### 解法：

同步遍历扫描即可

```cpp
class Solution {
public:
    bool arrayStringsAreEqual(vector<string>& word1, vector<string>& word2) {
        int index1 = 0; // 遍历到 word1 的 index
        int cur1 = 0; // 遍历到 word1[index] 字符串的 index
        int index2 = 0; // 遍历到 word2 的 index
        int cur2 = 0; // 遍历到 word2[index] 字符串的 index
        while (index1<word1.size() && index2<word2.size()) {
            if (word1[index1][cur1] != word2[index2][cur2]) {
                // 字符不一样
                return false;
            }
            move(index1, cur1, word1);
            move(index2, cur2, word2);
        }
        if (index1 == word1.size() && index2 == word2.size()) {
            // 同时遍历完成
            return true;
        }
        return false;
    }

    void move(int &index, int &cur, vector<string>& word) {
        if (word[index].size() -1 == cur) {
            // 该去下一个字符串了
            index++;
            cur = 0;
        } else {
            cur++;
        }
    }
};
```
