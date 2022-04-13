#### [380. O(1) 时间插入、删除和获取随机元素](https://leetcode-cn.com/problems/insert-delete-getrandom-o1/)

实现RandomizedSet 类：

RandomizedSet() 初始化 RandomizedSet 对象
bool insert(int val) 当元素 val 不存在时，向集合中插入该项，并返回 true ；否则，返回 false 。
bool remove(int val) 当元素 val 存在时，从集合中移除该项，并返回 true ；否则，返回 false 。
int getRandom() 随机返回现有集合中的一项（测试用例保证调用此方法时集合中至少存在一个元素）。每个元素应该有 相同的概率 被返回。
你必须实现类的所有函数，并满足每个函数的 平均 时间复杂度为 O(1) 。

### 解法

```cpp
class RandomizedSet {
private:
    unordered_map <int, int> maps; // maps[x]=y，值为x的数字的index=y
    vector <int> nums;
public:
    RandomizedSet() {
        srand((unsigned)time(NULL));
    }
    
    bool insert(int val) {
        if (!maps.count(val)) {
            // 插入到 nums 最后一个
            nums.push_back(val);
            maps[val]=nums.size()-1;
            return true;
        } else {
            return false;
        }
    }
    
    bool remove(int val) {
        if (!maps.count(val)) {
            return false;
        } else {
            // 将 nums 最后一个数字和要删除的数字交换
            int lastNum = nums[nums.size()-1];
            nums[maps[val]] = lastNum;
            maps[lastNum] = maps[val];
            nums.pop_back();
            maps.erase(val);
            return true;
        }
    }
    
    int getRandom() {
        int randomIndex = rand()%nums.size();
        return nums[randomIndex];
    }
};

/**
 * Your RandomizedSet object will be instantiated and called as such:
 * RandomizedSet* obj = new RandomizedSet();
 * bool param_1 = obj->insert(val);
 * bool param_2 = obj->remove(val);
 * int param_3 = obj->getRandom();
 */
```
