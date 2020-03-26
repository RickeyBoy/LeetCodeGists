### 65. Valid Number

验证给定的字符串是否可以解释为十进制数字。

例如:

"0" => true
" 0.1 " => true
"abc" => false
"1 a" => false
"2e10" => true
" -90e3   " => true
" 1e" => false
"e3" => false
" 6e-1" => true
" 99e2.5 " => false
"53.5e93" => true
" --6 " => false
"-+3" => false
"95a54e53" => false

说明: 我们有意将问题陈述地比较模糊。在实现代码之前，你应当事先思考所有可能的情况。这里给出一份可能存在于有效十进制数字中的字符列表：
```
数字 0-9
指数 - "e"
正/负号 - "+"/"-"
小数点 - "."
当然，在输入中，这些字符的上下文也很重要。
```

### 解法：状态转移方程

```cpp
class Solution {
public:
    // 状态
    int state;
    // -1：错误，0：空格，1：符号，2：数字，3：小数点，4：e
    int action;
    // 状态转移方程
    vector<vector<int>> transfer = {{ 0, 1, 6, 2,-1,-1},
                                    {-1,-1, 6, 2,-1,-1},
                                    {-1,-1, 3,-1,-1,-1},
                                    { 8,-1, 3,-1, 4,-1},
                                    {-1, 7, 5,-1,-1,-1},
                                    { 8,-1, 5,-1,-1,-1},
                                    { 8,-1, 6, 3, 4,-1},
                                    {-1,-1, 5,-1,-1,-1},
                                    { 8,-1,-1,-1,-1,-1}};
    // 结果出口
    vector<int> finals = {0,0,0,1,0,1,1,0,1};
    bool isNumber(string s) {
        state = 0;
        for(int i=0;i<s.size();i++) {
            state = next(state, getAct(s[i]));
            if (state<0) return false;
        }
        return finals[state];
    }
    // 根据上一步 state 和 action 计算下一步的 state
    int next(int state, int action) {
        return transfer[state][action];
    }
    // 根据字符确定对应的 action
    int getAct(char c) {
        if (c==' ') return 0;
        else if (c=='+'||c=='-') return 1;
        else if (c=='.') return 3;
        else if (c=='e') return 4;
        else if (c>='0'&&c<='9') return 2;
        else return 5;
    }
};
```
