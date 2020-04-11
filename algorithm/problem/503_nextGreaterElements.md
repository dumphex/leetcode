# [下一个更大元素 II](https://leetcode-cn.com/problems/next-greater-element-ii/)

```
给定一个循环数组（最后一个元素的下一个元素是数组的第一个元素），输出每个元素的下一个更大元素。数字 x 的下一个更大的元素是按数组遍历顺序，这个数字之后的第一个比它更大的数，这意味着你应该循环地搜索它的下一个更大的数。如果不存在，则输出 -1。

示例 1:

输入: [1,2,1]
输出: [2,-1,2]
解释: 第一个 1 的下一个更大的数是 2；
数字 2 找不到下一个更大的数； 
第二个 1 的下一个最大的数需要循环搜索，结果也是 2。
```

# Solution

## solution1
```cpp
class Solution {
public:
    vector<int> nextGreaterElements(vector<int>& nums) {
        int size = nums.size();
        int new_size = 2 * size;
        vector<int> tmp(new_size, 0);
        std::copy(nums.begin(), nums.end(), tmp.begin());
        std::copy(nums.begin(), nums.end(), tmp.begin() + size);

        std::stack<int> stack;
        std::unordered_map<int, int> map;
        for(int i = 0; i < new_size; i++) {
            while(!stack.empty() && tmp[i] > tmp[stack.top()]) {
                map[stack.top() % size] = tmp[i];
                stack.pop();
            }
            stack.push(i);
        }

        while(!stack.empty()) {
            int top = stack.top() % size;
            if(map.find(top) == map.end()) {
                map[top] = -1;
            }
            stack.pop();
        }

        vector<int> result;
        result.reserve(size);
        for(int i = 0; i < size; i++) {
            result.push_back(map[i]);
        }

        return result;
    }
};
```


## solution2
```cpp
class Solution {
public:
    vector<int> nextGreaterElements(vector<int>& nums) {
        int size = nums.size();
        int new_size = 2 * size;

        std::stack<int> stack;
        vector<int> result(size, -1);
        for(int i = 0; i < new_size; i++) {
            int j = i % size;
            while(!stack.empty() && nums[j] > nums[stack.top()]) {
                result[stack.top()] = nums[j];
                stack.pop();
            }
            stack.push(j);
        }

        return result;
    }
};
```
