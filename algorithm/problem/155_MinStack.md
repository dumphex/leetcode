# [最小栈](https://leetcode-cn.com/problems/min-stack/)

```
设计一个支持 push，pop，top 操作，并能在常数时间内检索到最小元素的栈。

push(x) -- 将元素 x 推入栈中。
pop() -- 删除栈顶的元素。
top() -- 获取栈顶元素。
getMin() -- 检索栈中的最小元素。
示例:

MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin();   --> 返回 -3.
minStack.pop();
minStack.top();      --> 返回 0.
minStack.getMin();   --> 返回 -2
```

# Solution

## 方案1: vector + dp
```cpp
class MinStack {
public:
    struct Object {
        int data;
        int min;

        Object(int d, int m) : data(d), min(m) {}
    };

    /** initialize your data structure here. */
    MinStack() {
        m_vector.reserve(32);
    }

    void push(int x) {
        int min = x;
        if (!m_vector.empty()) {
            int last = m_vector.back().min;
            min = min < last ? min : last;
        }

        m_vector.emplace_back(x, min);
    }

    void pop() {
        m_vector.pop_back();
    }

    int top() {
        return m_vector.back().data;
    }

    int getMin() {
        return m_vector.back().min;
    }

private:
    std::vector<Object> m_vector;
};

/**
 * Your MinStack object will be instantiated and called as such:
 * MinStack* obj = new MinStack();
 * obj->push(x);
 * obj->pop();
 * int param_3 = obj->top();
 * int param_4 = obj->getMin();
 */
```

## 方案2: 辅助栈
```cpp
class MinStack {
public:
    /** initialize your data structure here. */
    MinStack() {

    }
    
    void push(int x) {
        data_stack.push(x);
        if (min_stack.empty() || x < min_stack.top()) {
            min_stack.push(x);
        } else {
            min_stack.push(min_stack.top());
        }
    }
    
    void pop() {
        if (!data_stack.empty()) {
            data_stack.pop();
        }
        
        if (!min_stack.empty()) {
            min_stack.pop();
        }
    }
    
    int top() {
        return data_stack.top();
    }
    
    int getMin() {
        return min_stack.top();
    }

private:
    stack<int> data_stack;
    stack<int> min_stack;
};

/**
 * Your MinStack object will be instantiated and called as such:
 * MinStack* obj = new MinStack();
 * obj->push(x);
 * obj->pop();
 * int param_3 = obj->top();
 * int param_4 = obj->getMin();
 */
```
