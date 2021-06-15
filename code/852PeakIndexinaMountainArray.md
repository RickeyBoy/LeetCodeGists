#### [852. 山脉数组的峰顶索引](https://leetcode-cn.com/problems/peak-index-in-a-mountain-array/)

符合下列属性的数组 arr 称为 山脉数组 ：
arr.length >= 3
存在 i（0 < i < arr.length - 1）使得：
arr[0] < arr[1] < ... arr[i-1] < arr[i]
arr[i] > arr[i+1] > ... > arr[arr.length - 1]
给你由整数组成的山脉数组 arr ，返回任何满足 arr[0] < arr[1] < ... arr[i - 1] < arr[i] > arr[i + 1] > ... > arr[arr.length - 1] 的下标 i 。

**进阶：**很容易想到时间复杂度 `O(n)` 的解决方案，你可以设计一个 `O(log(n))` 的解决方案吗？



### 解法：二分

```cpp
class Solution {
public:
    int peakIndexInMountainArray(vector<int>& arr) {
        int left = 0, right = arr.size()-1;
        int mid = (left + right)/2;
        while (mid>left && mid<right) {
            if (arr[mid] < arr[mid+1]) {
                left = mid;
            } else {
                right = mid;
            }
            mid = (left + right)/2;
        }
        if (arr[mid] < arr[mid+1]) {
            return mid+1;
        } else {
            return mid;
        }
    }
};
```
