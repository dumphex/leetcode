# [三数之和](https://leetcode-cn.com/problems/3sum/)

```
给你一个包含 n 个整数的数组 nums，判断 nums 中是否存在三个元素 a，b，c ，使得 a + b + c = 0 ？请你找出所有满足条件且不重复的三元组。

注意：答案中不可以包含重复的三元组。

 

示例：

给定数组 nums = [-1, 0, 1, 2, -1, -4]，

满足要求的三元组集合为：
[
  [-1, 0, 1],
  [-1, -1, 2]
]
```

# Solution

```cpp
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
        vector<vector<int>> result;
        size_t size = nums.size();
        size_t lo = 0;
        size_t hi = size - 1;
        
        std::sort(nums.begin(), nums.end());

        for(size_t i = 0; i < size; i++) {
            if (nums[i] > 0) {
                break;
            }

            if (i >= 1 && nums[i] == nums[i - 1]) {
                continue;
            }

            lo = i + 1;
            hi = size - 1;
            int target = 0 - nums[i];
            while(lo < hi) {
                int sum = nums[lo] + nums[hi];
                if (sum < target) {
                    lo++;
                } else if (sum > target) {
                    hi--;
                } else {
                    result.push_back({nums[i], nums[lo], nums[hi]});
                    lo++;
                    hi--;
                    while(lo < hi && nums[lo] == nums[lo - 1]) {
                        lo++;
                    }

                    while(hi > lo && nums[hi] == nums[hi + 1]) {
                        hi--;
                    }
                }
            }
        }

        return result;
    }
};
```
