# [数据流的中位数](https://leetcode-cn.com/problems/find-median-from-data-stream/)

```
中位数是有序列表中间的数。如果列表长度是偶数，中位数则是中间两个数的平均值。

例如，

[2,3,4] 的中位数是 3

[2,3] 的中位数是 (2 + 3) / 2 = 2.5

设计一个支持以下两种操作的数据结构：

void addNum(int num) - 从数据流中添加一个整数到数据结构中。
double findMedian() - 返回目前所有元素的中位数。
示例：

addNum(1)
addNum(2)
findMedian() -> 1.5
addNum(3) 
findMedian() -> 2
进阶:

如果数据流中所有整数都在 0 到 100 范围内，你将如何优化你的算法？
如果数据流中 99% 的整数都在 0 到 100 范围内，你将如何优化你的算法？
```

# Solution

```cpp
class MedianFinder {
public:
    /** initialize your data structure here. */
    MedianFinder() {

    }
    
    void addNum(int num) {
        if (m_max_heap.empty()){
            m_max_heap.push(num);
            return;
        }

        if (num < m_max_heap.top()) {
            m_max_heap.push(num);
            if(m_max_heap.size() - m_min_heap.size() >= 2) {
                m_min_heap.push(m_max_heap.top());
                m_max_heap.pop();
            }
        } else {
            m_min_heap.push(num);
            if(m_min_heap.size() > m_max_heap.size()) {
                m_max_heap.push(m_min_heap.top());
                m_min_heap.pop();
            }
        }
    }
    
    double findMedian() {
        int max_size = m_max_heap.size();
        int min_size = m_min_heap.size();
        if (max_size == 0 && min_size == 0) {
            return 0.0;
        }

        if ((max_size + min_size) % 2 == 1) {
            return m_max_heap.top();
        } else {
            return (m_max_heap.top() + m_min_heap.top()) / 2.0;
        }
    }

private:
    std::priority_queue<int, vector<int>, std::less<int> > m_max_heap;
    std::priority_queue<int, vector<int>, std::greater<int> > m_min_heap;
};

/**
 * Your MedianFinder object will be instantiated and called as such:
 * MedianFinder* obj = new MedianFinder();
 * obj->addNum(num);
 * double param_2 = obj->findMedian();
 */
```
