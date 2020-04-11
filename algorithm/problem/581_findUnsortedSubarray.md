# [最短无序连续子数组](https://leetcode-cn.com/problems/shortest-unsorted-continuous-subarray/submissions/)

```
给定一个整数数组，你需要寻找一个连续的子数组，如果对这个子数组进行升序排序，那么整个数组都会变为升序排序。

你找到的子数组应是最短的，请输出它的长度。

示例 1:

输入: [2, 6, 4, 8, 10, 9, 15]
输出: 5
解释: 你只需要对 [6, 4, 8, 10, 9] 进行升序排序，那么整个表都会变为升序排序。
说明 :

输入的数组长度范围在 [1, 10,000]。
输入的数组可能包含重复元素 ，所以升序的意思是<=。
```

# Solution

## solution1: 排序
```cpp
class Solution {
public:
    int findUnsortedSubarray(vector<int>& nums) {
        int j = -1;
        int k = -1;
        int size = nums.size();

        vector<int> tmp(nums);
        std::sort(tmp.begin(), tmp.end());

        for(int i = 0; i < size; i++) {
            if(nums[i] != tmp[i]) {
                j = j < 0 ? i : j;
                k = i;
            }
        }

        return j < 0 ? 0 : k - j + 1;
    }
};
```


## solution2: 单调栈
```cpp
class Solution {
public:
    int findUnsortedSubarray(vector<int>& nums) {
        stack<int> stack;
        int size = nums.size();
        int l = size - 1;
        int r = 0;

        for(int i = 0; i < size; i++) {
            while(!stack.empty() && nums[i] < nums[stack.top()]) {
                l = std::min(l, stack.top());
                stack.pop();
            }
            stack.push(i);
        }

        while(!stack.empty()) {
            stack.pop();
        }
        for(int i = size - 1; i >= 0; i--) {
            while(!stack.empty() && nums[i] > nums[stack.top()]) {
                r = std::max(r, stack.top());
                stack.pop();
            }
            stack.push(i);
        }

        return l < r ? r - l + 1 : 0;
    }
};
```
