### 140. Word Break II

给定一个非空字符串 s 和一个包含非空单词列表的字典 wordDict，在字符串中增加空格来构建一个句子，使得句子中所有的单词都在词典中。返回所有这些可能的句子。

说明：

* 分隔时可以重复使用字典中的单词。
* 你可以假设字典中没有重复的单词。


示例 1：
```
输入:
s = "catsanddog"
wordDict = ["cat", "cats", "and", "sand", "dog"]
输出:
[
  "cats and dog",
  "cat sand dog"
]
```
示例 2：
```
输入:
s = "pineapplepenapple"
wordDict = ["apple", "pen", "applepen", "pine", "pineapple"]
输出:
[
  "pine apple pen apple",
  "pineapple pen apple",
  "pine applepen apple"
]
解释: 注意你可以重复使用字典中的单词。
```
示例 3：
```
输入:
s = "catsandog"
wordDict = ["cats", "dog", "sand", "and", "cat"]
输出:
[]
```


### 解法：记忆化回溯

1. 记忆化回溯，否则 `backtrack(s, index, wordDict)` 可能会重复调用多次相同的 index，所以新建 map 存 map[index]，避免多次重复计算。
2. `for (auto &word : wordDict)` 搜索时根据 wordDict 的 word 进行遍历，而不是 int i > lastIndex，效率更高

```cpp
class Solution {
public:
    unordered_map<int, vector<string>> map;
    vector<string> backtrack(string s, int lastindex, vector<string>& wordDict) {
        // 记忆化回溯
        if(map.count(lastindex)) return map[lastindex];
		int n = s.size();
        vector<string> result;
		if (lastindex >= n) return {""};
        for (auto &word : wordDict) {
            string sub = s.substr(lastindex, word.size());
            if (sub.compare(word)==0) {
                // 从新位置开始搜索
                vector<string> temp = backtrack(s, lastindex + word.size(), wordDict);
                // 把搜索结果全部存入 result 中
				for(auto &str : temp) {
                    if (str.empty()) {
                        result.push_back(sub);
                    } else {
                        result.push_back(sub + " " + str);
                    }
                }
            }
        }
        map[lastindex] = result;
        return result;
	}
    vector<string> wordBreak(string s, vector<string>& wordDict) {
        vector<string> result;
		result = backtrack(s, 0, wordDict);
        return result;
    }
};
```
