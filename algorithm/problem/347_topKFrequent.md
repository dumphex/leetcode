# [前 K 个高频元素](https://leetcode-cn.com/problems/top-k-frequent-elements/)

```
给定一个非空的整数数组，返回其中出现频率前 k 高的元素。

示例 1:

输入: nums = [1,1,1,2,2,3], k = 2
输出: [1,2]
示例 2:

输入: nums = [1], k = 1
输出: [1]
说明：

你可以假设给定的 k 总是合理的，且 1 ≤ k ≤ 数组中不相同的元素的个数。
你的算法的时间复杂度必须优于 O(n log n) , n 是数组的大小。
```

# Solution


```cpp
class Solution {
public:
    vector<int> topKFrequent(vector<int>& nums, int k) {
        std::unordered_map<int, size_t> umap;

        for(auto & n : nums) {
            umap[n]++;
        }

        // min heap
        using T = std::pair<int, int>;
        std::priority_queue<T, vector<T>, std::greater<T>> pq;
        for (auto & m : umap) {
            if (pq.size() < k) {
                pq.emplace(m.second, m.first);
            } else {
                if (m.second > pq.top().first) {
                    pq.pop();
                    pq.emplace(m.second, m.first);
                }
            }
        }

        vector<int> result(k);
        while(!pq.empty()) {
            result[--k] = pq.top().second;
            pq.pop();
        }

        return result;
    }
};
```
