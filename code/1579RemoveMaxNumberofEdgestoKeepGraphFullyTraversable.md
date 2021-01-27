### [1579. 保证图可完全遍历](https://leetcode-cn.com/problems/remove-max-number-of-edges-to-keep-graph-fully-traversable/)

Alice 和 Bob 共有一个无向图，其中包含 n 个节点和 3  种类型的边：

类型 1：只能由 Alice 遍历。
类型 2：只能由 Bob 遍历。
类型 3：Alice 和 Bob 都可以遍历。
给你一个数组 edges ，其中 edges[i] = [typei, ui, vi] 表示节点 ui 和 vi 之间存在类型为 typei 的双向边。请你在保证图仍能够被 Alice和 Bob 完全遍历的前提下，找出可以删除的最大边数。如果从任何节点开始，Alice 和 Bob 都可以到达所有其他节点，则认为图是可以完全遍历的。

返回可以删除的最大边数，如果 Alice 和 Bob 无法完全遍历图，则返回 -1 。

示例 1：
```
输入：n = 4, edges = [[3,1,2],[3,2,3],[1,1,3],[1,2,4],[1,1,2],[2,3,4]]
输出：2
解释：如果删除 [1,1,2] 和 [1,1,3] 这两条边，Alice 和 Bob 仍然可以完全遍历这个图。再删除任何其他的边都无法保证图可以完全遍历。所以可以删除的最大边数是 2 。
```


### 解法：并查集

```cpp
class Solution {
public:
    // 并查集模板
    vector<int> Alice;
    vector<int> Bob;
    void UnionFind(int totalNum, vector<int> &parents) {
        parents = vector(totalNum,0);
        for(int i=0;i<totalNum;i++) {
            parents[i]=i;
        }
    }
    int find(int x, vector<int> &parents) {
        if (x!=parents[x]) parents[x]=find(parents[x], parents); //顺手路径压缩
        return parents[x];
    }
    void unionSet(int x, int y, vector<int> &parents) {
        int xx = find(x, parents);
        int yy = find(y, parents);
        if (xx==yy) return;
        parents[xx] = yy;
    }
    // 主函数
    int maxNumEdgesToRemove(int n, vector<vector<int>>& edges) {
        UnionFind(n+1, Alice);
        UnionFind(n+1, Bob);
        int result = 0;
        // 统计 type3 中可以删除的边
        for (vector<int> edge : edges) {
            if (edge[0]==3) {
                if (find(edge[1], Alice) == find(edge[2], Alice) && find(edge[1], Bob) == find(edge[2], Bob)) result++; // Alice 和 Bob 都可以连通，这条边是多余的，可以删除
                else {
                    unionSet(edge[1], edge[2], Alice);
                    unionSet(edge[1], edge[2], Bob);
                }
            }
        }
        // 统计 type1、2 中可以删除的边
        for (vector<int> edge : edges) {
            if (edge[0]==1) {
                if (find(edge[1], Alice) == find(edge[2], Alice)) result++; // Alice 可以连通，重复的边，可以删除
                else {
                    unionSet(edge[1], edge[2], Alice);
                }
            } else if (edge[0]==2) {
                if (find(edge[1], Bob) == find(edge[2], Bob)) result++; // Bob 可以连通，重复的边，可以删除
                else {
                    unionSet(edge[1], edge[2], Bob);
                }
            }
        }
        // 判断整体的连接性
        int AliceRoot = find(1, Alice);
        int BobRoot = find(1, Bob);
        for (int i = 2; i<= n; i++) {
            if (find(i, Alice) != AliceRoot) return -1;
            if (find(i, Bob) != BobRoot) return -1;
        }
        return result;
    }
};
```
