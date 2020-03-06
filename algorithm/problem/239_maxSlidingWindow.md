# [滑动窗口最大值](https://leetcode-cn.com/problems/sliding-window-maximum/)

```
给定一个数组 nums，有一个大小为 k 的滑动窗口从数组的最左侧移动到数组的最右侧。你只可以看到在滑动窗口内的 k 个数字。滑动窗口每次只向右移动一位。

返回滑动窗口中的最大值。

 

示例:

输入: nums = [1,3,-1,-3,5,3,6,7], 和 k = 3
输出: [3,3,5,5,6,7] 
解释: 

  滑动窗口的位置                最大值
---------------               -----
[1  3  -1] -3  5  3  6  7       3
 1 [3  -1  -3] 5  3  6  7       3
 1  3 [-1  -3  5] 3  6  7       5
 1  3  -1 [-3  5  3] 6  7       5
 1  3  -1  -3 [5  3  6] 7       6
 1  3  -1  -3  5 [3  6  7]      7
 

提示：

你可以假设 k 总是有效的，在输入数组不为空的情况下，1 ≤ k ≤ 输入数组的大小。

 

进阶：

你能在线性时间复杂度内解决此题吗？
```

# Solution

```cpp

class Solution {
public:
    vector<int> maxSlidingWindow(vector<int>& nums, int k) {
        int max_idx = -2;
        int max_value = INT_MIN;
        int size = nums.size();
        int limit = size - k + 1;
        vector<int> results;
        if (size == 0) {
            return results;
        }

        for(int i = 0; i < limit; i++){
            if (max_idx < 0 || max_idx == i - 1) {
                max_value = nums[i];
                for(int j = i; j < i + k; j++) {
                    max_value = nums[j] >= max_value ? nums[j] : max_value;
                    max_idx = nums[j] >= max_value ? j : max_idx;
                }

            } else {
                int last_idx = i + k - 1;
                max_value = nums[last_idx] > max_value ? nums[last_idx] : max_value;
                max_idx = nums[last_idx] > max_value ? last_idx : max_idx;
            }


            results.push_back(max_value);
        }

        return results;
    }
};
```
