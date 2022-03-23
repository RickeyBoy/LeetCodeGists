# 排序算法

|          | 时间复杂度                                            | 空间复杂度 | 稳定性 |
| -------- | ----------------------------------------------------- | ---------- | ------ |
| 冒泡排序 | $O(n^2)$                                              | $O(1)$     | 稳定   |
| 选择排序 | $O(n^2)$                                              | $O(1)$     | 不稳定 |
| 希尔排序 | $O(n^{1.3 - 2})$                                      |            | 不稳定 |
| 快速排序 | 最差为 $O(n^2)$，平均为 $O(nlogn)$，最好为 $O(nlogn)$ |            | 不稳定 |
| 堆排序   | $O(nlogn)$                                            |            | 不稳定 |



### 交换算法

方法一：

```c++
// 使用：swap(vi[i], vi[j]);

void swap(int &a, int &b) {
    int temp = a;
    a = b;
    b = temp;
}
```

方法二：

```c++
// 使用：EXCHANGE(num[j], num[j + 1])

#define EXCHANGE(num1, num2)  { num1 = num1 ^ num2;\
num2 = num1 ^ num2;\
num1 = num1 ^ num2;}
```



### 冒泡

> 稳定排序，时间复杂度 $O(n^2)$



### 选择排序

> 不稳定排序，时间复杂度 $O(n^2)$

- 每一次从待排序的数据元素中选出最小（或最大）的一个元素，存放在序列的起始位置
- 交换次数比冒泡排序少多了，由于**交换所需CPU时间 > 比较所需的CPU时间**，n值较小时，选择排序比冒泡排序快



### 希尔排序

> Shell's Sort，非稳定，时间复杂度 $O(n^{1.3 - 2})$

- 把记录按下标的一定增量分组，对每组使用直接插入排序算法排序
- 我们来看下希尔排序的基本步骤
  - 选择初始增量：shellNum = 2
  - 选择初始增量 gap=length/2
  - 每组进行插入排序
  - 缩小增量继续以 gap = gap/shellNum 的方式，这种增量选择我们可以用一个序列来表示，{n/2,(n/2)/2...1}，称为**增量序列**

- 希尔排序的增量序列的选择与证明是个数学难题，我们选择的这个增量序列是比较常用的，也是希尔建议的增量，称为希尔增量

```c++
void shellSort(int vec[])
{
    int shellNum = 2; // 通常使用的希尔增量 = 2
    // 遍历增量序列中的 gap
		for(int gap = vec.size()/shellNum ; gap>0 ; gap/=shellNum) {
        // 某个 gap 的情况下，进行插入排序
        // 每组都从第二个数字开始遍历，所以需要遍历 [gap, vec.size) 的所有数字
      	for(int i=gap;i<vec.size();++i) {
            int j=i;
            // 插入排序
            while(vec[j-gap]>vec[j]) {
                swap(num[j-gap],j);
                j=j-gap;
            }
        }
    }
}
```



### 快排

> 非稳定
>
> 时间复杂度：最差为 $O(n^2)$，平均为 $O(nlogn)$，最好为 $O(nlogn)$

```c++
int partition(vector<int> &vi, int low, int up)
{
    int pivot = vi[up];
    int i = low-1;
    for (int j = low; j < up; j++) {
      if(vi[j] <= pivot) {
        i++;
        swap(vi[i], vi[j]);
      }
    }
    swap(vi[i+1], vi[up]);
    return i+1;
}

void quickSort(vector<int> &vi, int low, int up)
{
    if(low < up) {
        int mid = partition(vi, low, up);
        quickSort(vi, low, mid-1);
        quickSort(vi, mid+1, up);
    }
}
```



### 堆排序

> 非稳定，时间复杂度 $O(nlogn)$

- 堆（二叉堆、优先队列）：https://github.com/RickeyBoy/LeetCodeGists/blob/master/algorithm/Priority_Queue.md
- 堆排序：构建大顶堆($O(n)$)，每次取堆顶($O(1)$)后，删除堆顶($O(logn)$)并更新堆。