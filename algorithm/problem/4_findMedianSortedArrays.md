# [寻找两个有序数组的中位数](https://leetcode-cn.com/problems/median-of-two-sorted-arrays/)

```
给定两个大小为 m 和 n 的有序数组 nums1 和 nums2。

请你找出这两个有序数组的中位数，并且要求算法的时间复杂度为 O(log(m + n))。

你可以假设 nums1 和 nums2 不会同时为空。

示例 1:

nums1 = [1, 3]
nums2 = [2]

则中位数是 2.0
示例 2:

nums1 = [1, 2]
nums2 = [3, 4]

则中位数是 (2 + 3)/2 = 2.5
```

# Solution

## Solution1: O(m + n)
```cpp
class Solution {
public:
    double findMedianSortedArrays(vector<int>& nums1, vector<int>& nums2) {
        int sz1 = nums1.size();
        int sz2 = nums2.size();

        int i = 0;
        int j = 0;
        int k = 0;

        int sz = sz1 + sz2;
        vector<int> tmp(sz, 0);
        while(i < sz1 || j < sz2) {
            int a = i < sz1 ? nums1[i] : INT_MAX;
            int b = j < sz2 ? nums2[j] : INT_MAX;

            if (a < b) {
                tmp[k++] = a;
                i++;
            } else {
                tmp[k++] = b;
                j++;
            }

            if (k > sz / 2) {
                break;
            }
        }

        return sz % 2 == 1 ? tmp[sz / 2] : (tmp[sz / 2 - 1] + tmp[sz / 2]) / 2.0;
    }
};
```
