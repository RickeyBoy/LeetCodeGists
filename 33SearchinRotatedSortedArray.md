### 33. Search in Rotated Sorted Array

假设按照升序排序的数组在预先未知的某个点上进行了旋转。

( 例如，数组 [0,1,2,4,5,6,7] 可能变为 [4,5,6,7,0,1,2] )。

搜索一个给定的目标值，如果数组中存在这个目标值，则返回它的索引，否则返回 -1 。

你可以假设数组中不存在重复的元素。

你的算法时间复杂度必须是 O(log n) 级别。

示例 1:
```
输入: nums = [4,5,6,7,0,1,2], target = 0
输出: 4
```
示例 2:
```
输入: nums = [4,5,6,7,0,1,2], target = 3
输出: -1
```

### 解法：二分法

关键函数 `searchHalf` 的二分逻辑：
1. `nums[left]<nums[mid]` 说明左半部分为连续数组，旋转点在右半部分；否则反之
2. 如果 `target<=nums[mid]&&nums[left]<=target` 说明目标点在连续数组的一侧；否则反之。

```cpp
class Solution {
public:
    int searchHalf(vector<int>& nums, int target, int left, int right) {
        int mid = left + (right - left)/2;
        if(nums[left]<nums[mid]) {
            if(target<=nums[mid]&&nums[left]<=target) return -1;
            else return 1;
        } else {
            if(target>nums[mid]&&nums[right]>=target) return 1;
            else return -1;
        }
    }
    int search(vector<int>& nums, int target) {
        int left = 0, right = nums.size()-1;
        while(right>=left) {
            int res = searchHalf(nums, target, left, right);
            int mid = left + (right - left)/2;
            if(nums[left] == target){
                return left;
            } else if(nums[mid] == target){
                return mid;
            } else if(nums[right] == target){
                return right;
            } else if(res == -1){
                right = mid-1;
            } else {
                left = mid+1;
            }
        }
        return -1;
    }
};
```