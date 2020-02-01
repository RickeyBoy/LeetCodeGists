### 6. ZigZag Conversion

将一个给定字符串根据给定的行数，以从上往下、从左到右进行 Z 字形排列。

比如输入字符串为 "LEETCODEISHIRING" 行数为 3 时，排列如下：
```
L   C   I   R
E T O E S I I G
E   D   H   N
```
之后，你的输出需要从左往右逐行读取，产生出一个新的字符串，比如："LCIRETOESIIGEDHN"。

请你实现这个将字符串进行指定行数变换的函数：
```
string convert(string s, int numRows);
```
示例 1:
```
输入: s = "LEETCODEISHIRING", numRows = 3
输出: "LCIRETOESIIGEDHN"
```
示例 2:
```
输入: s = "LEETCODEISHIRING", numRows = 4
输出: "LDREOEIIECIHNTSG"
```
解释:
```
L     D     R
E   O E   I I
E C   I H   N
T     S     G
```

### 解法：模拟过程

```cpp
class Solution {
public:
    string convert(string s, int numRows) {
        if(numRows==1) return s;
        vector<string> loader = vector(numRows, string(""));
        int adder = 1, row = 0, i = 0;
        while(i<s.size()) {
            loader[row]+=s[i];
            i++;
            row+=adder;
            // 实现 z 字形输出
            if(row==0) adder=1;
            else if(row==numRows-1) adder=-1;
        }
        string result="";
        for(int j=0;j<numRows;j++) {
            result+=loader[j];
        }
        return result;
    }
};
```