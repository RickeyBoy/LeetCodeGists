### 14. Longest Common Prefix

编写一个函数来查找字符串数组中的最长公共前缀。

如果不存在公共前缀，返回空字符串 ""。

示例 1:
```
输入: ["flower","flow","flight"]
输出: "fl"
```
示例 2:
```
输入: ["dog","racecar","car"]
输出: ""
解释: 输入不存在公共前缀。
```
说明:
所有输入只包含小写字母 a-z 。

### 解法1：分治法

vector 分治法查找即可。

```cpp
class Solution {
public:
    // 两个字符串比较 
    string twoPrefix(string a, string b) {
        int n = min(a.length(), b.length());
        int i = 0;
        while(i<n&&a[i]==b[i]) i++;
        return a.substr(0,i);
    }
    // 二分方法
    string commonPrefix(vector<string>& strs, int left, int right) {
        if(left>right) return "";
        else if(left==right) return strs[left];
        else if(left+1==right) return twoPrefix(strs[left], strs[right]);
        else {
            int mid = left + (right-left)/2;
            string leftPre = commonPrefix(strs, left, mid);
            string rightPre = commonPrefix(strs, mid+1, right);
            return twoPrefix(leftPre, rightPre);
        }
    }
    // 最终方法
    string longestCommonPrefix(vector<string>& strs) {
        int n = strs.size();
        return commonPrefix(strs, 0, n-1);
    }
};
```



### 复杂度分析

但是为什么内存消耗这么高？

>执行用时 : 4 ms, 在所有 cpp 提交中击败了 96.25% 的用户
>内存消耗 : 11.4 MB, 在所有 cpp 提交中击败了 8.55% 的用户



最坏情况下，我们有 n 个长度为 m 的相同字符串。

**时间复杂度**：O(S)，S 是所有字符串中字符数量的总和，S=m*n。

时间复杂度的递推式为$T(n)=2 \cdot T(\frac{n}{2})+O(m)$， 化简后可知其就是 O(S)。最好情况下，算法会进行 $minLen\cdot n$ 次比较，其中 $minLen$ 是数组中最短字符串的长度。

**空间复杂度**：$O(m \cdot log(n))$

内存开支主要是递归过程中使用的栈空间所消耗的。 一共会进行 $log(n)$ 次递归，每次需要 m 的空间存储返回结果，所以空间复杂度为 $O(m \cdot log(n))$。



### 解法2：二分法

找出最大前缀长度，对长度进行二分检验。

```cpp
class Solution {
public:
    // 长度 len 的前缀是不是公共前缀
    bool isCommonPrefix(vector<string>& strs, int len) {
        string prefix = strs[0].substr(0, len);
        for(int i=1;i<strs.size();i++) {
            if (strs[i].rfind(prefix, 0) == 0) {
                // starts with prefix
                continue;
            } else {
                return false;
            }
        }
        return true;
    }
    string longestCommonPrefix(vector<string>& strs) {
        if(strs.empty()) return "";
        // 找出最短字符串长度
        int minLength = strs[0].length();
        for(int i=1;i<strs.size();i++) {
            int tempL = strs[i].length();
            minLength = min(minLength, tempL);
        }
        int left = 0;
        int right = minLength;
        // 二分
        while(left<right) {
            int mid = left + (right - left)/2;
            if(isCommonPrefix(strs, mid)) {
                left = mid + 1;
            } else {
                right = mid;
            }
        }
        if(!isCommonPrefix(strs, left)) {
            left--;
        }
        return strs[0].substr(0, left);
    }
};
```



### 复杂度分析

>  执行用时 :12 ms, 在所有 cpp 提交中击败了31.58%的用户
>
> 内存消耗 :9 MB, 在所有 cpp 提交中击败了73.69%的用户



最坏情况下，我们有 n 个长度为 m 的相同字符串。

时间复杂度：$O(S \cdot log(n))$，其中 S 所有字符串中字符数量的总和。

算法一共会进行 log(n)log(n) 次迭代，每次一都会进行 S=m∗n 次比较，所以总时间复杂度为 $O(S \cdot log(n))$。

空间复杂度：O(1)，我们只需要使用常数级别的额外空间。



### 解法 3：Swift 暴力解法

```swift
class Solution {
    func longestCommonPrefix(_ strs: [String]) -> String {
        guard let first = strs.min(), let last = strs.max() else { return "" }
        return first.commonPrefix(with: last, options: .literal)
    }
}
```

