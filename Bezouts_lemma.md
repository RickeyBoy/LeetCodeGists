# 裴蜀定理

定义：设 a、b  是不全为零的整数，则存在整数 x、y , 使得 ax + by == gcd(a,b) .
证明：[裴蜀定理 - OI Wiki](https://oi-wiki.org/math/bezouts/)

### 欧几里得算法（辗转相除法）

利用欧几里得算法求最大公约数：
```
int gcd(int a,int b){
    return b ? gcd(b,a%b) : a;
}
```

### 拓展欧几里得算法

求裴蜀定理中使等式满足的 x、y 值，且是满足裴蜀等式的最简系数。

具体：TODO
