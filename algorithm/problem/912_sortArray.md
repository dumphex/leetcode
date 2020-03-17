# [排序数组](https://leetcode-cn.com/problems/sort-an-array/)

```
给定一个整数数组 nums，将该数组升序排列。

 

示例 1：

输入：[5,2,3,1]
输出：[1,2,3,5]
示例 2：

输入：[5,1,1,2,0,0]
输出：[0,0,1,1,2,5]
 

提示：

1 <= A.length <= 10000
-50000 <= A[i] <= 50000
```

# Solution

```cpp
class Solution {
public:
    vector<int> sortArray(vector<int>& nums) {
        vector<int> tmp(nums);
        quick_sort(tmp, 0, tmp.size() - 1);

        return tmp;
    }

private:
    void quick_sort(vector<int> & nums, int lo, int hi) {
        if (lo >= hi) {
            return;
        }

        int idx = partition(nums, lo, hi);
        quick_sort(nums, lo, idx - 1);
        quick_sort(nums, idx + 1, hi);
    }

    int partition(vector<int>& nums, int lo, int hi) {
        int i = lo;
        int j = hi + 1;
        int pivot = nums[lo];

        while(true) {
            while(++i < hi && nums[i] < pivot);
            while(--j > lo && nums[j] > pivot);

            if (i >= j) {
                break;
            }

            std::swap(nums[i], nums[j]);
        }

        std::swap(nums[lo], nums[j]);
        return j;
    }
};
```
