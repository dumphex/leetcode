# [题目](https://leetcode-cn.com/problems/two-sum/)
```
1. 两数之和
给定一个整数数组 nums 和一个目标值 target，请你在该数组中找出和为目标值的那 两个 整数，并返回他们的数组下标。

你可以假设每种输入只会对应一个答案。但是，你不能重复利用这个数组中同样的元素。

示例:

给定 nums = [2, 7, 11, 15], target = 9

因为 nums[0] + nums[1] = 2 + 7 = 9
所以返回 [0, 1]
```

# Solution

```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        std::unordered_map<int, int> umap;
        std::vector<int> result(2, 0);
        size_t n = nums.size();

        for (size_t i = 0; i < n; i++) {
            int diff = target - nums[i];
            if(umap.find(diff) == umap.end()) {
                umap[nums[i]] = i;
            } else {
                result[0] = umap[diff];
                result[1] = i;
                break;
            }
        }

        return result;
    }
};
```

