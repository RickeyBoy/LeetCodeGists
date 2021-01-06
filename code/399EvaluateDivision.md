### [399. 除法求值](https://leetcode-cn.com/problems/evaluate-division/)

给你一个变量对数组 equations 和一个实数值数组 values 作为已知条件，其中 equations[i] = [Ai, Bi] 和 values[i] 共同表示等式 Ai / Bi = values[i] 。每个 Ai 或 Bi 是一个表示单个变量的字符串。

另有一些以数组 queries 表示的问题，其中 queries[j] = [Cj, Dj] 表示第 j 个问题，请你根据已知条件找出 Cj / Dj = ? 的结果作为答案。

返回 所有问题的答案 。如果存在某个无法确定的答案，则用 -1.0 替代这个答案。

 

注意：输入总是有效的。你可以假设除法运算中不会出现除数为 0 的情况，且不存在任何矛盾的结果。

 

示例 1：
```
输入：equations = [["a","b"],["b","c"]], values = [2.0,3.0], queries = [["a","c"],["b","a"],["a","e"],["a","a"],["x","x"]]
输出：[6.00000,0.50000,-1.00000,1.00000,-1.00000]
解释：
条件：a / b = 2.0, b / c = 3.0
问题：a / c = ?, b / a = ?, a / e = ?, a / a = ?, x / x = ?
结果：[6.0, 0.5, -1.0, 1.0, -1.0 ]
```
示例 2：
```
输入：equations = [["a","b"],["b","c"],["bc","cd"]], values = [1.5,2.5,5.0], queries = [["a","c"],["c","b"],["bc","cd"],["cd","bc"]]
输出：[3.75000,0.40000,5.00000,0.20000]
```
示例 3：
```
输入：equations = [["a","b"]], values = [0.5], queries = [["a","b"],["b","a"],["a","c"],["x","y"]]
输出：[0.50000,2.00000,-1.00000,-1.00000]
```

提示：
```
1 <= equations.length <= 20
equations[i].length == 2
1 <= Ai.length, Bi.length <= 5
values.length == equations.length
0.0 < values[i] <= 20.0
1 <= queries.length <= 20
queries[i].length == 2
1 <= Cj.length, Dj.length <= 5
Ai, Bi, Cj, Dj 由小写英文字母与数字组成
```

### 解法：加权并查集

```cpp
class Solution {
public:
    // vector<int> parents == 记录父节点
    // vector<double> weight == 节点到根节点的权重
    int find(vector<int>& parents, vector<double>& weight, int x) {
        if (x!=parents[x])  {
            int p = parents[x]; // 父节点
            int root = find(parents, weight, p); // 根节点
            weight[x] = weight[x] * weight[p]; // 更新权重
            parents[x] = root; // 顺带路径压缩
        }
        return parents[x];
    }
    void unionSet(vector<int>& parents, vector<double>& weight, int x, int y, double w) {
        int xx = find(parents, weight, x);
        int yy = find(parents, weight, y);
        parents[xx] = yy; // x 根节点指向 y 根节点
        weight[xx] = w * weight[y] / weight[x]; // 更新 xx 的 weight
    }
    vector<double> calcEquation(vector<vector<string>>& equations, vector<double>& values, vector<vector<string>>& queries) {
        int num_vars = 0; // 变量个数
        unordered_map<string, int> vars; // 变量对应的下标序号
        int n = equations.size();
        // 统计变量情况，将变量节点化
        for (int i = 0; i < n; i++) {
            if (vars.count(equations[i][0]) == 0) {
                vars[equations[i][0]] = num_vars++;
            }
            if (vars.count(equations[i][1]) == 0) {
                vars[equations[i][1]] = num_vars++;
            }
        }
        // 开始加权并查集
        vector<int> parents(num_vars);
        vector<double> weight(num_vars, 1.0);
        // 初始化
        for (int i = 0; i < num_vars; i++) {
            parents[i] = i;
        }
        // 构建
        for (int i = 0; i < n; i++) {
            // 将 equations 中的边依次加入
            int va = vars[equations[i][0]], vb = vars[equations[i][1]];
            unionSet(parents, weight, va, vb, values[i]);
        }
        // 结果
        vector<double> result;
        for (auto q: queries) {
            double cur = -1.0;
            // 答案算式的两个节点存在
            if (vars.find(q[0]) != vars.end() && vars.find(q[1]) != vars.end()) {
                int ia = vars[q[0]], ib = vars[q[1]];
                int fa = find(parents, weight, ia), fb = find(parents, weight, ib);
                if (fa == fb) {
                    cur = weight[ia] / weight[ib];
                }
            }
            result.push_back(cur);
        }
        return result;
    }
};
```
