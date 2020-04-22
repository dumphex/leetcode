# [面试题39. 数组中出现次数超过一半的数字](https://leetcode-cn.com/problems/shu-zu-zhong-chu-xian-ci-shu-chao-guo-yi-ban-de-shu-zi-lcof/)

```
数组中有一个数字出现的次数超过数组长度的一半，请找出这个数字。

 

你可以假设数组是非空的，并且给定的数组总是存在多数元素。

 

示例 1:

输入: [1, 2, 3, 2, 2, 2, 5, 4, 2]
输出: 2
```

# Solution

## solution1: 排序, O(NlogN)
```cpp
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        std::sort(nums.begin(), nums.end());
        return nums[nums.size() / 2];
    }
};
```


## solution2: 哈希表, O(N)
```cpp
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        std::unordered_map<int, int> umap;
        int target = nums.size() / 2 + 1;
        for(auto & n : nums) {
            umap[n]++;
            if (umap[n] >= target) {
                return n;
            }
        }

        return nums[0];
    }
};
```


## solutoin3: 快速选择
- 修改了原数组

```cpp
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        int size = nums.size();

        int idx = quick_sort(nums, 0, size - 1, size / 2);
        return nums[idx];
    }

private:
    int quick_sort(vector<int> & nums, int lo, int hi, int target) {
        int idx = partition(nums, lo, hi);
        if (target == idx) {
            return idx;
        } 
        
        return target < idx ? quick_sort(nums, lo, idx - 1, target) : quick_sort(nums, idx + 1, hi, target);
    }

    int partition(vector<int> & nums, int lo, int hi) {
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

## solution4: 投票法, O(N)
```cpp
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        int counter = 0;
        int target = nums[0];

        for(auto & n : nums) {
            if (counter == 0) {
                target = n;
            }
            
            n == target ? counter++ : counter--;
            //counter += n == target ? 1 : -1;
        }

        return target;
    }
};
```
