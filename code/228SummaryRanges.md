### [228. 汇总区间](https://leetcode-cn.com/problems/summary-ranges/)

给定一个无重复元素的有序整数数组 nums 。

返回 恰好覆盖数组中所有数字 的 最小有序 区间范围列表。也就是说，nums 的每个元素都恰好被某个区间范围所覆盖，并且不存在属于某个范围但不属于 nums 的数字 x 。

列表中的每个区间范围 [a,b] 应该按如下格式输出：

"a->b" ，如果 a != b
"a" ，如果 a == b

示例 1：
```
输入：nums = [0,1,2,4,5,7]
输出：["0->2","4->5","7"]
解释：区间范围是：
[0,2] --> "0->2"
[4,5] --> "4->5"
[7,7] --> "7"
```


### 解法：双指针

```cpp
class Solution {
public:
    vector<string> summaryRanges(vector<int>& nums) {
        int n = nums.size();
        int left=0, right=1;
        vector<string> result;
        while (left<n) {
            if (right < n && nums[left] + (right - left) == nums[right]) right++;
            else {
                // 区间中断
                if (right == left + 1) {
                    result.push_back(std::to_string(nums[left]));
                } else {
                    result.push_back(std::to_string(nums[left])+"->"+std::to_string(nums[right-1]));
                }
                left = right;
            }
        }
        return result;
    }
};
```
