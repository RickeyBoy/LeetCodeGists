# Rickey's Roadmap





## 数据结构

### 0. 常见操作

https://github.com/RickeyBoy/LeetCodeGists/blob/master/dataStructure/Basic.md

### 1. 链表

https://github.com/RickeyBoy/LeetCodeGists/blob/master/dataStructure/ListNode.md

### 2. 二叉树

https://github.com/RickeyBoy/LeetCodeGists/blob/master/dataStructure/BinaryTree.md

### 3. 二叉堆

https://github.com/RickeyBoy/LeetCodeGists/blob/master/dataStructure/BinaryHeap.md

### 4. 并查集

https://github.com/RickeyBoy/LeetCodeGists/blob/master/dataStructure/UnionFind.md

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

- [3. Longest Substring Without Repeating Characters 无重复字符的最长子串](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/3LongestSubstringWithoutRepeatingCharacters.md) - medium
- [76. Minimum Window Substring 最小覆盖子串](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/76MinimumWindowSubstring.md) - hard
- [567. Permutation in String 字符串的排列](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/567PermutationinString.md) - medium
- [992. Subarrays with K Different Integers K 个不同整数的子数组](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/992SubarrayswithKDifferentIntegers.md) - hard
- [438. Find All Anagrams in a String 找到字符串中所有字母异位词](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/438FindAllAnagramsinaString.md) - medium

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

##### 模板

```cpp
class Solution {
public:
    int search(vector<int>& nums, int target) {
        int left = 0;
        int right = nums.size()-1;
        while (right >= left) {
            int mid = (right - left) / 2 + left;
            if (nums[mid]==target) {
                return mid;
            } else if (nums[mid]<target) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }
        return -1;
    }
};
```

##### 例题

- [704. binary Search 二分查找](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/704binarySearch.md) - easy
- [69. Sqrt(x) x 的平方根](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/69Sqrt(x).md) - easy
- [278. First Bad Version 第一个错误的版本](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/278FirstBadVersion.md) - easy
- [33. Search in Rotated Sorted Array 搜索旋转排序数组](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/33SearchinRotatedSortedArray.md) - medium
- [34. Find First and Last Position of Element in Sorted Array 在排序数组中查找元素的第一个和最后一个位置](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/34FindFirstandLastPositionofElementinSortedArray.md) - medium

### 4. 深度优先搜索 DFS

##### 求解

- 定义通用 dfs 函数，函数需要拼上每一步需要的参数
- 递归调用

##### 关键字

“输出所有可能结果”

##### 例题

- [617. Merge Two Binary Trees 合并二叉树](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/617MergeTwoBinaryTrees.md) - easy
- [236. Lowest Common Ancestor of a Binary Tree 二叉树的最近公共祖先](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/236LowestCommonAncestorofaBinaryTree.md) - medium
- [301. Remove Invalid Parentheses 删除无效的括号](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/301RemoveInvalidParentheses.md) - hard

### 5. 宽度优先搜索 BFS

##### 求解：

- 定义通用 bfs 函数，函数需要拼上每一步需要的参数
- 递归调用，每一次递归都需要探索当前的所有可能
- 通常可以转化为二叉树 or 图的问题

##### 关键字

- "二叉树"、"区域（图）"

##### 例题：

- [102. Binary Tree Level Order Traversal 二叉树的层次遍历](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/102BinaryTreeLevelOrderTraversal.md) - medium
- [200. Number of Islands 岛屿数量](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/200NumberofIslands.md) - medium
- [279. Perfect Squares 完全平方数](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/279PerfectSquares.md) - medium

### 6. 回溯

##### 求解

- 标准回溯：递归 + 回溯
- 广义回溯：递归，全排列
- 维护当前进行的步骤情况

##### 关键字

- “全排列”、“全部组合”

##### 例题

- [22. Generate Parentheses 括号生成](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/22GenerateParentheses.md) - medium
- [39. Combination Sum 组合总和](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/39CombinationSum.md) - medium
- [40. Combination Sum II 组合总和 II](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/40CombinationSumII.md) - medium
- [51. N-Queens](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/51N-Queens.md) - hard
- [52. N-QueensII](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/52N-QueensII.md) - hard
- [78. Subsets 子集](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/78Subsets.md) - medium
- [79. Word Search 单词搜索](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/79WordSearch.md) - medium

**代码模板**

> 本质就是：**“做选择 → 递归 → 撤销选择”**

**N-Queens 模板**：

