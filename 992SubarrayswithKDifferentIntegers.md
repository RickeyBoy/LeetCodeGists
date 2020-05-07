### 992. K 个不同整数的子数组

给定一个正整数数组 A，如果 A 的某个子数组中不同整数的个数恰好为 K，则称 A 的这个连续、不一定独立的子数组为好子数组。

（例如，[1,2,3,1,2] 中有 3 个不同的整数：1，2，以及 3。）

返回 A 中好子数组的数目。

 

示例 1：
```
输入：A = [1,2,1,2,3], K = 2
输出：7
解释：恰好由 2 个不同整数组成的子数组：[1,2], [2,1], [1,2], [2,3], [1,2,1], [2,1,2], [1,2,1,2].
```
示例 2：
```
输入：A = [1,2,1,3,4], K = 3
输出：3
解释：恰好由 3 个不同整数组成的子数组：[1,2,1,3], [2,1,3], [1,3,4].
```

提示：
```
1 <= A.length <= 20000
1 <= A[i] <= A.length
1 <= K <= A.length
```

### 解法：滑动窗口 + 回溯

[我的题解 - leetcode](https://leetcode-cn.com/problems/subarrays-with-k-different-integers/solution/hua-dong-chuang-kou-hui-su-fa-by-rickeyboy/)

1. 用滑动窗口思想，找到每次 diffNum == K 的时刻
2. 固定窗口右指针，遍历左指针找到所有符合的结果
3. 回溯左指针

```cpp
class Solution {
public:
    int subarraysWithKDistinct(vector<int>& A, int K) {
        unordered_map<int, int> window;
  	    int left = 0, right = 0;
        int result = 0;
        int diffNum = 0;  // 不同整数的个数
        while (right < A.size()) {
            // 右移窗口
            window[A[right]]++;
            if (window[A[right]]==1) diffNum++;
            right++;
            // 判断左侧窗口是否要收缩
            while (diffNum>K) {
                // 左移窗口
                window[A[left]]--;
                if (window[A[left]]==0) diffNum--;
                left++;
            }
            int temp = left;
            // 遍历符合的结果
            if (diffNum==K) {
                while(diffNum==K) {
                    // 一个符合的结果
                    result++;
                    // 不断左移窗口
                    window[A[left]]--;
                    if (window[A[left]]==0) diffNum--;
                    left++;
                }
                while(left>temp) {
                    // 回溯 left 指针
                    left--;
                    window[A[left]]++;
                    if (window[A[left]]==1) diffNum++;
                }
            }
        }
        return result;
    }
};
```
