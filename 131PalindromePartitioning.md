### 131. Palindrome Partitioning

给定一个字符串 s，将 s 分割成一些子串，使每个子串都是回文串。

返回 s 所有可能的分割方案。

示例:
```
输入: "aab"
输出:
[
  ["aa","b"],
  ["a","a","b"]
]
```

### 解法：回溯法

```cpp
class Solution {
public:
    bool isPalin(string s) {
        if(s.size()<=1) return true;
        for(int i=0;i<s.size()/2;i++) {
            if(s.at(i)!=s.at(s.size()-1-i)) return false;
        }
        return true;
    }
    void backtrack(string s, vector<string> &cur, int lastindex, vector<vector<string>> &result) {
		int n = s.size();
		if (lastindex >= n) {
			result.push_back(cur);
			return;
		}
		for (int i = lastindex; i < n; i++) {
			string toAdd = s.substr(lastindex, i - lastindex + 1);
			if (isPalin(toAdd)) {
				// 发现回文，加入该回文串到 cur
				cur.push_back(toAdd);
				// 并从 i+1 开始搜索
				backtrack(s, cur, i + 1, result);
				// 回溯
				cur.pop_back();
			}
		}
	}
	// 主函数
	vector<vector<string>> partition(string s) {
		vector<string>cur;
    vector<vector<string>> result;
		backtrack(s, cur, 0, result);
		return result;
	}
};
```
