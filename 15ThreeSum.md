### 15. 3Sum

给定一个包含 n 个整数的数组 nums，判断 nums 中是否存在三个元素 a，b，c ，使得 a + b + c = 0 ？找出所有满足条件且不重复的三元组。

注意：答案中不可以包含重复的三元组。

```
例如, 给定数组 nums = [-1, 0, 1, 2, -1, -4]，

满足要求的三元组集合为：
[
  [-1, 0, 1],
  [-1, -1, 2]
]
```

### 解法：排序后双指针

```cpp
class Solution {
public: 
    vector<vector<int>> threeSum(vector<int>& nums) {
        vector<vector<int>> result;
        if (nums.size()<=2) return result;
        sort( nums.begin(), nums.end() );
        for(int i=0;i<nums.size()-2;i++) {
            // avoid duplicates
            if(i>0&&nums[i]==nums[i-1]) continue;
            int aim = -nums[i];
            int left = i+1, right = nums.size()-1;
            while(right>left) {
                // avoid duplicates
                if(left>i+1&&nums[left]==nums[left-1]) { left++;continue; }
                if(right<nums.size()-1&&nums[right]==nums[right+1]) { right--;continue; }
                if(nums[right] + nums[left] == aim) {
                    result.push_back({nums[i], nums[left], nums[right]});
                    left++;
                    right--;
                } else if (nums[right] + nums[left] > aim) {
                    right--;
                } else {
                    left++;
                }
            }
        }
        return result;
    }
};
```