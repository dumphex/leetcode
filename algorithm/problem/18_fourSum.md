# [四数之和](https://leetcode-cn.com/problems/4sum/)

```
给定一个包含 n 个整数的数组 nums 和一个目标值 target，判断 nums 中是否存在四个元素 a，b，c 和 d ，使得 a + b + c + d 的值与 target 相等？找出所有满足条件且不重复的四元组。

注意：

答案中不可以包含重复的四元组。

示例：

给定数组 nums = [1, 0, -1, 0, -2, 2]，和 target = 0。

满足要求的四元组集合为：
[
  [-1,  0, 0, 1],
  [-2, -1, 1, 2],
  [-2,  0, 0, 2]
]
```

# Solution

```cpp
class Solution {
public:
    vector<vector<int>> fourSum(vector<int>& nums, int target) {
        vector<vector<int>> result;
        int size = nums.size();

        std::sort(nums.begin(), nums.end());

        for(int i = 0; i < size - 3; i++) {
            if (i >= 1 && nums[i] == nums[i - 1]) {
                continue;
            }

            for(int j = i + 1; j < size - 2; j++) {
                if (j > i + 1 && nums[j] == nums[j - 1]) {
                    continue;
                }

                int lo = j + 1;
                int hi = size - 1;

                while(lo < hi) {
                    int sum = nums[i] + nums[j] + nums[lo] + nums[hi];
                    if (sum < target) {
                        lo++;
                    } else if (sum > target) {
                        hi--;
                    } else {
                        result.push_back({nums[i], nums[j], nums[lo], nums[hi]});
                        while(lo < hi && nums[lo] == nums[++lo]);
                        while(lo < hi && nums[hi] == nums[--hi]);
                    }
                }
            }
        }

        return result;
    }
};
```
