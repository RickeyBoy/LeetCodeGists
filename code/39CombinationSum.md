### 39. 组合总和

给定一个无重复元素的数组 candidates 和一个目标数 target ，找出 candidates 中所有可以使数字和为 target 的组合。

candidates 中的数字可以无限制重复被选取。

说明：

所有数字（包括 target）都是正整数。
解集不能包含重复的组合。 

示例 1：
```
输入：candidates = [2,3,6,7], target = 7,
所求解集为：
[
  [7],
  [2,2,3]
]
```
示例 2：
```
输入：candidates = [2,3,5], target = 8,
所求解集为：
[
  [2,2,2,2],
  [2,3,3],
  [3,5]
]
```

提示：
```
1 <= candidates.length <= 30
1 <= candidates[i] <= 200
candidate 中的每个元素都是独一无二的。
1 <= target <= 500
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
            for (int i=index;i<candidates.size();i++) {
                if (newTarget - candidates[i]<0) { 
                    // 超过了，剪支
                    break;
                } 
                // 深度搜索
                dfs(i, candidates, combine, newTarget, ans);
            }
            // 回溯
            combine.pop_back();
        }
    }
    vector<vector<int>> combinationSum(vector<int>& candidates, int target) {
        sort(candidates.begin(), candidates.end());
        vector<vector<int>> ans;
        vector<int> combine;
        for (int i=0;i<candidates.size();i++) {
            dfs(i, candidates, combine, target, ans);
        }
        return ans;
    }
};
```

