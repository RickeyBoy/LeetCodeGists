#### [215. 数组中的第K个最大元素](https://leetcode-cn.com/problems/kth-largest-element-in-an-array/)

给定整数数组 nums 和整数 k，请返回数组中第 k 个最大的元素。

请注意，你需要找的是数组排序后的第 k 个最大的元素，而不是第 k 个不同的元素。

 

示例 1:
```
输入: [3,2,1,5,6,4] 和 k = 2
输出: 5
```
示例 2:
```
输入: [3,2,3,1,2,4,5,5,6] 和 k = 4
输出: 4
```

提示：
```
1 <= k <= nums.length <= 104
-104 <= nums[i] <= 104
```

### 解法：堆排序


```cpp
class Solution {
public:
    int findKthLargest(vector<int>& nums, int k) {
        priority_queue<int> heap;
        for (int x : nums) {
            heap.push(x);
        }
        for (int i=0;i<k-1;i++) {
            heap.pop();
        }
        return heap.top();
    }
};
```

