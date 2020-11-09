# Quick Select 快速选择算法

快速选择是一种从无序列表找到第k小元素的选择算法。

Quick select 采用和 Quick sort类似的步骤。首先选定一个pivot，然后根据每个数字与该pivot的大小关系将整个数组分为两部分。那么与Quick sort不同的是，Quick select只考虑所寻找的目标所在的那一部分子数组，而非像Quick sort一样分别再对两边进行分割。

正是因为如此，Quick select 将"先快排再选前 K 个"的复杂度从 O(nlogn) 降到了 O(n)。

### 核心方法

1. 随机选取一个 pivot
2. 对整个 array 针对 pivot 进行 partition
3. 将 pivot 置换到队列中间
4. [leftPart, pivot, rightPart]
4.1 如果 K == leftLength + 1，直接返回 Target
4.2 如果 K <= leftLength，递归 leftPart
4.3 如果 K > leftLength，递归 rightPart

### 复杂度

- 时间复杂度 O(n)
一般来说，因为我们才用了随机选取pivot的过程，平均来看，我们可以假设每次pivot都能选在中间位置。
设算法时间复杂度为T(n)。在第一层循环中，我们将pivot与n个元素进行了比较，这个时间为cn 。
所以第一步时间为：T(n) = cn + T(n/2)。其中T(n/2)为接下来递归搜索其中一半的子数组所需要的时间。
在递归过程中，我们可以得到如下公式：
T(n/2) = c(n/2) + T(n/4)
T(n/4) = c(n/4) + T(n/8)
...
T(2) = 2*c + T(1)
T(1) = 1*c
将以上公式循环相加消除T项可以得到：
T(n) = c(n + n/2 + n/4 + n/8 + ... + 2 + 1) = 2n = O(n)
因此得到Quick Select算法的时间复杂度为O(n)。

- 空间复杂度 O(1)
算法没有使用额外空间，swap操作是inplace操作，所以算法的空间复杂度为O(1)。

### 代码

```cpp
void swap(int &a, int &b) {
    int temp = a;
    a = b;
    b = temp;
}

int findKthLargest(vector<int>& nums, int k) {
    int l = 0, r = nums.size()-1;
    while(l <= r) {
        int index = partition(nums,l,r);
        if(index==k) return nums[index];
        else if(index<k) l = index+1;
        else r = index-1;
    }
    return 0;
}

int partition(vector<int> &vi, int low, int up) {
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
```