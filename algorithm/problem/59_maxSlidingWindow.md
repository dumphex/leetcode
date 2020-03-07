# [面试题59 - I. 滑动窗口的最大值](https://leetcode-cn.com/problems/hua-dong-chuang-kou-de-zui-da-zhi-lcof/)

```
面试题59 - I. 滑动窗口的最大值
给定一个数组 nums 和滑动窗口的大小 k，请找出所有滑动窗口里的最大值。

示例:

输入: nums = [1,3,-1,-3,5,3,6,7], 和 k = 3
输出: [3,3,5,5,6,7] 
解释: 

  滑动窗口的位置                最大值
---------------               -----
[1  3  -1] -3  5  3  6  7       3
 1 [3  -1  -3] 5  3  6  7       3
 1  3 [-1  -3  5] 3  6  7       5
 1  3  -1 [-3  5  3] 6  7       5
 1  3  -1  -3 [5  3  6] 7       6
 1  3  -1  -3  5 [3  6  7]      7
 

提示：

你可以假设 k 总是有效的，在输入数组不为空的情况下，1 ≤ k ≤ 输入数组的大小。

注意：本题与主站 239 题相同：https://leetcode-cn.com/problems/sliding-window-maximum/
```

# Solution

## 数组
```cpp
class Solution {
public:
    vector<int> maxSlidingWindow(vector<int>& nums, int k) {

        int max_idx = -2;
        int max_value = INT_MIN;
        int size = nums.size();
        int limit = size - k + 1;
        vector<int> results;
        if (size == 0) {
            return results;
        }

        for(int i = 0; i < limit; i++){
            if (max_idx < 0 || max_idx == i - 1) {
                max_value = nums[i];
                for(int j = i; j < i + k; j++) {
                    max_value = nums[j] >= max_value ? nums[j] : max_value;
                    max_idx = nums[j] >= max_value ? j : max_idx;
                }

            } else {
                int last_idx = i + k - 1;
                max_value = nums[last_idx] > max_value ? nums[last_idx] : max_value;
                max_idx = nums[last_idx] > max_value ? last_idx : max_idx;
            }


            results.push_back(max_value);
        }

        return results;
    }
};
```

## 双端队列
```cpp
class Solution {
public:
    class maxQueue {
     public:
        void push(int v) {
            while(!m_deque.empty() && m_deque.back() < v) {
                m_deque.pop_back();
            }

            m_deque.push_back(v);
        }

        int top() {
            return m_deque.front();
        }

        void pop() {
            if (!m_deque.empty()) {
                m_deque.pop_front();
            }
        }

     private:
        std::deque<int> m_deque;
    };

    vector<int> maxSlidingWindow(vector<int>& nums, int k) {
        vector<int> result;
        if (nums.empty()) {
            return result;
        }

        size_t size = nums.size() - k + 1;
        result.reserve(size);

        maxQueue mq;
        for(int i = 0; i < k; i++) {
            mq.push(nums[i]);
        }

        for(int i = 0; i < size; i++) {
            result.push_back(mq.top());

            if(nums[i] == mq.top()) {
                mq.pop();
            }
            if (i != size - 1) {
                mq.push(nums[i + k]);       
            }
        }

        return result;
    }
};
```
