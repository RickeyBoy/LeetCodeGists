### 959. Regions Cut By Slashes

在由 1 x 1 方格组成的 N x N 网格 grid 中，每个 1 x 1 方块由 /、\ 或空格构成。这些字符会将方块划分为一些共边的区域。

（请注意，反斜杠字符是转义的，因此 \ 用 "\\" 表示。）。

返回区域的数目。

 

示例 1：

输入：
```
[
  " /",
  "/ "
]
```
输出：2
```
解释：2x2 网格如下：
```
示例 2：

输入：
```
[
  " /",
  "  "
]
```
输出：1
```
解释：2x2 网格如下：
```
示例 3：

输入：
```
[
  "\\/",
  "/\\"
]
```
输出：4
```
解释：（回想一下，因为 \ 字符是转义的，所以 "\\/" 表示 \/，而 "/\\" 表示 /\。）
2x2 网格如下：
```
示例 4：

输入：
```
[
  "/\\",
  "\\/"
]
```
输出：5
```
解释：（回想一下，因为 \ 字符是转义的，所以 "/\\" 表示 /\，而 "\\/" 表示 \/。）
2x2 网格如下：
```
示例 5：
```
输入：
[
  "//",
  "/ "
]
```
输出：3
```
解释：2x2 网格如下：
```
 

提示：
```
1 <= grid.length == grid[0].length <= 30
grid[i][j] 是 '/'、'\'、或 ' '。
```


### 解法：并查集

并查集不需要启发式，因为肯定是新遍历到的点的 size 更小
todo：可以不需要 map 二维数组，直接使用一个 vector parent 就行了

```cpp
class UnionFind {
private:
    vector<int> parents;
public:
    UnionFind(int totalNum) {
        parents = vector(totalNum,0);
        for(int i=0;i<totalNum;i++) {
            parents[i]=i;
        }
    }
    
    int find(int x) {
        if (x!=parents[x]) parents[x]=find(parents[x]); //顺手路径压缩
        return parents[x];
    }
    
    int unionSet(int x, int y) {
        int xx = find(x);
        int yy = find(y);
        if (xx==yy) return 0;
        parents[yy] = xx;
        return 1;
    }
};

class Solution {
public:
    vector<vector<int>> map;
    int regionsBySlashes(vector<string>& grid) {
        int n = grid.size();
        if(n==0) return 0;
        map = vector(3*n, vector(3*n,0));
        for(int i=0;i<n;i++) {
            for (int j=0;j<n;j++) {
                createMap(grid[i][j], i*3, j*3);
            }
        }
        // union find
        int result = 0;
        int N = 3*n;
        UnionFind uf = UnionFind(N*N);
        for(int i=0;i<N;i++) {
            for(int j=0;j<N;j++) {
                if(map[i][j]==1) continue;
                result++;
                if(i>0&&map[i-1][j]==0) {
                    int temp = uf.unionSet(N*(i-1)+j,N*i+j);
                    result-=temp;
                }
                if(j>0&&map[i][j-1]==0) {
                    int temp = uf.unionSet(N*i+j-1,N*i+j);
                    result-=temp;
                }
            }
        }
        return result;
    }

    void createMap(char c, int x, int y) {
        if (c=='/') {
            map[x+2][y]=1;
            map[x+1][y+1]=1;
            map[x][y+2]=1;
        } else if (c=='\\') {
            map[x][y]=1;
            map[x+1][y+1]=1;
            map[x+2][y+2]=1;
        }
    }
};
```
