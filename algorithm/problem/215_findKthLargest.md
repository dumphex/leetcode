# [数组中的第K个最大元素](https://leetcode-cn.com/problems/kth-largest-element-in-an-array/)

```
在未排序的数组中找到第 k 个最大的元素。请注意，你需要找的是数组排序后的第 k 个最大的元素，而不是第 k 个不同的元素。

示例 1:

输入: [3,2,1,5,6,4] 和 k = 2
输出: 5
示例 2:

输入: [3,2,3,1,2,4,5,5,6] 和 k = 4
输出: 4
说明:

你可以假设 k 总是有效的，且 1 ≤ k ≤ 数组的长度。
```


# Solution
## solution1: 堆
- O(Nlogk)

```cpp
class Solution {
public:
    int findKthLargest(vector<int>& nums, int k) {
        std::priority_queue<int, vector<int>, std::greater<int>> pq;

        for (auto n : nums) {
            if (pq.size() < k) {
                pq.push(n);
            } else if (n > pq.top()) {
                pq.pop();
                pq.push(n);
            }
        }

        return pq.top();
    }
};

```

## solution2: 快速排序
- O(NlogN)

```cpp
class Solution {
public:
    int findKthLargest(vector<int>& nums, int k) {
        std::sort(nums.begin(), nums.end(), std::greater<int>());
        return nums[k - 1];
    }
};
```


## solution3: 快速选择
- O(N)

```cpp
class Solution {
public:
    int findKthLargest(vector<int>& nums, int k) {
        int size = nums.size();
        int idx = quickSelect(nums, 0, size - 1, size - k);
        return nums[idx];
    }

private:
    int quickSelect(vector<int> & nums, int lo, int hi, int k) {
        if (lo >= hi) {
            return lo;
        }

        int idx = partition(nums, lo, hi);
        if (idx == k) {
            return idx;
        }

        return idx > k ? quickSelect(nums, lo, idx - 1, k) : quickSelect(nums, idx + 1, hi, k);
    }

    int partition(vector<int> & nums, int lo, int hi) {
        int i = lo;
        int j = hi + 1;
        int pivot = nums[lo];

        while(true) {
            while(++i < hi && nums[i] < pivot);
            while(--j > lo && nums[j] > pivot);

            if (i >= j){
                break;
            }

            std::swap(nums[i], nums[j]);
        }

        std::swap(nums[lo], nums[j]);

        return j;
    }
};
```

