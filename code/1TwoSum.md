### 1. Two Sum
Given an array of integers, return indices of the two numbers such that they add up to a specific target.
You may assume that each input would have exactly one solution, and you may not use the same element twice.

Example:
```
Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```

### 解法 1 - 0(n^2)
基础 Brute Force，两个 for 循环。
注意：`nums[j] == target - nums[i]`，**避免溢出**，所以用减法。

### 解法 2 - 0(n\*lgn)
先排序，然后首尾逼近。

### 解法 3 - O(n) 
基础哈希表，Unordered Map 用法。
``` cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map<int,int> hash;
        vector<int> res;
        for (int i=0;i<nums.size();i++) {
            int numbersToFind = target - nums[i];
            if (hash.find(numbersToFind)!=hash.end()) {
                // 注意push_back的顺序
                res.push_back(hash[numbersToFind]);
                res.push_back(i);
                return res;
            }
            hash[nums[i]] = i;
        }
        return res;
    }
};
```