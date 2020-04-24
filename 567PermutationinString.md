### 567. 字符串的排列

给定两个字符串 s1 和 s2，写一个函数来判断 s2 是否包含 s1 的排列。

换句话说，第一个字符串的排列之一是第二个字符串的子串。

示例1:

输入: s1 = "ab" s2 = "eidbaooo"
输出: True
解释: s2 包含 s1 的排列之一 ("ba").
 

示例2:

输入: s1= "ab" s2 = "eidboaoo"
输出: False
 

注意：
```
输入的字符串只包含小写字母
两个字符串的长度都在 [1, 10,000] 之间
```


### 解法：固定窗口

```cpp
class Solution {
public:
    bool checkInclusion(string s1, string s2) {
        // 边界
        if (s2.size()<s1.size()) return false;
        if (s1.size()==0) return true;
        // 定义
        vector<int> need = vector(26,0);
        int left = 0, right = s1.size();
        int sameCount = 0; 
        // 初始化
        for (char c : s1) need[c-'a']++;
        for (int i=0;i<s1.size();i++) need[s2[i]-'a']--;
        for (int i=0;i<26;i++) if (need[i]==0) sameCount++;
        // 固定窗口
        while (right < s2.size()) {
            // 判断
            if(sameCount==26) return true;
            /*** debug 输出的位置 ***/
            printf("window: [%d, %d)\n", left, right);
            /********************/
            // 右移窗口
            int rightIndex = s2[right]-'a';
            need[rightIndex]--;
            if (need[rightIndex]==-1) sameCount--;
            else if (need[rightIndex]==0) sameCount++;
            right++;
            // 左移窗口
            int leftIndex = s2[left]-'a';
            need[leftIndex]++;
            if (need[leftIndex]==0) sameCount++;
            else if (need[leftIndex]==1) sameCount--;
            left++;
        }
        // 判断
        if(sameCount==26) return true;
        return false;
    }
};
```
