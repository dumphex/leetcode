# [多数元素](https://leetcode-cn.com/problems/majority-element/)

```
给定一个大小为 n 的数组，找到其中的多数元素。多数元素是指在数组中出现次数大于 ⌊ n/2 ⌋ 的元素。

你可以假设数组是非空的，并且给定的数组总是存在多数元素。

示例 1:

输入: [3,2,3]
输出: 3
示例 2:

输入: [2,2,1,1,1,2,2]
输出: 2
```

# Solution

## solution1: 排序
```cpp
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        std::sort(nums.begin(), nums.end());
        return nums[nums.size() / 2];
    }
};
```


## solution2: 哈希表
```cpp
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        std::unordered_map<int, int> umap;
        int len = nums.size() / 2;
        int result = 0;

        for (auto & n : nums) {
            umap[n]++;
            if (umap[n] > len) {
                result = n;
                break;
            }
        }

        return result;
    }
};
```

## solution3: 快速排序 

```cpp
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        int size = nums.size();

        int idx = quick_sort(nums, 0, size - 1, size / 2);
        return nums[idx];
    }

private:
    int quick_sort(vector<int> & nums, int l, int r, int target) {
        int idx = partition(nums, l, r);
        if (target == idx) {
            return idx;
        } else if (target < idx) {
            return quick_sort(nums, l, idx - 1, target);
        } else {
            return quick_sort(nums, idx + 1, r, target);
        }
    }

    int partition(vector<int> & nums, int l, int r) {
        int pivot = nums[l];
        int i = l, j = r + 1;

        while(true) {
            while(++i < r && nums[i] < pivot);
            while(--j > l && nums[j] > pivot);

            if (i >= j) {
                break;
            }
            
            std::swap(nums[i], nums[j]);
        }
	    std::swap(nums[l], nums[j]);

        return j;
    }

};
```
