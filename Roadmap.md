# Rickey's Roadmap

> 参考链接：[LeetCode按照怎样的顺序来刷题比较好？ - 知乎]
> (https://www.zhihu.com/question/36738189/answer/908664455)
>
> ACM金牌选手整理的【LeetCode刷题顺序】 - 编程熊的文章 - 知乎 https://zhuanlan.zhihu.com/p/388470520

## TODO
1. 按照这个顺序再刷题
2. 每个类型应该有原理 + 方法论 + 模板 + 题目分析 + 例题合集



## 数据结构





## 基础类型

### 1. Sliding window，滑动窗口类型

##### 分类

- 固定窗口大小
- 可变窗口，求解最大or最小的满足条件的窗口

##### 求解

- 固定窗口：同时移动左右指针，保证窗口宽度一定
- 可变窗口：分别移动左右指针
- 移动后需要及时更新状态位、最优解等

##### 关键字

“连续子串 xxxx”、“连续子数组 xxxx”

##### 模板

```cpp
/* 滑动窗口算法框架 */
void slidingWindow(string s, string t) {
    unordered_map<char, int> need, window; // 有时可以直接用 vector 替代
  	int left = 0, right = 0;
    int sameCount = 0; 
  	// 初始化
    for (char c : t) need[c]++;
    while (right < s.size()) {
        // 右移窗口
        right++;
        ...

        /*** debug 输出的位置 ***/
        printf("window: [%d, %d)\n", left, right);
        /********************/
      
        // 判断左侧窗口是否要收缩
        while (window needs shrink) {
            // 左移窗口
            left++;
            ...
        }
    }
}
```

##### 例题

- [438. Find All Anagrams in a String 找到字符串中所有字母异位词](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/438FindAllAnagramsinaString.md) - medium
- [76. Minimum Window Substring 最小覆盖子串](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/76MinimumWindowSubstring.md) - hard
- [3. Longest Substring Without Repeating Characters 无重复字符的最长子串](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/3LongestSubstringWithoutRepeatingCharacters.md) - medium
- [567. Permutation in String 字符串的排列](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/567PermutationinString.md) - medium
- [992. Subarrays with K Different Integers K 个不同整数的子数组](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/992SubarrayswithKDifferentIntegers.md) - hard

##### 参考资料

- [labuladong - 滑动窗口](https://mp.weixin.qq.com/s/ioKXTMZufDECBUwRRp3zaA)

### 2. Two points 双指针类型

##### 分类

- （同向）快慢指针：链表、环形数组
- （反向）双向指针：线性数组字符串等
- （同向）滑动窗口：独立章节分析
- （反向）二分查找：独立章节分析

##### 例题

- [141. Linked List Cycle 环形链表](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/141LinkedListCycle.md) - easy
- [142. Linked List Cycle II 环形链表 II](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/142LinkedListCycleII.md) - medium
- [202. Happy Number 快乐数](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/202HappyNumber.md) - easy
- [876. Middle of the Linked List 链表的中间结点](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/876MiddleoftheLinkedList.md) - easy
- [1. Two Sum 两数之和](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/1TwoSum.md) - easy
- [15. 3Sum 三数之和](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/15ThreeSum.md) - medium
- [16. 3Sum Closest 最接近的三数之和](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/16ThreeSumClosest.md) - medium
- [18. 4Sum 四数之和](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/184Sum.md) - medium
- [11. Container With Most Water 盛最多水的容器](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/11ContainerWithMostWater.md) - medium
- [26. Remove Duplicates from Sorted Array 删除排序数组中的重复项](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/26RemoveDuplicatesfromSortedArray.md) - easy
- [27. Remove Element 移除元素](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/27RemoveElement.md) - easy

### 3. Binary Search 二分查找

##### 注意点

- 注意二分的边界条件

##### 例题

- [33. Search in Rotated Sorted Array 搜索旋转排序数组](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/33SearchinRotatedSortedArray.md) - medium
- [34. Find First and Last Position of Element in Sorted Array 在排序数组中查找元素的第一个和最后一个位置](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/34FindFirstandLastPositionofElementinSortedArray.md) - medium



---

TODO：

### 4. Pattern: Merge Intervals，区间合并类型

经典题目：

Merge Intervals (medium)

Insert Interval (medium)

Intervals Intersection (medium)

Conflicting Appointments (medium)

### 5. Pattern: Cyclic Sort，循环排序

Cyclic Sort (easy)Find the Missing Number (easy)Find all Missing Numbers (easy)Find the Duplicate Number (easy)Find all Duplicate Numbers (easy)

### 6. Pattern: In-place Reversal of a LinkedList，链表翻转

Reverse a LinkedList (easy)

Reverse a Sub-list (medium)

Reverse every K-element Sub-list (medium)

### **深度优先搜索DFS**

1. [LeetCode 236. 二叉树的最近公共祖先](https://link.zhihu.com/?target=https%3A//leetcode-cn.com/problems/lowest-common-ancestor-of-a-binary-tree/)
2. [LeetCode 301. 删除无效的括号](https://link.zhihu.com/?target=https%3A//leetcode-cn.com/problems/remove-invalid-parentheses/)

### **宽度优先搜索BFS**

1. [LeetCode 200. 岛屿数量](https://link.zhihu.com/?target=https%3A//leetcode-cn.com/problems/number-of-islands/)
2. [LeetCode 617. 合并二叉树](https://link.zhihu.com/?target=https%3A//leetcode-cn.com/problems/merge-two-binary-trees/)

### 9. Pattern: Two Heaps，双堆类型

Find the Median of a Number Stream (medium)

Sliding Window Median (hard)

Maximize Capital (hard)

### 10. Pattern: Subsets，子集类型，一般都是使用多重DFS

Subsets (easy)Subsets With Duplicates (easy)Permutations (medium)String Permutations by changing case (medium)Balanced Parentheses (hard)Unique Generalized Abbreviations (hard)

### 11. Pattern: Modified Binary Search，改造过的二分

Order-agnostic Binary Search (easy)Ceiling of a Number (medium)Next Letter (medium)Number Range (medium)Search in a Sorted Infinite Array (medium)Minimum Difference Element (medium)Bitonic Array Maximum (easy)

### 12. Pattern: Top ‘K’ Elements，前K个系列

Top ‘K’ Numbers (easy)Kth Smallest Number (easy)‘K’ Closest Points to the Origin (easy)Connect Ropes (easy)Top ‘K’ Frequent Numbers (medium)Frequency Sort (medium)Kth Largest Number in a Stream (medium)‘K’ Closest Numbers (medium)Maximum Distinct Elements (medium)Sum of Elements (medium)Rearrange String (hard)

### 13. Pattern: K-way merge，多路归并

Merge K Sorted Lists (medium)Kth Smallest Number in M Sorted Lists (Medium)Kth Smallest Number in a Sorted Matrix (Hard)Smallest Number Range (Hard)

### 15. Pattern: Topological Sort (Graph)，拓扑排序类型

Topological Sort (medium)Tasks Scheduling (medium)Tasks Scheduling Order (medium)All Tasks Scheduling Orders (hard)Alien Dictionary (hard)

### **字典树Trie**

1. [LeetCode 139. 单词拆分](https://link.zhihu.com/?target=https%3A//leetcode-cn.com/problems/word-break/)
2. [LeetCode 208. 实现 Trie (前缀树)](https://link.zhihu.com/?target=https%3A//leetcode-cn.com/problems/implement-trie-prefix-tree/)

### **递归&回溯**

1. [LeetCode 17. 电话号码的字母组合](https://link.zhihu.com/?target=https%3A//leetcode-cn.com/problems/letter-combinations-of-a-phone-number/)
2. [LeetCode 22. 括号生成](https://link.zhihu.com/?target=https%3A//leetcode-cn.com/problems/generate-parentheses/)
3. [LeetCode 39. 组合总和](https://link.zhihu.com/?target=https%3A//leetcode-cn.com/problems/combination-sum/)
4. [LeetCode 46. 全排列](https://link.zhihu.com/?target=https%3A//leetcode-cn.com/problems/permutations/)
5. [LeetCode 78. 子集](https://link.zhihu.com/?target=https%3A//leetcode-cn.com/problems/subsets/)
6. [LeetCode 79. 单词搜索](https://link.zhihu.com/?target=https%3A//leetcode-cn.com/problems/word-search/)
7. [LeetCode 226. 翻转二叉树](https://link.zhihu.com/?target=https%3A//leetcode-cn.com/problems/invert-binary-tree/)



### **最短路算法**

1. [LeetCode 743. 网络延迟时间](https://link.zhihu.com/?target=https%3A//leetcode-cn.com/problems/network-delay-time/)

### **最小生成树**

1. [1584. 连接所有点的最小费用](https://link.zhihu.com/?target=https%3A//leetcode-cn.com/problems/min-cost-to-connect-all-points/)

### **拓扑排序**

1. [LeetCode 207. 课程表](https://link.zhihu.com/?target=https%3A//leetcode-cn.com/problems/course-schedule/)







## 动态规划

### 1. 0/1 Knapsack, 0/1背包 & Unbounded Knapsack, 无限背包

##### 求解

- 状态转移数组：`dp[背包容量][可选择的物品]`
- 状态转移方程：`dp[i][w] = max(dp[i - 1][w - wt[i-1]] + val[i-1], dp[i - 1][w]);`
- 是否可以状态压缩？

##### 模板

```cpp
/* 01背包算法框架 */
int knapsack(int W, int N, vector<int>& wt, vector<int>& val) {
    // base case 已初始化
    vector<vector<int>> dp(N + 1, vector<int>(W + 1, 0));
    for (int i = 1; i <= N; i++) {
        for (int w = 1; w <= W; w++) {
            if (w - wt[i-1] < 0) {
                // 这种情况下只能选择不装入背包
                dp[i][w] = dp[i - 1][w];
            } else {
                // 装入或者不装入背包，择优
                dp[i][w] = max(dp[i - 1][w - wt[i-1]] + val[i-1], 
                               dp[i - 1][w]);
            }
        }
    }
    return dp[N][W];
}
```

##### 例题

- 子集背包： [416. Partition Equal Subset Sum 分割等和子集](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/416PartitionEqualSubsetSum.md) - medium
- 01 背包：
  - [474. Ones and Zeroes 一和零](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/474OnesandZeroes.md) - medium
  - [494. Target Sum 目标和](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/494TargetSum.md) - medium
- 完全背包：[518. Coin Change 2 零钱兑换 II](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/518CoinChange2.md) - medium

### 2. Subsequence 子序列问题

##### 求解

- 一维的 dp 数组（二维的压缩版）
- 二维的 dp 数组

##### 模板：一维dp（二维 dp 压缩）

```cpp
int n = array.length;
int[] dp = new int[n];
for (int i = 1; i < n; i++) {
    for (int j = 0; j < i; j++) {
        dp[i] = 最值(dp[i], dp[j] + ...)
    }
}
```

##### 模板：二维dp

```cpp
int n = arr.length;
int[][] dp = new dp[n][n];
for (int i = 0; i < n; i++) {
    for (int j = 0; j < n; j++) {
        if (arr[i] == arr[j]) 
            dp[i][j] = dp[i][j] + ...
        else
            dp[i][j] = 最值(...)
    }
}
```

##### 例题

- LCS：[1143. Longest Common Subsequence 最长公共子序列](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/1143LongestCommonSubsequence.md) - medium
- 编辑距离：[72. Edit Distance 编辑距离](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/72EditDistance.md) - hard
- LCS：[516. Longest Palindromic Subsequence 最长回文子序列](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/516LongestPalindromicSubsequence.md) - medium
- 一维 dp：[53. Maximum Subarray 最大子序和](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/53MaximumSubarray.md) - easy

### 3. State Machine 状态机

##### 求解：
- `dp[x][y][z]` 的含义就是：今天是第 x 天，至今最多进行 y 次交易，我现在z(持有or未持有)着股票

##### 模板：一维dp（二维 dp 压缩）

```cpp
// base case：
dp[-1][k][0] = dp[i][0][0] = 0
dp[-1][k][1] = dp[i][0][1] = -infinity
// 状态转移方程：
dp[i][k][0] = max(dp[i-1][k][0], dp[i-1][k][1] + prices[i])
dp[i][k][1] = max(dp[i-1][k][1], dp[i-1][k-1][0] - prices[i])
```

##### 例题
- [121. Best Time to Buy and Sell Stock 买卖股票的最佳时机](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/121BestTimetoBuyandSellStock.md) - easy
- [122. Best Time to Buy and Sell Stock II 买卖股票的最佳时机 II](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/122BestTimetoBuyandSellStockII.md) - easy
- [123. Best Time to Buy and Sell Stock III 买卖股票的最佳时机 III](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/123BestTimetoBuyandSellStockIII.md) - hard
- [188. Best Time to Buy and Sell Stock IV 买卖股票的最佳时机 IV](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/188BestTimetoBuyandSellStockIV.md) - hard
- [309. Best Time to Buy and Sell Stock with Cooldown 最佳买卖股票时机含冷冻期](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/309BestTimetoBuyandSellStockwithCooldown.md) - medium
- [714. Best Time to Buy and Sell Stock with Transaction Fee 买卖股票的最佳时机含手续费](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/714BestTimetoBuyandSellStockwithTransactionFee.md) - medium

### 3. Fibonacci Numbers，斐波那契数列，6个题

- [70. Climbing Stairs 爬楼梯](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/70ClimbingStairs.md) - easy

Fibonacci numbers，斐波那契数列问题Staircase，爬楼梯问题Number factors，分解因子问题Minimum jumps to reach the end，蛙跳最小步数问题Minimum jumps with fee，蛙跳带有代价的问题House thief，偷房子问题

### 4. Palindromic Subsequence，回文子系列，5个题

Longest Palindromic Subsequence，最长回文子序列Longest Palindromic Substring，最长回文子字符串Count of Palindromic Substrings，最长子字符串的个数问题Minimum Deletions in a String to make it a Palindrome，怎么删掉最少字符构成回文Palindromic Partitioning，怎么分配字符，形成回文

### 5. Longest Common Substring，最长子字符串系列，13个题

Longest Common Substring，最长相同子串Longest Common Subsequence，最长相同子序列Minimum Deletions & Insertions to Transform a String into another，字符串变换Longest Increasing Subsequence，最长上升子序列Maximum Sum Increasing Subsequence，最长上升子序列和Shortest Common Super-sequence，最短超级子序列Minimum Deletions to Make a Sequence Sorted，最少删除变换出子序列Longest Repeating Subsequence，最长重复子序列Subsequence Pattern Matching，子序列匹配Longest Bitonic Subsequence，最长字节子序列Longest Alternating Subsequence，最长交差变换子序列Edit Distance，编辑距离Strings Interleaving，交织字符串



