# LeetCode 二叉堆

### 概述

|      | LeetCode                                                     | 方法                         | 备注                 |                                                              |
| ---- | ------------------------------------------------------------ | ---------------------------- | -------------------- | ------------------------------------------------------------ |
| 1    | [23. 合并K个升序链表（困难）](https://leetcode-cn.com/problems/merge-k-sorted-lists/) | 优先级队列（二叉堆） + dummy | 【重点题】+ 求复杂度 | [解](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/23MergekSortedLists.md) |
| 2    | [215. 数组中的第K个最大元素](https://leetcode-cn.com/problems/kth-largest-element-in-an-array/) | 大顶堆                       |                      | [解](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/215KthLargestElementinanArray.md) |

### 二叉堆基础概念

> 参考：https://oi-wiki.org/ds/binary-heap/

堆是一棵树，其每个节点都有一个键值，且每个节点的键值都大于等于/小于等于其父亲的键值。

![rickey_4951](https://github.com/RickeyBoy/LeetCodeGists/blob/master/images/rickey_4951.png?raw=true)

STL 中的 priority_queue 其实就是一个大根堆。

```cpp
// 声明方式 小顶堆
struct compare {
	bool operator()(ListNode* a, ListNode* b) {
		return a->val > b->val;
	}
};
priority_queue <ListNode*, vector<ListNode*>, compare> queue; 
```

### 二叉堆特性

- 完全二叉树
- 插入 $O(logn)$
- 查询最大值 $O(1)$
- 删除最大值 $O(logn)$
- 合并 $O(n)$
- 增大一个元素的值 $O(logn)$
- 支持持久化

### 215 Kth Largest 模板

```cpp
int findKthLargest(vector<int>& nums, int k) {
  	// 最小堆，堆顶是第 k 大的元素
    priority_queue<int, vector<int>, greater<int>> minHeap; 
    for (int num : nums) {
        minHeap.push(num);
        if (minHeap.size() > k) {
            minHeap.pop(); // 保证堆中最多有 k 个元素
        }
    }
    return minHeap.top(); // 堆顶就是第 k 大元素
}
```

对比用 QuickSelect

```cpp
class Solution {
public:
    // 主函数：返回第 k 大元素
    int findKthLargest(vector<int>& nums, int k) {
        // QuickSelect 本质是找 "第 k 大" 对应的 "第 (k-1) 小"
        return quickSelect(nums, 0, nums.size() - 1, k);
    }
private:
    // QuickSelect 主逻辑：在 nums[left...right] 中找第 k 大
    int quickSelect(vector<int>& nums, int left, int right, int k) {
        int pivot = nums[right];       // 选取最右边为 pivot
        int i = left;                  // i 是分区指针
      
        // 把 >= pivot 的数放左边，< pivot 的放右边
        for (int j = left; j < right; ++j) {
            if (nums[j] >= pivot) {
                swap(nums[i], nums[j]);
                i++;
            }
        }
        swap(nums[i], nums[right]); // 把 pivot 放到中间
        int count = i - left + 1;   // 左边含 pivot 的元素个数（即当前是第几大）
      
        if (count == k) return nums[i]; // 正好是第 k 大
        else if (count > k) return quickSelect(nums, left, i - 1, k); // 第 k 大在左边
        else return quickSelect(nums, i + 1, right, k - count); // 在右边，更新 k
    }
};
```

### 327 Top K Frequent

用 `unordered_map` 额外存频率，二叉堆用 Pair 排序

```cpp
vector<int> topKFrequent(vector<int>& nums, int k) {
    unordered_map<int, int> freq;
    for (int num : nums) freq[num]++;
		// 堆 + Pair，默认先比较 Pair 的第一个元素
    priority_queue<pair<int, int>, vector<pair<int, int>>, greater<>> minHeap;
    for (auto& [num, count] : freq) {
        minHeap.push({count, num});
        if (minHeap.size() > k) minHeap.pop();
    }

    vector<int> res;
    while (!minHeap.empty()) {
        res.push_back(minHeap.top().second);
        minHeap.pop();
    }
    return res;
}
```

### 二叉堆操作

##### 查询最大值

> priority_queue.top

1. 直接获取 root 节点

##### 插入操作

> priority_queue.push

1. 从最下层最右侧（如果满了就新开一层）插入新叶子节点
2. 向上调整：将叶子节点与父节点比较，如果不满足大根堆，则互换位置
3. 循环比较，直到叶子节点满足大根堆

##### 删除最大值

> priority_queue.pop

1. 将最下层最右侧的叶子节点放到根节点，原有根节点删除
2. 向下调整：选择两个叶子节点中的更大值，和根节点进行位置互换
3. 循环比较，直到节点满足大根堆

##### 增大元素的值

1. 向上调整即可

### 具体操作

考虑使用一个序列 $h$ 来表示堆。$h_i$ 的两个儿子分别是 $h_{2i}$ 和 $h_{2i+1}$，1 是根结点。

##### 向上调整（叶子节点不断向上）

```cpp
void up(int x) {
  while (x > 1 && h[x] > h[x / 2]) {
    swap(h[x], h[x / 2]);
    x /= 2;
  }
}
```

##### 向下调整（根节点不断向下）

```cpp
void down(int x) {
  while (x * 2 <= n) {
    t = x * 2;
    if (t + 1 <= n && h[t + 1] > h[t]) t++;
    if (h[t] <= h[x]) break;
    std::swap(h[x], h[t]);
    x = t;
  }
}
```

##### 建堆

> `priority_queue<int> q;` 大顶堆

1. 方法一：使用 decreasekey（即，向上调整）。从根开始，按 BFS 序进行。 $O(nlogn)$

```cpp
void build_heap_2() {
  for (i = n; i >= 1; i--) up(i);
}
```

2. 这时换一种思路，从叶子开始，逐个向下调整。 $O(n)$

```cpp
void build_heap_2() {
  for (i = n; i >= 1; i--) down(i);
}
```

