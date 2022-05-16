# 快速幂

快速幂，二进制取幂（Binary Exponentiation，也称平方法），是一个在 $O(log(n))$ 的时间内计算 $a^n$ 的小技巧，而暴力的计算需要 $O(n)$ 的时间。

一篇非常好的讲解文章：[快速幂 - OI Wiki](https://oi-wiki.org/math/quick-pow/)

### 核心

- $a^{b+c}=a^b*a^c$
- 利用二进制将 n 分割为更小的任务

### 非递归代码

```c++
long long binpow(long long a, long long b) {
  long long res = 1;
  while (b > 0) {
    if (b & 1) res = res * a;
    a = a * a;
    b >>= 1;
  }
  return res;
}
```