```cpp
class Solution {
public:
    vector<vector<string>> res;
    vector<string> board;
    unordered_set<int> cols, diag1, diag2; // 列、主对角线、次对角线

    void backtrack(int row, int n) {
        if (row == n) {
          	// 终止条件
            res.push_back(board);
            return;
        }
        for (int col = 0; col < n; ++col) {
            if (cols.count(col) || diag1.count(row - col) || diag2.count(row + col))
                continue;
            // [做选择] 放置皇后
            board[row][col] = 'Q';
            cols.insert(col);
            diag1.insert(row - col);
            diag2.insert(row + col);
          	// [递归]
            backtrack(row + 1, n);
            // [回溯] 撤销选择
            board[row][col] = '.';
            cols.erase(col);
            diag1.erase(row - col);
            diag2.erase(row + col);
        }
    }
    vector<vector<string>> solveNQueens(int n) {
        board = vector<string>(n, string(n, '.'));
        backtrack(0, n);
        return res;
    }
};
```



## 动态规划

### 0. Fibonacci Numbers 斐波那契数列 

##### 求解

- 一维线性递推公式
- 可以使用特征根

##### 例题

- [70. Climbing Stairs 爬楼梯](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/70ClimbingStairs.md) - easy
- [509. Fibonacci Number 斐波那契数](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/509FibonacciNumber.md) - easy
- [264. Ugly Number II 丑数 II](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/264UglyNumberII.md) - medium

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
  - [494. Target Sum 目标和](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/494TargetSum.md) - medium
  - [474. Ones and Zeroes 一和零](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/474OnesandZeroes.md) - medium
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
- LCS：[516. Longest Palindromic Subsequence 最长回文子序列](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/516LongestPalindromicSubsequence.md) - medium
- 编辑距离：[72. Edit Distance 编辑距离](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/72EditDistance.md) - hard

**LCS 问题模板 1143**

```cpp
class Solution {
public:
    int longestCommonSubsequence(string text1, string text2) {
        int m = text1.size();
        int n = text2.size();
        // dp[x][y] 代表 text1[1..x] 和 text2[1..y] 的 LCS 串
        vector<vector<int>> dp = vector(m+1, vector(n+1, 0));
        for (int i=1;i<=m;i++) {
            for (int j=1;j<=n;j++) {
                if (text1[i-1]==text2[j-1]) {
                    // 相同字符，在 LCS 串中
                    dp[i][j] = dp[i-1][j-1] + 1;
                } else {
                    // 不同字符，必定有一个不在 LCS 串中
                    dp[i][j] = max(dp[i-1][j],dp[i][j-1]);
                }
            }
        }
        return dp[m][n];
    }
};
```

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



## 高级类型

### 1. 字典树Trie

Todo

