# [字母异位词分组](https://leetcode-cn.com/problems/group-anagrams/)

```
给定一个字符串数组，将字母异位词组合在一起。字母异位词指字母相同，但排列不同的字符串。

示例:

输入: ["eat", "tea", "tan", "ate", "nat", "bat"],
输出:
[
  ["ate","eat","tea"],
  ["nat","tan"],
  ["bat"]
]
说明：

所有输入均为小写字母。
不考虑答案输出的顺序。
```

# Solution

```cpp
class Solution {
public:
    vector<vector<string>> groupAnagrams(vector<string>& strs) {
        vector<vector<string>> result;
        size_t idx = 0;
        size_t size = strs.size();
        if (size == 0) {
            return result;
        }

        std::unordered_map<string, size_t> umap;

        for(auto & str : strs) {
            string s = str;
            std::sort(s.begin(), s.end());
            if (umap.find(s) == umap.end()) {
                umap[s] = idx++;
                result.push_back({str});
            } else {
                result[umap[s]].push_back(str);
            }
        }
        return result;
    }
};
```
