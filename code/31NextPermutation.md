### [Next Permutation](https://leetcode-cn.com/problems/next-permutation/)

实现获取下一个排列的函数，算法需要将给定数字序列重新排列成字典序中下一个更大的排列。

如果不存在下一个更大的排列，则将数字重新排列成最小的排列（即升序排列）。

必须原地修改，只允许使用额外常数空间。

以下是一些例子，输入位于左侧列，其相应输出位于右侧列。
1,2,3 → 1,3,2
3,2,1 → 1,2,3
1,1,5 → 1,5,1


### 解法

1. 双循环，找到尽量低位置换的数字
2. 将此数字后面的部分重新排序

举例：1 → 3 → 2
1. 2 → 3 → 1
2. 2 → 1 → 3

```cpp
class Solution {
public:
    void nextPermutation(vector<int>& nums) {
        for (int i = nums.size()-1;i>=0;i--) {
            for (int j = nums.size()-1;j>i;j--) {
                if (nums[i]<nums[j]) {
                    swap(nums[i],nums[j]);
                    quickSort(nums, i+1, nums.size()-1);
                    return;
                }
            }
        }
        return reverse(nums.begin(),nums.end());
    }

    void swap(int &a, int &b) {
        int temp = a;
        a = b;
        b = temp;
    }

    int partition(vector<int> &vi, int low, int up)
    {
        int pivot = vi[up];
        int i = low-1;
        for (int j = low; j < up; j++) {
        if(vi[j] <= pivot) {
            i++;
            swap(vi[i], vi[j]);
        }
        }
        swap(vi[i+1], vi[up]);
        return i+1;
    }

    void quickSort(vector<int> &vi, int low, int up)
    {
        if(low < up) {
            int mid = partition(vi, low, up);
            quickSort(vi, low, mid-1);
            quickSort(vi, mid+1, up);
        }
    }
};
```
