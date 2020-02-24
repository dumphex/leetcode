# [LRU缓存机制](https://leetcode-cn.com/problems/lru-cache/)

```
运用你所掌握的数据结构，设计和实现一个  LRU (最近最少使用) 缓存机制。它应该支持以下操作： 获取数据 get 和 写入数据 put 。

获取数据 get(key) - 如果密钥 (key) 存在于缓存中，则获取密钥的值（总是正数），否则返回 -1。
写入数据 put(key, value) - 如果密钥不存在，则写入其数据值。当缓存容量达到上限时，它应该在写入新数据之前删除最近最少使用的数据值，从而为新的数据值留出空间。

进阶:

你是否可以在 O(1) 时间复杂度内完成这两种操作？

示例:

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

# Solution

```cpp
class LRUCache {
public:
    typedef struct ListNode{
        int key;
        int value;
        ListNode(int k, int v) {
            key = k;
            value = v;
        }
    }ListNode;

    LRUCache(int capacity) :m_capacity(capacity) {
        
    }
    
    int get(int key) {
        if (m_map.find(key) == m_map.end()) {
            return -1;
        }
        
        auto it = m_list.begin();
        if (it->key != key) {
            m_list.splice(m_list.begin(), m_list, m_map[key]);
            m_map[key] = m_list.begin();
        }

        //return m_map[key]->value;
        return m_list.begin()->value;
    }
    
    void put(int key, int value) {
        if (m_map.find(key) != m_map.end()) {
            // update
            m_map[key]->value = value;
            m_list.splice(m_list.begin(), m_list, m_map[key]);          
        } else {
            // add
            ListNode node(key, value);
            if (m_list.size() == m_capacity) {
                //超过容量
                m_map.erase(m_list.rbegin()->key);
                m_list.pop_back();
            }

            m_list.push_front(node);
        }
        
        m_map[key] = m_list.begin();
    }
private:
    int m_capacity;
    unordered_map<int, list<ListNode>::iterator> m_map;
    list<ListNode> m_list;
};

/**
 * Your LRUCache object will be instantiated and called as such:
 * LRUCache* obj = new LRUCache(capacity);
 * int param_1 = obj->get(key);
 * obj->put(key,value);
 */
```