模板：[Trie 字典树](https://github.com/RickeyBoy/LeetCodeGists/blob/master/algorithm/Trie.md)

- [139. Word Break 单词拆分](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/139WordBreak.md) - medium
- [208. Implement Trie (Prefix Tree) 实现 Trie (前缀树)](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/208ImplementTriePrefixTree.md) - medium
- [211. Design Add and Search Words Data Structure  添加与搜索单词 - 数据结构设计](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/211DesignAddandSearchWordsDataStructure.md) - medium

TODO

### 2. 最短路算法

1. [LeetCode 743. 网络延迟时间](https://link.zhihu.com/?target=https%3A//leetcode-cn.com/problems/network-delay-time/)

### 3. 最小生成树

1. [1584. 连接所有点的最小费用](https://link.zhihu.com/?target=https%3A//leetcode-cn.com/problems/min-cost-to-connect-all-points/)

### 4. 拓扑排序

**拓扑排序是对有向无环图（DAG）中节点的一种线性排序，使得每条边 (u → v)，都满足 u 在 v 前面。**

核心思想：维护一个队列，始终保存所有入度为 0 的点，不断销毁其相关的边，看最终能否销毁完

[LeetCode 207. 课程表](https://link.zhihu.com/?target=https%3A//leetcode-cn.com/problems/course-schedule/): 解法如下

```cpp
bool canFinish(int numCourses, vector<vector<int>>& prerequisites) {
    vector<vector<int>> graph(numCourses);   // 邻接表，graph[x] = {y1, y2...} 表示 x → y
    vector<int> inDegree(numCourses, 0);     // 每个点的入度
    // Step 1: 构建图 + 统计入度
    for (auto& pre : prerequisites) {
        int to = pre[0], from = pre[1];
        graph[from].push_back(to);
        inDegree[to]++;
    }
    // Step 2: 把所有入度为 0 的点加入队列
    queue<int> q;
    for (int i = 0; i < numCourses; ++i) {
        if (inDegree[i] == 0) q.push(i);
    }
    // Step 3: BFS 拓扑排序
    int count = 0;  // 记录可以完成的课程数
    while (!q.empty()) {
        int curr = q.front(); q.pop();
        count++;
        for (int neighbor : graph[curr]) {
            inDegree[neighbor]--;
            if (inDegree[neighbor] == 0) {
                q.push(neighbor);
            }
        }
    }
    // Step 4: 如果所有课程都能完成，说明无环
    return count == numCourses;
}
```



### 5. 二叉搜索树

1. [面试题 04.06. 后继者](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/interview04_06.md) - medium



## 系列题目

### 1. 排序

https://github.com/RickeyBoy/LeetCodeGists/blob/master/series/sort.md

### 2. 回文子系列

**最长回文子序列 Longest Palindromic Substring 【区间 DP 问题】**

```c++
dp[i][j] => [i...j] 之间的最长子序列
1. if s[i] == s[j] { dp[i][j] = dp[i+1][j-1] + 2 } // 左右两边相等，LPS 可以 +1
2. else { dp[i][j] = max(dp[i+1][j], dp[i][j-1]) } // 左右两边不等，LPS 只能二选一
3. 遍历方式：i 从大到小，j 从 i 开始大到小
4. 初始化 dp[i][i] = 1
5. 可以优化到一维 dp
```

**最长回文子字符串 Longest Palindromic Substring【中心拓展法】**

```c++
// 遍历所有 idx，以 idx 为中心，尝试左右 expand
// 需要考虑【奇数、偶数】两种情况
for (int i = 0; i < s.size(); i++) {
    expand(i, i);     // 奇数回文
    expand(i, i + 1); // 偶数回文
}
```

**最长回文子字符串个数 Count of Palindromic Substrings【中心拓展法】**

```c++
同样的方法，只不过每次记录个数
```

**最长子字符串的个数问题 Minimum Deletions in a String to make it a Palindrome【DP】**

```c++
同第一种，计算最长子序列长度，然后整体长度 - 最长子序列长度
```

**回文串切割 Palindromic Partitioning【回溯法】**

> LeetCode 131: 给你一个字符串 s，请你将它**切分成多个回文子串的组合**，返回所有合法切法。

```c++
void backtrack(string& s, int start, vector<string>& path, vector<vector<string>>& res)
// start: 切割起始位置，终止条件 s.size() == start
// path: 当前已切好的部分
// 每次从 start 开始，尝试 end = start+1 到 s.size()，如果有回文，就进入下一轮 backtrack
for (int end = start; end < s.size(); ++end) {
    if (isPalindrome(s, start, end)) {
        path.push_back(s.substr(start, end - start + 1));
        backtrack(s, end + 1, path, res);
        path.pop_back();
    }
}
```

**回文串切割 II Palindromic Partitioning II【DP】**

> LeetCode 132: 将一个字符串切成最少的几段，每段都是回文子串，返回最少切割次数

```c++
1. 预处理所有回文串情况，s[i][j] = 1 or 0
2. 动态规划, dp[i] => 0...i 的最小切割段数
3. dp[x] = min(遍历0到x-1，所有 s[i][x]=1 的 dp[i]+1 )
```



### 3. TwoSum 系列

- [1. Two Sum 两数之和](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/1TwoSum.md) - easy
- [15. 3Sum 三数之和](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/15ThreeSum.md) - medium
- [16. 3Sum Closest 最接近的三数之和](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/16ThreeSumClosest.md) - medium
- [18. 4Sum 四数之和](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/184Sum.md) - medium



### 4. N 皇后问题

- [51. N-Queens](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/51N-Queens.md) - hard
- [52. N-QueensII](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/52N-QueensII.md) - hard



### 5. 股票手续费问题

- [121. Best Time to Buy and Sell Stock 买卖股票的最佳时机](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/121BestTimetoBuyandSellStock.md) - easy
- [122. Best Time to Buy and Sell Stock II 买卖股票的最佳时机 II](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/122BestTimetoBuyandSellStockII.md) - easy
- [123. Best Time to Buy and Sell Stock III 买卖股票的最佳时机 III](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/123BestTimetoBuyandSellStockIII.md) - hard
- [188. Best Time to Buy and Sell Stock IV 买卖股票的最佳时机 IV](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/188BestTimetoBuyandSellStockIV.md) - hard
- [309. Best Time to Buy and Sell Stock with Cooldown 最佳买卖股票时机含冷冻期](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/309BestTimetoBuyandSellStockwithCooldown.md) - medium
- [714. Best Time to Buy and Sell Stock with Transaction Fee 买卖股票的最佳时机含手续费](https://github.com/RickeyBoy/LeetCodeGists/blob/master/code/714BestTimetoBuyandSellStockwithTransactionFee.md) - medium



## 特殊算法





## 参考资料

[LeetCode按照怎样的顺序来刷题比较好？ - 知乎](https://www.zhihu.com/question/36738189/answer/908664455)

[ACM金牌选手整理的【LeetCode刷题顺序】 - 编程熊的文章 - 知乎](https://zhuanlan.zhihu.com/p/388470520)

[数据结构参考 - labuladong](https://labuladong.gitee.io/algo/1/)
