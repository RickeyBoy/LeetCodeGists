### 79. Word Search

给定一个二维网格和一个单词，找出该单词是否存在于网格中。

单词必须按照字母顺序，通过相邻的单元格内的字母构成，其中“相邻”单元格是那些水平相邻或垂直相邻的单元格。同一个单元格内的字母不允许被重复使用。

示例:
```
board =
[
  ['A','B','C','E'],
  ['S','F','C','S'],
  ['A','D','E','E']
]

给定 word = "ABCCED", 返回 true.
给定 word = "SEE", 返回 true.
给定 word = "ABCB", 返回 false.
```

### 解法：回溯

```cpp
class Solution {
public:
    bool exist(vector<vector<char>>& board, string word) {
        if(word.size()==0) return true;
        if(board.size()==0 || board[0].size()==0) return false;
        for (int i=0;i<board.size();i++) {
            for (int j=0;j<board[0].size();j++) {
                if(findWord(board,i,j,word,0)) return true;
            }
        }
        return false;
    }
    bool findWord(vector<vector<char>>& board, int x, int y, string word, int i) {
        if(i==word.size()) return true;
        char memo = board[x][y];
        board[x][y] = '_'; // 标记：已经被使用过
        char c = word[i];
        if(i==0) {
            if(memo==c&&findWord(board,x,y,word,i+1)) return true;
        } else {
            if(x>0&&board[x-1][y]==c) {
                if(findWord(board,x-1,y,word,i+1)) return true;
            }
            if(y>0&&board[x][y-1]==c) {
                if(findWord(board,x,y-1,word,i+1)) return true;
            } 
            if(x<board.size()-1&&board[x+1][y]==c) {
                if(findWord(board,x+1,y,word,i+1)) return true;
            } 
            if(y<board[0].size()-1&&board[x][y+1]==c) {
                if(findWord(board,x,y+1,word,i+1)) return true;
            }
        }
        board[x][y] = memo; //回溯
        return false;
    }
};
```
