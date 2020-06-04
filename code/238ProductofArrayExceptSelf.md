### 238. 除自身以外数组的乘积

给你一个长度为 n 的整数数组 nums，其中 n > 1，返回输出数组 output ，其中 output[i] 等于 nums 中除 nums[i] 之外其余各元素的乘积。

 

示例:
```
输入: [1,2,3,4]
输出: [24,12,8,6]
```

提示：题目数据保证数组之中任意元素的全部前缀元素和后缀（甚至是整个数组）的乘积都在 32 位整数范围内。

说明: 请不要使用除法，且在 O(n) 时间复杂度内完成此题。

进阶：
你可以在常数空间复杂度内完成这个题目吗？（ 出于对空间复杂度分析的目的，输出数组不被视为额外空间。）


### 解法：动态规划 + 压缩

```cpp
class Solution {
public:
    vector<int> productExceptSelf(vector<int>& nums) {
        int n = nums.size();
        if (n<1) return nums;
        // 也用作输出数组
        vector<int> L = vector(n,1);
        // 压缩 R 数组
        int lastR = 1;
        // 构造左数组
        for (int i=1;i<n;i++) {
            L[i]=nums[i-1]*L[i-1];
        }
        // 构造右数组
        for (int i=n-1;i>=0;i--) {
            // 计算结果
            L[i] = L[i]*lastR;
            // 迭代 R
            lastR *= nums[i];
        }
        return L;
    }
};
```
