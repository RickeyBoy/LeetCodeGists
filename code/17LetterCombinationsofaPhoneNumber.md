### 17. Letter Combinations of a Phone Number

给定一个仅包含数字 2-9 的字符串，返回所有它能表示的字母组合。

给出数字到字母的映射如下（与电话按键相同）。注意 1 不对应任何字母。



示例:
```
输入："23"
输出：["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"].
```
说明:
```
尽管上面的答案是按字典序排列的，但是你可以任意选择答案输出的顺序。
```

### 解法：模拟，全排列即可

```cpp
class Solution {
public:
    vector<string> results;
    vector<string> letterCombinations(string digits) {
        if(digits.size()<1) return {};
        results = {};
        for(int i=0;i<digits.size();i++) {
            int digit = (int)(digits[i]-'0');
            string newStr = getStrFromInt(digit);
            addString(newStr);
        }
        return results;
    }
    string getStrFromInt(int i) {
        switch (i) {
            case 2: return "abc";
            case 3: return "def";
            case 4: return "ghi";
            case 5: return "jkl";
            case 6: return "mno";
            case 7: return "pqrs";
            case 8: return "tuv";
            case 9: return "wxyz";
            default: return "";
        }
    }
    void addString(string s) {
        vector<string> temp = results;
        results.clear();
        for(int i=0;i<s.size();i++) {
            if(temp.size()==0) {
                // 第一个数字
                results.push_back(string(1,s[i]));
            } else {
                // 后续数字
                for(auto str : temp) {
                    results.push_back(str+s[i]);
                }
            }
        }
    }
};
```