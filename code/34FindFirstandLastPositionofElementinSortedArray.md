### [34. 在排序数组中查找元素的第一个和最后一个位置](https://leetcode-cn.com/problems/find-first-and-last-position-of-element-in-sorted-array/)

给定一个按照升序排列的整数数组 nums，和一个目标值 target。找出给定目标值在数组中的开始位置和结束位置。

如果数组中不存在目标值 target，返回 [-1, -1]。

进阶：

你可以设计并实现时间复杂度为 O(log n) 的算法解决此问题吗？

```
示例 1：

输入：nums = [5,7,7,8,8,10], target = 8
输出：[3,4]
示例 2：

输入：nums = [5,7,7,8,8,10], target = 6
输出：[-1,-1]
示例 3：

输入：nums = [], target = 0
输出：[-1,-1]
```

提示：
- 0 <= nums.length <= 105
- 109 <= nums[i] <= 109
- nums 是一个非递减数组
- 109 <= target <= 109

### 解法：二分查找

- 注意边界信息！

```cpp
class Solution {
public:
    // 二分寻找一个 target
    int findTarget(vector<int>& nums, int target) {
        int left = 0;
        int right = nums.size()-1;
        if (nums.size() == 0) return -1; // 注意边界
        if (nums[right]==target) return right;
        if (nums[left]==target) return left;
        while (right>=left) {
            // 二分查找
            int mid = left + (right-left)/2;
            if (nums[mid]==target) {
                return mid;
            } else if (nums[mid]<target) {
                left = mid+1;
            } else {
                right = mid-1;
            }
        }
        return -1;
    }
    // 分区间找 head or tail
    int findHeadOrTail(vector<int>& nums, int target, int initIndex, bool isFirst) {
        int left = 0;
        int right = nums.size()-1;
        if (initIndex == -1) return -1;// 没有target，直接返回
        if (isFirst) {
            // 寻找起点
            right = initIndex; // 右指针需要+1
        } else {
            // 寻找末尾
            left = initIndex;
        }
        while (right-left>1) {
            // 二分查找
            int mid = left + (right-left)/2;
            if (nums[mid]==target) {
                if (isFirst) {
                    // 寻找起点
                    right = mid;
                } else {
                    // 寻找末尾
                    left = mid;
                }
            } else if (nums[mid]<target) {
                left = mid;
            } else {
                right = mid;
            }
        }
        if (isFirst) {
             // 寻找起点
             if (nums[left] == target) return left;
            return right;
        } else {
            // 寻找末尾
            if (nums[right] == target) return right;
            return left;
        }
    }
    vector<int> searchRange(vector<int>& nums, int target) {
        vector<int> result = vector(2,0);
        int firstTarget = findTarget(nums,target);
        result[0] = findHeadOrTail(nums,target,firstTarget,true);
        result[1] = findHeadOrTail(nums,target,firstTarget,false);
        return result;
    }
};
```