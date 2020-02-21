# [重复的DNA序列](https://leetcode-cn.com/problems/repeated-dna-sequences/)

```
所有 DNA 都由一系列缩写为 A，C，G 和 T 的核苷酸组成，例如：“ACGAATTCCG”。在研究 DNA 时，识别 DNA 中的重复序列有时会对研究非常有帮助。

编写一个函数来查找 DNA 分子中所有出现超过一次的 10 个字母长的序列（子串）。

 

示例：

输入：s = "AAAAACCCCCAAAAACCCCCCAAAAAGGGTTT"
输出：["AAAAACCCCC", "CCCCCAAAAA"]
```


# Solution
```cpp
class Solution {
public:
    vector<string> findRepeatedDnaSequences(string s) {
        int len = s.length();
        vector<string> result;
        result.reserve(len);

        if (len <= 10) {
            return result;
        }

        std::unordered_map<string, int> map;
        for (int i = 0; i <= len - 10; i++) {
            string sub = s.substr(i, 10);
            if (map.find(sub) == map.end()) {
                map[sub] = 1;
            } else{
                map[sub]++;
                if (map[sub] == 2) {
                    result.push_back(sub);
                }
            }
        }

        return result;
    }
};
```
