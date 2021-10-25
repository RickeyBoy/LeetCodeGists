#### [35. 搜索插入位置](https://leetcode-cn.com/problems/search-insert-position/)

给定一个排序数组和一个目标值，在数组中找到目标值，并返回其索引。如果目标值不存在于数组中，返回它将会被按顺序插入的位置。

请必须使用时间复杂度为 O(log n) 的算法。

 

示例 1:
```
输入: nums = [1,3,5,6], target = 5
输出: 2
```

### 解法：二分查找

```cpp
class Solution {
public:
    int searchInsert(vector<int>& nums, int target) {
        int left = 0;
        int right = nums.size()-1;
        while (right > left + 1) {
            int mid = left + (right - left)/2;
            if (nums[mid]==target) {
                return mid;
            } else if (nums[mid]<target) {
                left = mid;
            } else {
                right = mid;
            }
        }
        if (nums[left] >= target) {
            return left;
        } else  if (nums[right] < target) {
            return right+1;
        } else {
            return left + 1;
        }
    }
};
```