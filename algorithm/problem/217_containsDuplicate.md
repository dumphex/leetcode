# [存在重复元素](https://leetcode-cn.com/problems/contains-duplicate/)

```
给定一个整数数组，判断是否存在重复元素。

如果任何值在数组中出现至少两次，函数返回 true。如果数组中每个元素都不相同，则返回 false。

示例 1:

输入: [1,2,3,1]
输出: true
示例 2:

输入: [1,2,3,4]
输出: false
示例 3:

输入: [1,1,1,3,3,4,3,2,4,2]
输出: true
```

# Solution

## solution1: 哈希表
```cpp
class Solution {
public:
    bool containsDuplicate(vector<int>& nums) {
        std::unordered_map<int, size_t> umap;

        for(auto & n : nums) {
            if (umap.find(n) != umap.end()) {
                return true;
            }

            umap[n]++;
        }

        return false;
    }
};
```


## solution2: 集合
```cpp
class Solution {
public:
    bool containsDuplicate(vector<int>& nums) {
        std::unordered_set<int> uset(nums.begin(), nums.end());
        return uset.size() != nums.size();
    }
};
```
