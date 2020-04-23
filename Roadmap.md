# Rickey's Roadmap

> 参考链接：[LeetCode按照怎样的顺序来刷题比较好？ - 知乎]
(https://www.zhihu.com/question/36738189/answer/908664455)

## TODO
1. 按照这个顺序再刷题
2. 每个类型应该有原理 + 方法论 + 模板 + 题目分析 + 例题合集

## 基础类型

### 1. Pattern: Sliding window，滑动窗口类型

##### 分类

* 固定窗口大小
* 可变窗口，求解最大or最小的满足条件的窗口

##### 求解

* 固定窗口：同时移动左右指针，保证窗口宽度一定
* 可变窗口：分别移动左右指针
* 移动后需要及时更新状态位、最优解等

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

- [438. Find All Anagrams in a String 找到字符串中所有字母异位词](https://github.com/RickeyBoy/LeetCodeGists/blob/master/438FindAllAnagramsinaString.md) - medium

- [76. Minimum Window Substring 最小覆盖子串](https://github.com/RickeyBoy/LeetCodeGists/blob/master/76MinimumWindowSubstring.md) - hard

##### 参考资料

- [labuladong - 滑动窗口](https://mp.weixin.qq.com/s/ioKXTMZufDECBUwRRp3zaA)

---

https://juejin.im/post/5cccc9d1f265da0384129e5f

掘金：438、76、159、340、3、567、992、424、239、480

经典题目：Maximum Sum Subarray of Size K (easy)Smallest Subarray with a given sum (easy)Longest Substring with K Distinct Characters (medium)Fruits into Baskets (medium)No-repeat Substring (hard)Longest Substring with Same Letters after Replacement (hard)Longest Subarray with Ones after Replacement (hard)

### 2. Pattern: two points, 双指针类型

经典题目：Pair with Target Sum (easy)Remove Duplicates (easy)Squaring a Sorted Array (easy)Triplet Sum to Zero (medium)Triplet Sum Close to Target (medium)Triplets with Smaller Sum (medium)Subarrays with Product Less than a Target (medium)Dutch National Flag Problem (medium)

### 3. Pattern: Fast & Slow pointers, 快慢指针类型

经典题目：

LinkedList Cycle (easy)

Start of LinkedList Cycle (medium)

Happy Number (medium)

Middle of the LinkedList (easy)

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

### 7. Pattern: Tree Breadth First Search，树上的BFS

Binary Tree Level Order Traversal (easy)Reverse Level Order Traversal (easy)Zigzag Traversal (medium)Level Averages in a Binary Tree (easy)Minimum Depth of a Binary Tree (easy)Level Order Successor (easy)Connect Level Order Siblings (medium)

### 8. Pattern: Tree Depth First Search，树上的DFS

Binary Tree Path Sum (easy)All Paths for a Sum (medium)Sum of Path Numbers (medium)Path With Given Sequence (medium)Count Paths for a Sum (medium)

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

### 14. Pattern: 0/1 Knapsack (Dynamic Programming)，0/1背包类型

0/1 Knapsack (medium)

Equal Subset Sum Partition (medium)

Subset Sum (medium)

Minimum Subset Sum Difference (hard)

### 15. Pattern: Topological Sort (Graph)，拓扑排序类型

Topological Sort (medium)Tasks Scheduling (medium)Tasks Scheduling Order (medium)All Tasks Scheduling Orders (hard)Alien Dictionary (hard)

## 动态规划

### 1. 0/1 Knapsack, 0/1背包，6个题

0/1 Knapsack，0/1背包问题Equal Subset Sum Partition，相等子集划分问题Subset Sum，子集和问题Minimum Subset Sum Difference，子集和的最小差问题Count of Subset Sum，相等子集和的个数问题Target Sum，寻找目标和的问题

### 2. Unbounded Knapsack，无限背包，5个题

Unbounded Knapsack，无限背包

Rod Cutting，切钢条问题

Coin Change，换硬币问题

Minimum Coin Change，凑齐每个数需要的最少硬币问题

Maximum Ribbon Cut，丝带的最大值切法

### 3. Fibonacci Numbers，斐波那契数列，6个题

Fibonacci numbers，斐波那契数列问题Staircase，爬楼梯问题Number factors，分解因子问题Minimum jumps to reach the end，蛙跳最小步数问题Minimum jumps with fee，蛙跳带有代价的问题House thief，偷房子问题

### 4. Palindromic Subsequence，回文子系列，5个题

Longest Palindromic Subsequence，最长回文子序列Longest Palindromic Substring，最长回文子字符串Count of Palindromic Substrings，最长子字符串的个数问题Minimum Deletions in a String to make it a Palindrome，怎么删掉最少字符构成回文Palindromic Partitioning，怎么分配字符，形成回文

### 5. Longest Common Substring，最长子字符串系列，13个题

Longest Common Substring，最长相同子串Longest Common Subsequence，最长相同子序列Minimum Deletions & Insertions to Transform a String into another，字符串变换Longest Increasing Subsequence，最长上升子序列Maximum Sum Increasing Subsequence，最长上升子序列和Shortest Common Super-sequence，最短超级子序列Minimum Deletions to Make a Sequence Sorted，最少删除变换出子序列Longest Repeating Subsequence，最长重复子序列Subsequence Pattern Matching，子序列匹配Longest Bitonic Subsequence，最长字节子序列Longest Alternating Subsequence，最长交差变换子序列Edit Distance，编辑距离Strings Interleaving，交织字符串




