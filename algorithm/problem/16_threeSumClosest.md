# [最接近的三数之和](https://leetcode-cn.com/problems/3sum-closest/)

```
给定一个包括 n 个整数的数组 nums 和 一个目标值 target。找出 nums 中的三个整数，使得它们的和与 target 最接近。返回这三个数的和。假定每组输入只存在唯一答案。

例如，给定数组 nums = [-1，2，1，-4], 和 target = 1.

与 target 最接近的三个数的和为 2. (-1 + 2 + 1 = 2).
```

# Solution

```cpp
class Solution {
public:
    int threeSumClosest(vector<int>& nums, int target) {
        int diff = INT_MAX;
        int sum = 0;
        int size = nums.size();

        std::sort(nums.begin(), nums.end());

        for(int i = 0; i < size - 2; i++) {
            int lo = i + 1;
            int hi = size - 1;
            while(lo < hi) {
                int s = nums[i] + nums[lo] + nums[hi];
                int d = std::abs(s - target);
                if (d < diff) {
                    diff = d;
                    sum = s;
                }
                if (s < target) {
                    lo++;
                } else if (s > target) {
                    hi--;
                } else {
                    return sum;
                }
            }
        }

        return sum;
    }
};
```
