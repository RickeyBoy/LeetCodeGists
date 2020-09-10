### 40. 组合总和 II

给定一个数组 candidates 和一个目标数 target ，找出 candidates 中所有可以使数字和为 target 的组合。

candidates 中的每个数字在每个组合中只能使用一次。

说明：

所有数字（包括目标数）都是正整数。
解集不能包含重复的组合。 
示例 1:
```
输入: candidates = [10,1,2,7,6,1,5], target = 8,
所求解集为:
[
  [1, 7],
  [1, 2, 5],
  [2, 6],
  [1, 1, 6]
]
```
示例 2:
```
输入: candidates = [2,5,2,1,2], target = 5,
所求解集为:
[
  [1,2,2],
  [5]
]
```



### 解法：DFS 回溯 + 排序剪枝


```cpp
class Solution {
public:
    // 当前尝试的 index、全数组、dfs 已选数字集合、目标数、所有结果
    void dfs(int index, vector<int>& candidates, vector<int>& combine, int target, vector<vector<int>>& ans) {
        int newTarget = target - candidates[index];
        if (newTarget<0) {
            // 超过了，终止
            return; 
        } else if (newTarget == 0) {
            // 完成目标，加入 ans 中
            combine.push_back(candidates[index]);
            ans.push_back(combine);
            combine.pop_back();
        } else {
            // 选中当前节点，继续 dfs
            combine.push_back(candidates[index]);
            for (int i=index+1;i<candidates.size();i++) {
                if (newTarget - candidates[i]<0) { 
                    // 超过了，剪支
                    break;
                } 
                if (i>index+1 && candidates[i]==candidates[i-1]) continue; // 相同数字 dfs 跳过
                // 深度搜索
                dfs(i, candidates, combine, newTarget, ans);
            }
            // 回溯
            combine.pop_back();
        }
    }
    vector<vector<int>> combinationSum2(vector<int>& candidates, int target) {
        sort(candidates.begin(), candidates.end());
        vector<vector<int>> ans;
        vector<int> combine;
        for (int i=0;i<candidates.size();i++) {
            if (i>0 && candidates[i]==candidates[i-1]) continue; // 相同数字 dfs 跳过
            dfs(i, candidates, combine, target, ans);
        }
        return ans;
    }
};
```

