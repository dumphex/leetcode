# [在排序数组中查找元素的第一个和最后一个位置](https://leetcode-cn.com/problems/find-first-and-last-position-of-element-in-sorted-array/)

```
给定一个按照升序排列的整数数组 nums，和一个目标值 target。找出给定目标值在数组中的开始位置和结束位置。

你的算法时间复杂度必须是 O(log n) 级别。

如果数组中不存在目标值，返回 [-1, -1]。

示例 1:

输入: nums = [5,7,7,8,8,10], target = 8
输出: [3,4]
示例 2:

输入: nums = [5,7,7,8,8,10], target = 6
输出: [-1,-1]
```

# Solution

```cpp
class Solution {
public:
    vector<int> searchRange(vector<int>& nums, int target) {
        int lo = 0;
        int hi = nums.size() - 1;
        vector<int> result(2, -1);

        while(lo <= hi) {
            int mid = lo + ((hi - lo) >> 1);
            if (target < nums[mid]) {
                hi = mid - 1;
            } else if (target > nums[mid]) {
                lo = mid + 1;
            } else {
                result[0] = doBSerach(nums, lo, mid, target, true);
                result[1] = doBSerach(nums, mid, hi, target, false);
                break;
            }
        }

        return result;
    }

    int doBSerach(vector<int> & nums, int lo, int hi, int target, bool left) {
        while(lo <= hi) {
            int mid = lo + ((hi - lo) >> 1);
            if (target < nums[mid]) {
                hi = mid - 1;
            } else if (target > nums[mid]) {
                lo = mid + 1;
            } else {
                if (left) {
                    int prev = doBSerach(nums, lo, mid - 1, target, true);
                    return prev < 0 ? mid : prev < mid ? prev : mid;
                } else {
                    int post = doBSerach(nums, mid + 1, hi, target, false);
                    return post < 0 ? mid : post > mid ? post : mid;
                }
            }
        }

        return -1;
    }
};
```
