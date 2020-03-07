# [面试题59 - II. 队列的最大值](https://leetcode-cn.com/problems/dui-lie-de-zui-da-zhi-lcof/)

```
请定义一个队列并实现函数 max_value 得到队列里的最大值，要求函数max_value、push_back 和 pop_front 的时间复杂度都是O(1)。

若队列为空，pop_front 和 max_value 需要返回 -1

示例 1：

输入: 
["MaxQueue","push_back","push_back","max_value","pop_front","max_value"]
[[],[1],[2],[],[],[]]
输出: [null,null,null,2,1,2]
示例 2：

输入: 
["MaxQueue","pop_front","max_value"]
[[],[],[]]
输出: [null,-1,-1]
 

限制：

1 <= push_back,pop_front,max_value的总操作数 <= 10000
1 <= value <= 10^5
```

# Solution

```cpp
class MaxQueue {
public:
    MaxQueue() {

    }
    
    int max_value() {
        return m_deque.empty() ? -1 : m_deque.front();
    }
    
    void push_back(int value) {
        m_queue.push(value);

        while(!m_deque.empty() && m_deque.back() < value) {
            m_deque.pop_back();
        }

        m_deque.push_back(value);
    }
    
    int pop_front() {
        if (m_queue.empty()) {
            return -1;
        }

        int v = m_queue.front();
        m_queue.pop();

        if (v == m_deque.front()) {
            m_deque.pop_front();
        }

        return v;
    }

private:
    std::queue<int> m_queue;
    std::deque<int> m_deque;
};

/**
 * Your MaxQueue object will be instantiated and called as such:
 * MaxQueue* obj = new MaxQueue();
 * int param_1 = obj->max_value();
 * obj->push_back(value);
 * int param_3 = obj->pop_front();
 */
```
