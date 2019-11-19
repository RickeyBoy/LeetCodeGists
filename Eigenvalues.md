# 特征根、不动点与线性递推方程


主要目的：利用特征根，通过递推关系式求通项公式

一篇非常好的讲解：[怎么用特征根法和不动点法求数列的通项公式? - 灵剑的回答 - 知乎](https://www.zhihu.com/question/51662733/answer/126920544)

本文进行一个梳理，内容包括：
1. 线性递推方程
2. 特征根原理
3. 线性齐次方程组求解
4. 非线性其次方程组求解


### 线性递推方程

$a_n+p_{k-1}a_{k-1}+p_{k-2}a_{k-2}+...p_1a_{n-k}=f(n)$
$p_0 \not= 0$: k 阶线性递推方程
$f(n)=0$: k 阶齐次线性递推方程
$f(n)\not=0$: k 阶非齐次线性递推方程

### 线性无关

对于基底（base）：$b_n^{(1)}$

```
dp[j][c] = next
0 <= j < M，代表当前的状态
0 <= c < 256，代表遇到的字符（ASCII 码）
0 <= next <= M，代表下一个状态

dp[4]['A'] = 3 表示：
当前是状态 4，如果遇到字符 A，
pat 应该转移到状态 3

dp[1]['B'] = 2 表示：
当前是状态 1，如果遇到字符 B，
pat 应该转移到状态 2
```



### 确定有限状态机的作用

有了 dp 矩阵之后，每次遇到不匹配的情况，不用回退到最开始，只需要根据 dp 数组（即转移矩阵）回退到之前的某个位置即可（即 `dp[j][txt.charAt(i)]` ）。

```c++
public int search(String txt) {
    int M = pat.length();
    int N = txt.length();
    // pat 的初始态为 0
    int j = 0;
    for (int i = 0; i < N; i++) {
        // 当前是状态 j，遇到字符 txt[i]，
        // pat 应该转移到哪个状态？
        j = dp[j][txt.charAt(i)];
        // 如果达到终止态，返回匹配开头的索引
        if (j == M) return i - M + 1;
    }
    // 没到达终止态，匹配失败
    return -1;
}
```



### 影子状态 X

本质：pat 字符串、pat[x...j] 子串拥有相同的前缀 pat[1...x]。

意义：状态 j 遇到 c 时，如果不匹配，就应该回退到状态 X。



### 如何构建 dp 数组：遍历 + 影子状态 X

当如果状态 j 遇到新的字符 c 时：

如果匹配：状态 (j,c) 应该进入下一个状态

如果不匹配：状态 (j,c) 应该回退到之前一个影子状态 X

```cpp
for 0 <= j < M: # 状态
    for 0 <= c < 256: # 字符
    	if("匹配") d[j][c] = j+1;
    	if("不匹配") d[j][c] = X;
```



### 如果找到影子状态 X：动态规划

```cpp
// 完整代码
public class KMP {
    private int[][] dp;
    private String pat;

    public KMP(String pat) {
        this.pat = pat;
        int M = pat.length();
        // dp[状态][字符] = 下个状态
        dp = new int[M][256];
        // base case
        dp[0][pat.charAt(0)] = 1;
        // 影子状态 X 初始为 0
        int X = 0;
        // 当前状态 j 从 1 开始
        for (int j = 1; j < M; j++) {
            for (int c = 0; c < 256; c++) {
                if (pat.charAt(j) == c) 
                    dp[j][c] = j + 1;
                else 
                    dp[j][c] = dp[X][c];
            }
            // 更新影子状态
            X = dp[X][pat.charAt(j)];
        }
    }

    public int search(String txt) {...}
}
```

最关键语句 ---- 影子状态的 dp 关系式：

**不好理解，一定要通过动态规划的思想去考虑**

```cpp
X = dp[X][pat.charAt(j)];
```

翻译一下：

新的影子状态 = 旧的影子状态，遇到下一个 pat 中字符时的 next 状态。

动态规划的思想：

- 如果匹配，newX = oldX + 1
- 如果不匹配，newX = oldX 之前的影子状态