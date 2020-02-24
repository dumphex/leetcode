# [数组的度](https://leetcode-cn.com/problems/degree-of-an-array/)

```
给定一个非空且只包含非负数的整数数组 nums, 数组的度的定义是指数组里任一元素出现频数的最大值。

你的任务是找到与 nums 拥有相同大小的度的最短连续子数组，返回其长度。

示例 1:

输入: [1, 2, 2, 3, 1]
输出: 2
解释: 
输入数组的度是2，因为元素1和2的出现频数最大，均为2.
连续子数组里面拥有相同度的有如下所示:
[1, 2, 2, 3, 1], [1, 2, 2, 3], [2, 2, 3, 1], [1, 2, 2], [2, 2, 3], [2, 2]
最短连续子数组[2, 2]的长度为2，所以返回2.
示例 2:

输入: [1,2,2,3,1,4,2]
输出: 6
注意:

nums.length 在1到50,000区间范围内。
nums[i] 是一个在0到49,999范围内的整数。
```

# Solution

```cpp
class Solution {
public:
    int findShortestSubArray(vector<int>& nums) {
        std::unordered_map<int, vector<int>> umap;
        size_t size = nums.size();
        for (size_t i = 0; i < size; i++) {
            umap[nums[i]].push_back(i);
        }

        size_t max_degree = 0, min_len = size;
        for (auto m : umap) {
            size_t degree = m.second.size();
            size_t len = m.second[degree - 1] - m.second[0] + 1;
            if (degree > max_degree) {
                max_degree = degree;
                min_len = len;
            } else if (degree == max_degree) {
                min_len = len < min_len ? len : min_len;
            }
        }

        return min_len;
    }
};
```
