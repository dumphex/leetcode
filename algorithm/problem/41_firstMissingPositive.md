# [缺失的第一个正数](https://leetcode-cn.com/problems/first-missing-positive/)

```
给定一个未排序的整数数组，找出其中没有出现的最小的正整数。

示例 1:

输入: [1,2,0]
输出: 3
示例 2:

输入: [3,4,-1,1]
输出: 2
示例 3:

输入: [7,8,9,11,12]
输出: 1
说明:

你的算法的时间复杂度应为O(n)，并且只能使用常数级别的空间。
```

# Solution

```cpp
class Solution {
public:
    int firstMissingPositive(vector<int>& nums) {
        int size = nums.size();
        if (size == 0) {
            return 1;
        }

        int i = 0;
        for(i = 0; i < size; i++){
            while(nums[i] >= 1 && nums[i] <= size && nums[i] != nums[nums[i] - 1]) {
                swap(nums[i], nums[nums[i] - 1]);
            }
        }

        for(i = 0; i < size; i++) {
            if (i != nums[i] - 1) {
                break;
            }
        }

        return i < size ? i + 1 : size + 1;
    }
};
```
