### [36. 有效的数独](https://leetcode-cn.com/problems/valid-sudoku/)

请你判断一个 9x9 的数独是否有效。只需要 根据以下规则 ，验证已经填入的数字是否有效即可。

数字 1-9 在每一行只能出现一次。
数字 1-9 在每一列只能出现一次。
数字 1-9 在每一个以粗实线分隔的 3x3 宫内只能出现一次。（请参考示例图）
数独部分空格内已填入了数字，空白格用 '.' 表示。

注意：

一个有效的数独（部分已被填充）不一定是可解的。
只需要根据以上规则，验证已经填入的数字是否有效即可。

### 解法：模拟遍历

- 初始化：`vector<set<int>> rows = vector(9,set<int>());`

```cpp
class Solution {
public:
    bool isValidSudoku(vector<vector<char>>& board) {
        vector<set<int>> rows = vector(9,set<int>());
        vector<set<int>> lines = vector(9,set<int>());
        vector<set<int>> squares = vector(9,set<int>());
        for (int i=0;i<9;i++) {
            for (int j=0;j<9;j++) {
                if (board[i][j] == '.') continue; // 未填充直接忽略
                int num = board[i][j] - '0';
                // 判定行合规
                if (rows[i].count(num)>0) {
                    return false;
                } else {
                    rows[i].insert(num);
                }
                // 判定列合规
                if (lines[j].count(num)>0) {
                    return false;
                } else {
                    lines[j].insert(num);
                }
                // 判定九宫格合规
                int sIndex = (i/3)*3+j/3;
                if (squares[sIndex].count(num)>0) {
                    return false;
                } else {
                    squares[sIndex].insert(num);
                }
            }
        }
        return true;
    }
};
```