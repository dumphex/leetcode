# []()

```
给定一个整数数组 nums，按要求返回一个新数组 counts。数组 counts 有该性质： counts[i] 的值是  nums[i] 右侧小于 nums[i] 的元素的数量。

示例:

输入: [5,2,6,1]
输出: [2,1,1,0] 
解释:
5 的右侧有 2 个更小的元素 (2 和 1).
2 的右侧仅有 1 个更小的元素 (1).
6 的右侧有 1 个更小的元素 (1).
1 的右侧有 0 个更小的元素.
```

# Solution

## Solution1: O(n^2), 超时
```cpp
class Solution {
public:
    vector<int> countSmaller(vector<int>& nums) {
        vector<int> result;
        int size = nums.size();
        result.reserve(size);

        for(int i = 0; i < size; i++) {
            int counter = 0;
            for(int j = i + 1; j < size; j++) {
                if (nums[j] < nums[i]) {
                    counter++;
                }
            }
            result.push_back(counter);
        }

        return result;
    }
};
```
