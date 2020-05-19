### 41. First Missing Positive

给定一个未排序的整数数组，找出其中没有出现的最小的正整数。

示例 1:
```
输入: [1,2,0]
输出: 3
```
示例 2:
```
输入: [3,4,-1,1]
输出: 2
```
示例 3:
```
输入: [7,8,9,11,12]
输出: 1
```
说明:

你的算法的时间复杂度应为O(n)，并且只能使用常数级别的空间。



### 解法：拿自己作为哈希表

拿自己作为哈希表，对于 nums[i] > 0，代表 i 没有出现过。

**第一次循环**
1. 判断 1 是否存在
2. 过滤掉 nums[i]<=0||nums[i]>nums.size()，全部替换为 nums[i]=1

**第二次循环**
1. 如果 nums[i] == 1 || -1，continue
2. 否则，temp = abs(nums[i])，说明 temp 出现过，则更新 nums[temp-1] 为相对应的负数

**第三次循环**

1. 寻找第一个 nums[i]，返回 i+1，说明 mei+1 没有出现过。否则返回 nums.size()+1



**代码如下**


```cpp
class Solution {
public:
    int firstMissingPositive(vector<int>& nums) {
        bool is1Showed = false;
        for(int i=0;i<nums.size();i++) {
            if(nums[i]==1) {
                is1Showed = true;
            }
            if(nums[i]<=0||nums[i]>nums.size()) {
                nums[i]=1;
            }
        }
        if(is1Showed==false) return 1;
        for(int i=0;i<nums.size();i++) {
            if(nums[i]==1||nums[i]==-1) {
                continue;
            } else {
                int temp = abs(nums[i])-1;
                nums[temp] = -abs(nums[temp]); 
            }
        }
        for(int i=0;i<nums.size();i++) {
            if(i==0) continue;
            if(nums[i]>0) return i+1;
        }
        return nums.size()+1;
    }
};
```

