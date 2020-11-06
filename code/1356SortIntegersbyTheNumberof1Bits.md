### 1356. Sort Integers by The Number of 1 Bits

给你一个整数数组 arr 。请你将数组中的元素按照其二进制表示中数字 1 的数目升序排序。

如果存在多个数字二进制中 1 的数目相同，则必须将它们按照数值大小升序排列。

请你返回排序后的数组。

 

示例 1：
```
输入：arr = [0,1,2,3,4,5,6,7,8]
输出：[0,1,2,4,8,3,5,6,7]
解释：[0] 是唯一一个有 0 个 1 的数。
[1,2,4,8] 都有 1 个 1 。
[3,5,6] 有 2 个 1 。
[7] 有 3 个 1 。
按照 1 的个数排序得到的结果数组为 [0,1,2,4,8,3,5,6,7]
```

### 解法1：快排 + 二进制中 1 的个数

```cpp
class Solution {
public:
    vector<int> sortByBits(vector<int>& arr) {
        quickSort(arr,0,arr.size()-1);
        return arr;
    }

    int NumberOf1(int n) {
			int count = 0;
			while (n) {
				count++;
				n = (n - 1)&n;
			}
			return count;
    }

    bool compare(int low, int up) {
        int numLow = NumberOf1(low);
        int numUp = NumberOf1(up);
        if (numLow<numUp) {
            return true;
        } else if (numLow==numUp) {
            return low <= up;
        } else {
            return false;
        }
    }

    void swap(int &a, int &b) {
        int temp = a;
        a = b;
        b = temp;
    }

    int partition(vector<int> &vi, int low, int up)
    {
        int pivot = vi[up];
        int i = low-1;
        for (int j = low; j < up; j++) {
            if(compare(vi[j],pivot)) {
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
};
```