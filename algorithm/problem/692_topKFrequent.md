# [前K个高频单词](https://leetcode-cn.com/problems/top-k-frequent-words/)

```
给一非空的单词列表，返回前 k 个出现次数最多的单词。

返回的答案应该按单词出现频率由高到低排序。如果不同的单词有相同出现频率，按字母顺序排序。

示例 1：

输入: ["i", "love", "leetcode", "i", "love", "coding"], k = 2
输出: ["i", "love"]
解析: "i" 和 "love" 为出现次数最多的两个单词，均为2次。
    注意，按字母顺序 "i" 在 "love" 之前。
 

示例 2：

输入: ["the", "day", "is", "sunny", "the", "the", "the", "sunny", "is", "is"], k = 4
输出: ["the", "is", "sunny", "day"]
解析: "the", "is", "sunny" 和 "day" 是出现次数最多的四个单词，
    出现次数依次为 4, 3, 2 和 1 次。
 

注意：

假定 k 总为有效值， 1 ≤ k ≤ 集合元素数。
输入的单词均由小写字母组成。
 

扩展练习：

尝试以 O(n log k) 时间复杂度和 O(n) 空间复杂度解决。
```

# Solution

## min heap
```cpp
class Solution {
public:
    using mypair = std::pair<std::string, size_t>;
    struct mycompare {
        bool operator()(const mypair & l, const mypair & r) const {
            if (l.second > r.second) {
                return true;
            } else if (l.second == r.second) {
                return l.first < r.first;
            } else {
                return false;
            }
        }
    };

    vector<string> topKFrequent(vector<string>& words, int k) {
        std::unordered_map<std::string, size_t> umap;

        for(auto & w : words) {
            umap[w]++;
        }

        // min heap
        std::priority_queue<mypair, std::vector<mypair>, mycompare> pq;
        for (auto & m : umap) {
            pq.push(std::make_pair(m.first, m.second));
            if (pq.size() > k) {
                pq.pop();
            }
        }

        std::vector<string> result;
        result.resize(k);
        int i = k - 1;
        while(!pq.empty() && i >= 0) {
            result[i--] = pq.top().first;
            pq.pop();
        }

        return result;
    }
};
```

## max heap

```cpp
class Solution {
public:
    using mypair = std::pair<std::string, size_t>;
    struct mycompare {
        bool operator()(const mypair & l, const mypair & r) const {
            if (l.second < r.second) {
                return true;
            } else if (l.second == r.second) {
                return l.first > r.first;
            } else {
                return false;
            }
        }
    };

    vector<string> topKFrequent(vector<string>& words, int k) {
        std::unordered_map<std::string, size_t> umap;

        for(auto & w : words) {
            if (umap.find(w) == umap.end()) {
                umap[w] = 1;
            } else {
                umap[w]++;
            }
        }

        // max heap
        std::priority_queue<mypair, std::vector<mypair>, mycompare> pq;
        
        for (auto & m : umap) {
            pq.push(std::make_pair(m.first, m.second));
        }

        std::vector<string> result;
        result.reserve(k);
        size_t i = 0;
        while(!pq.empty() && i++ < k) {
            result.push_back(pq.top().first);
            pq.pop();
        }

        return result;
    }
};
```
