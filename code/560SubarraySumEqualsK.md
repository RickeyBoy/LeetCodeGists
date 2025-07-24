### [560. Subarray Sum Equals K](https://leetcode.cn/problems/subarray-sum-equals-k/)

Given an array of integers `nums` and an integer `k`, return *the total number of subarrays whose sum equals to* `k`.

A subarray is a contiguous **non-empty** sequence of elements within an array.

 

**Example 1:**

```
Input: nums = [1,1,1], k = 2
Output: 2
```

**Example 2:**

```
Input: nums = [1,2,3], k = 3
Output: 2
```

 

**Constraints:**

- `1 <= nums.length <= 2 * 104`
- `-1000 <= nums[i] <= 1000`
- `-107 <= k <= 107`


### 解法：前缀和 + Hash map

```cpp
class Solution {
    func subarraySum(_ nums: [Int], _ k: Int) -> Int {
        var n = nums.count
        var sumCount: [Int: Int] = [:] // record aim value to sum to k
        var results = 0
        var sum = 0
        sumCount[0] = 1 // initial
        for i in (1..<n+1) {
            sum+=nums[i-1]
            //print("i=\(i), sum=\(sum), aim=\(sum-k), sumCount[sum-k]=\(sumCount[sum-k, default: 0])")
            results += sumCount[sum-k, default: 0]
            sumCount[sum, default: 0]+=1
        }

        return results;
    }
}
```
