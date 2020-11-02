### 349. 两个数组的交集

给定两个数组，编写一个函数来计算它们的交集。

 

示例 1：
```
输入：nums1 = [1,2,2,1], nums2 = [2,2]
输出：[2]
```
示例 2：
```
输入：nums1 = [4,9,5], nums2 = [9,4,9,8,4]
输出：[9,4]
```

### 解法

```cpp
class Solution {
public:
    vector<int> intersection(vector<int>& nums1, vector<int>& nums2) {
        set<int> set;
        for (int a : nums1) {
            set.insert(a);
        }
        vector<int> result;
        for (int b : nums2) {
            if (set.count(b) > 0) {
                result.push_back(b);
                set.erase(b); // 避免输出重复元素
            }
        }
        return result;
    }
};
```
