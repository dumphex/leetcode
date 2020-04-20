# [寻找旋转排序数组中的最小值](https://leetcode-cn.com/problems/find-minimum-in-rotated-sorted-array/)

```
假设按照升序排序的数组在预先未知的某个点上进行了旋转。

( 例如，数组 [0,1,2,4,5,6,7] 可能变为 [4,5,6,7,0,1,2] )。

请找出其中最小的元素。

你可以假设数组中不存在重复元素。

示例 1:

输入: [3,4,5,1,2]
输出: 1
示例 2:

输入: [4,5,6,7,0,1,2]
输出: 0
```

# Solution

```cpp
class Solution {
public:
    int findMin(vector<int>& nums) {
        int lo = 0;
        int hi = nums.size() - 1;

        while(lo < hi) {
            int mid = lo + (hi - lo) / 2;
            if (nums[mid] >= nums[lo] && nums[mid] > nums[hi]) {
                lo = mid + 1;
            } else if (nums[mid] <= nums[lo] && nums[mid] < nums[hi]) {
                hi = mid;
            } else if (nums[mid] >= nums[lo] && nums[mid] < nums[hi]) {
                hi = mid - 1;
            }
        }

        return nums[lo];
    }
};
```


## solution2: 基于solution1的优化
```cpp
class Solution {
public:
    int findMin(vector<int>& nums) {
        int lo = 0;
        int hi = nums.size() - 1;

        while(lo < hi) {
            int mid = lo + (hi - lo) / 2;
            if (nums[mid] > nums[hi]) {
                lo = mid + 1;
            } else {
                hi = mid;
            }
        }

        return nums[lo];
    }
};
```
