# [柱状图中最大的矩形](https://leetcode-cn.com/problems/largest-rectangle-in-histogram/)

```
给定 n 个非负整数，用来表示柱状图中各个柱子的高度。每个柱子彼此相邻，且宽度为 1 。

求在该柱状图中，能够勾勒出来的矩形的最大面积。

 



以上是柱状图的示例，其中每个柱子的宽度为 1，给定的高度为 [2,1,5,6,2,3]。

 



图中阴影部分为所能勾勒出的最大矩形面积，其面积为 10 个单位。

 

示例:

输入: [2,1,5,6,2,3]
输出: 10
```

# Solution

## solution1: 暴力(超时)
```cpp
class Solution {
public:
    int largestRectangleArea(vector<int>& heights) {
        int size = heights.size();
        if (size == 0) {
            return 0;
        }

        int max = 0;

        for(int i = 0; i < size; i++) {
            int min = heights[i];
            for(int j = i; j < size; j++) {
                min = heights[j] < min ? heights[j] : min;
                int product = min * (j - i + 1);
                max = product > max ? product : max;
            }
        }

        return max;
    }
};
```

## 单调栈
```cpp
class Solution {
public:
    int largestRectangleArea(vector<int>& heights) {
        int size = heights.size();
        if (size == 0) {
            return 0;
        }

        int max = 0;
        stack<int> stack;
        heights.push_back(-1);
        size++;
        for(int i = 0; i < size; i++) {
            while(!stack.empty() && heights[stack.top()] >= heights[i]) {
                int top = heights[stack.top()];
                stack.pop();
                int product = top * (stack.empty() ? i : i - stack.top() - 1);
                max = product > max ? product : max;
            }
            stack.push(i);
        }

        return max;
    }
};
```
