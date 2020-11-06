# 二进制中 1 的个数

### 方法 1： 循环 + 除法

- 时间复杂度高（O(n)，n 为二进制数的位数）
- 除法效率低
- 只能处理正数

```cpp
int  NumberOf(int n) {
		int count = 0;
		while (n) {
			if (n % 2 == 1)
				count++;
			n /= 2;
		}
		return count;
}
```

### 方法 2：循环 + 位运算 + 右移

- 每次统计最右边的位数是不是 1，然后右移一位
- 时间复杂度高（O(n)，n 为二进制数的位数）
- 位运算效率高于除法
- 此方法可能引起死循环，例如输入的 n=0x8000000，右移最终会得到 0xFFFFFFF

```cpp
int NumberOf1(int n) {
		int count = 0;
		while (n) {
			if (n & 1) count++;
			n=n>>1;
		}
		return count;
}
```

### 方法 3：循环 + 位运算 + 左移

- 每次统计最左边的位数是不是 1，然后左移一位
- 时间复杂度更高（O(32)，32 > n 为二进制数的位数）
- 位运算效率高于除法
- 此方法不会死循环

```cpp
int NumberOf1(int n) {
		unsigned flag = 1;
		int count = 0;
		while (flag) // 这个循环次数等于整数二进制的位数，32位的整数要循环32次
		{
			if (n&1)
				count++;
			flag = flag << 1;
		}
}
```

### 方法 4：位移运算

- 效率最高（O(m)，m 为二进制数中 1 的个数）

```cpp
int NumberOf1(int n) {
		int count = 0;
		while (n) {
			count++;
			n = (n - 1)&n;
		}
		return count;
}
```