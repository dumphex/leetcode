# [最大子序和](https://leetcode-cn.com/problems/maximum-subarray/)

```
给定一个整数数组 nums ，找到一个具有最大和的连续子数组（子数组最少包含一个元素），返回其最大和。

示例:

输入: [-2,1,-3,4,-1,2,1,-5,4],
输出: 6
解释: 连续子数组 [4,-1,2,1] 的和最大，为 6。
进阶:

如果你已经实现复杂度为 O(n) 的解法，尝试使用更为精妙的分治法求解。
```

# Solution

## Solution1
```cpp
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        size_t size = nums.size();
        int max = nums[0];
        vector<int> dp(size, 0);
        dp[0] = nums[0];

        for(size_t i = 1; i < size; i++) {
            dp[i] = std::max(dp[i - 1] + nums[i], nums[i]);
            max = std::max(max, dp[i]);
        }

        return max;
    }
};
```

## Solution2(降低空间复杂度)
```cpp
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        int max = 0;
        int size = nums.size();
        if (size == 0) {
            return max;
        }

        int last = nums[0];
        max = nums[0];
        for(int i = 1; i < size; i++) {
            last = std::max(last + nums[i], nums[i]);
            max = last > max ? last : max;
        }
        
        return max;
    }
};
```
