### 4. Median of Two Sorted Arrays.md

给定两个大小为 m 和 n 的有序数组 nums1 和 nums2。

请你找出这两个有序数组的中位数，并且要求算法的时间复杂度为 O(log(m + n))。

你可以假设 nums1 和 nums2 不会同时为空。

示例 1:
```
nums1 = [1, 3]
nums2 = [2]

则中位数是 2.0
```
示例 2:
```
nums1 = [1, 2]
nums2 = [3, 4]

则中位数是 (2 + 3)/2 = 2.5
```

### 解法

[官方题解](https://leetcode-cn.com/problems/median-of-two-sorted-arrays/solution/xun-zhao-liang-ge-you-xu-shu-zu-de-zhong-wei-shu-b/)

##### 核心思想
1. 两个指针分别为 i、j，保证 i、j 左右部分个数相等。推断得到关系式 $j = \frac{m+n+1}{2} - i$ 
2. 找到合适的 i 的终止条件：i、j 左侧所有元素的最大值 $max([i-1], [j-1])$ 小于右侧所有元素最小值 $min([i], [j])$，说明 i、j 就是两个中位数。
3. 采用二分法，寻找 i 的值，用条件 2 作为终止条件。
4. 通常结果：i 和 j 分别在 nums1，nums2 中间，代表两个中位数分别在这两个 nums 中。
5. 但是有非常多的边界条件：
   1. i、j 有可能越界。所以需要保证 nums1 更短。
   2. 可能 i == 0。说明两个中位数都在 nums2 中。
   3. 可能 i == m。说明两个中位数都在 nums1 中。

```cpp
class Solution {
public:
    double findMedianSortedArrays(vector<int>& nums1, vector<int>& nums2) {
        // 保证 nums1 更短
        if(nums1.size()>nums2.size()) {
            return findMedianSortedArrays(nums2, nums1);
        }
        int isEven = (nums1.size()+nums2.size())%2==0;
        int left = 0;
        int right = nums1.size();
        int halfLen = (nums1.size()+nums2.size()+1)/2;
        while(left<=right) {
            int i = (left + right)/2;
            int j = halfLen - i;
            if(i<right && nums2[j-1]>nums1[i]) {
                // i 需要右移
                left = i+1;
            } else if (i>left && nums1[i-1]>nums2[j]) {
                // i 需要左移
                right = i-1;
            } else {
                // i 正好，但是需要判定边界情况
                int maxLeft = 0;
                if (i == 0) { maxLeft = nums2[j-1]; } // i==0,说明两个中位数都在 nums2 中
                else if (j == 0) { maxLeft = nums1[i-1]; } // j==0,说明两个中位数都在 nums1 中
                else { maxLeft = max(nums1[i-1], nums2[j-1]); } // 否则说明分别在两个 nums 中
                // 奇数可以直接返回 maxLeft
                if ( !isEven ) { return maxLeft; }
                // 同理
                int minRight = 0;
                if (i == nums1.size()) { minRight = nums2[j]; }
                else if (j == nums2.size()) { minRight = nums1[i]; }
                else { minRight = min(nums2[j], nums1[i]); }
                // 偶数需要 /2.0
                return (maxLeft + minRight) / 2.0;
            }
        }
        return 0.0;
    }
};
```
