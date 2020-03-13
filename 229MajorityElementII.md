### 229. 求众数 II

给定一个大小为 n 的数组，找出其中所有出现超过 ⌊ n/3 ⌋ 次的元素。

说明: 要求算法的时间复杂度为 O(n)，空间复杂度为 O(1)。

示例 1:
```
输入: [3,2,3]
输出: [3]
```
示例 2:
```
输入: [1,1,1,3,3,2,2,2]
输出: [1,2]
```


### 解法：摩尔投票延伸

```cpp
class Solution {
public:
    vector<int> majorityElement(vector<int>& nums) {
        int count1 = 0, count2 = 0, candidate1 = -1, candidate2 = -1;
        for (int i=0;i<nums.size();i++) {
            if(nums[i]==candidate1) {
                count1++;
            } else if(nums[i]==candidate2) {
                count2++;
            } else if(count1==0) {
                candidate1 = nums[i];
                count1++;
            } else if(count2==0) {
                candidate2 = nums[i];
                count2++;
            } else {
                count1--;
                count2--;
            }
        }
        count1=0;
        count2=0;
        printf("%d,%d",candidate1,candidate2);
        for (int i=0;i<nums.size();i++) {
            if(nums[i]==candidate1) count1++;
            else if(nums[i]==candidate2) count2++;
        }
        vector<int> result;
        if(count1>nums.size()/3) result.push_back(candidate1);
        if(count2>nums.size()/3) result.push_back(candidate2);
        return result;
    }
};
```
