### [216. 组合总和 III](https://leetcode-cn.com/problems/combination-sum-iii/)

找出所有相加之和为 n 的 k 个数的组合。组合中只允许含有 1 - 9 的正整数，并且每种组合中不存在重复的数字。

说明：

所有数字都是正整数。
解集不能包含重复的组合。 
示例 1:
```
输入: k = 3, n = 7
输出: [[1,2,4]]
```
示例 2:
```
输入: k = 3, n = 9
输出: [[1,2,6], [1,3,5], [2,3,4]]
```



### 解法：DFS 回溯 + 剪枝


```cpp
class Solution {
public:
    // 当前尝试的 index、全数组、dfs 已选数字集合、目标数、所有结果
    void dfs(int index, vector<int>& candidates, vector<int>& combine, int target, vector<vector<int>>& ans, int k) {
        int newTarget = target - candidates[index];
        if (newTarget<0) {
            // 超过了，终止
            return; 
        } else if (newTarget == 0) {
            if (combine.size() + 1 != k) return; // 位数不符合，终止 
            // 完成目标，加入 ans 中
            combine.push_back(candidates[index]);
            ans.push_back(combine);
            combine.pop_back();
        } else if (combine.size()>=k) {
            // 位数过多，终止
            return;
        } else {
            // 选中当前节点，继续 dfs
            combine.push_back(candidates[index]);
            for (int i=index+1;i<candidates.size();i++) {
                if (newTarget - candidates[i]<0) { 
                    // 超过了，剪支
                    break;
                } 
                // 深度搜索
                dfs(i, candidates, combine, newTarget, ans, k);
            }
            // 回溯
            combine.pop_back();
        }
    }
    vector<vector<int>> combinationSum3(int k, int n) {
        vector<int> candidates = {1,2,3,4,5,6,7,8,9};
        vector<vector<int>> ans;
        vector<int> combine;
        for (int i=0;i<candidates.size();i++) {
            dfs(i, candidates, combine, n, ans, k);
        }
        return ans;
    }
};
```

