#### [977. 有序数组的平方](https://leetcode-cn.com/problems/squares-of-a-sorted-array/)

给你一个按 非递减顺序 排序的整数数组 nums，返回 每个数字的平方 组成的新数组，要求也按 非递减顺序 排序。

 

示例 1：
```
输入：nums = [-4,-1,0,3,10]
输出：[0,1,9,16,100]
解释：平方后，数组变为 [16,1,0,9,100]
排序后，数组变为 [0,1,9,16,100]
```

### 解法：双指针

```cpp
class Solution {
public:
    vector<int> sortedSquares(vector<int>& nums) {
        vector<int> res = vector(nums.size(), 0);
        int cur = nums.size()-1;
        int left = 0;
        int right = nums.size()-1;
        while (right>=left) {
            if (nums[right]<=0 || -nums[left] > nums[right]) {
                // 计算左指针
                res[cur] = nums[left]*nums[left];
                left++;
                cur--;
            } else {
                // 计算右指针
                res[cur] = nums[right]*nums[right];
                right--;
                cur--;
            }
        }
        return res;
    }
};
```
