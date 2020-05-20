### 16. 最接近的三数之和

给定一个包括 n 个整数的数组 nums 和 一个目标值 target。找出 nums 中的三个整数，使得它们的和与 target 最接近。返回这三个数的和。假定每组输入只存在唯一答案。

例如，给定数组 nums = [-1，2，1，-4], 和 target = 1.

```
与 target 最接近的三个数的和为 2. (-1 + 2 + 1 = 2).
```

### 解法：排序后双指针

```cpp
class Solution {
public:
    int threeSumClosest(vector<int>& nums, int target) {
        int result = INT_MAX;
        if (nums.size()<=2) return result;
        sort( nums.begin(), nums.end() );
        for(int i=0;i<nums.size()-2;i++) {
            // avoid duplicates
            if(i>0 && nums[i] == nums[i-1]) continue;
            int left = i+1, right = nums.size()-1;
            // 双指针
            while(right>left) {
                // avoid duplicates
                if(left>i+1 && nums[left]==nums[left-1]) { left++;continue; }
                if(right<nums.size()-1 && nums[right]==nums[right+1]) { right--;continue; }
                // 移动指针
                int delta = target-nums[i]-nums[left]-nums[right];
                if(delta==0) {
                    return target;
                } else if (delta<0) {
                    right--;
                } else {
                    left++;
                }
                // 贪心更新 result
                if (abs(result)>abs(delta)) {
                    result = delta;
                }
            }
        }
        return target - result;
    }
};
```