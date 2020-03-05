# [错误的集合](https://leetcode-cn.com/problems/set-mismatch/)

```
集合 S 包含从1到 n 的整数。不幸的是，因为数据错误，导致集合里面某一个元素复制了成了集合里面的另外一个元素的值，导致集合丢失了一个整数并且有一个元素重复。

给定一个数组 nums 代表了集合 S 发生错误后的结果。你的任务是首先寻找到重复出现的整数，再找到丢失的整数，将它们以数组的形式返回。

示例 1:

输入: nums = [1,2,2,4]
输出: [2,3]
注意:

给定数组的长度范围是 [2, 10000]。
给定的数组是无序的。
```

# Solution

## 哈希表
```cpp
class Solution {
public:
    vector<int> findErrorNums(vector<int>& nums) {
        std::unordered_map<int, size_t> umap;

        for(auto & n : nums) {
            umap[n]++;
        }

        size_t size = nums.size();
        vector<int> result(2, -1);
        for(size_t i = 1; i <= size; i++) {
            if (umap.find(i) == umap.end()) {
                result[1] = i;
            } else if (umap[i] > 1) {
                result[0] = i;
            }
        }

        return result;
    }
};
```
