### 303. Range Sum Query - Immutable

给定一个整数数组  nums，求出数组从索引 i 到 j  (i ≤ j) 范围内元素的总和，包含 i,  j 两点。

示例：
```
给定 nums = [-2, 0, 3, -5, 2, -1]，求和函数为 sumRange()

sumRange(0, 2) -> 1
sumRange(2, 5) -> -1
sumRange(0, 5) -> -3
```
说明:

* 你可以假设数组不可变。
* 会多次调用 sumRange 方法。




### 解法：动态规划

注意边界条件处理

```cpp
class NumArray {
public:
    vector<int> results;
    NumArray(vector<int>& nums) {
        results = nums;
        if(results.size()<=1) return;
        for(int i=1;i<results.size();i++) {
            results[i]+=results[i-1];
        }
        return;
    }
    
    int sumRange(int i, int j) {
        if(i<1) return results[j];
        else return results[j]-results[i-1];
    }
};

/**
 * Your NumArray object will be instantiated and called as such:
 * NumArray* obj = new NumArray(nums);
 * int param_1 = obj->sumRange(i,j);
 */
```
