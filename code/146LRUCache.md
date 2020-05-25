### 146. LRU缓存机制

运用你所掌握的数据结构，设计和实现一个  LRU (最近最少使用) 缓存机制。它应该支持以下操作： 获取数据 get 和 写入数据 put 。

获取数据 get(key) - 如果密钥 (key) 存在于缓存中，则获取密钥的值（总是正数），否则返回 -1。
写入数据 put(key, value) - 如果密钥已经存在，则变更其数据值；如果密钥不存在，则插入该组「密钥/数据值」。当缓存容量达到上限时，它应该在写入新数据之前删除最久未使用的数据值，从而为新的数据值留出空间。

 

进阶:

你是否可以在 O(1) 时间复杂度内完成这两种操作？

 

示例:
```
LRUCache cache = new LRUCache( 2 /* 缓存容量 */ );

cache.put(1, 1);
cache.put(2, 2);
cache.get(1);       // 返回  1
cache.put(3, 3);    // 该操作会使得密钥 2 作废
cache.get(2);       // 返回 -1 (未找到)
cache.put(4, 4);    // 该操作会使得密钥 1 作废
cache.get(1);       // 返回 -1 (未找到)
cache.get(3);       // 返回  3
cache.get(4);       // 返回  4
```

### 解法：双向链表（pair+list） + 哈希表（pair+iterator）

```cpp
class LRUCache {
private:
    int cap;
    list<pair<int, int>> cache; // 双向链表, <前,value>::后
    unordered_map<int, list<pair<int, int>>::iterator> map; // 哈希表，指向双向链表迭代器
public:
    LRUCache(int capacity) : cap(capacity) {

    }
    
    int get(int key) {
        if(map.count(key)==0) return -1;
        auto value = *map[key];
        cache.erase(map[key]); // 根据地址移除，O(1)
        cache.push_front(value); // 将指针移到开头
        map[key]=cache.begin(); // 更新map
        return value.second;
    }
    
    void put(int key, int value) {
        if(map.count(key)==0) {
            if (cache.size() == cap) {
                // 满了，删除最后一个
                map.erase(cache.back().first);
                cache.pop_back();
            }
        } else {
            // 删除旧的
            cache.erase(map[key]);
        }
        cache.push_front({key, value});
        map[key] = cache.begin();
    }
};
```
