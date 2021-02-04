### [[643. 子数组最大平均数 I](https://leetcode-cn.com/problems/maximum-average-subarray-i/)](https://leetcode-cn.com/problems/longest-continuous-increasing-subsequence/)

给定 n 个整数，找出平均数最大且长度为 k 的连续子数组，并输出该最大平均数。

 

示例：

```
输入：[1,12,-5,-6,50,3], k = 4
输出：12.75
解释：最大平均数 (12-5-6+50)/4 = 51/4 = 12.75
```


### 解法：滑动窗口

```cpp
class Solution {
public:
    double findMaxAverage(vector<int>& nums, int k) {
        int result = 0;
        int window = 0;
        int i = 0;
        // 构建窗口
        while (i<k) {
            window += nums[i];
            i++;
        }
        result = window;
        // 滑动窗口
        while (i<nums.size()) {
            window = window - nums[i-k] + nums[i];
            result = max(result, window);
            i++;
        }
        return result / double(k);
    }
};
```
