# [面试题50. 第一个只出现一次的字符](https://leetcode-cn.com/problems/di-yi-ge-zhi-chu-xian-yi-ci-de-zi-fu-lcof/)

```
在字符串 s 中找出第一个只出现一次的字符。如果没有，返回一个单空格。

示例:

s = "abaccdeff"
返回 "b"

s = "" 
返回 " "
 

限制：

0 <= s 的长度 <= 50000
```

# Solution

```cpp
class Solution {
public:
    char firstUniqChar(string s) {
        std::unordered_map<char, int> umap;

        for(auto & ch : s) {
            umap[ch]++;
        }

        char target = ' ';
        for(auto & ch : s) {
            if (umap[ch] == 1) {
                target = ch;
                break;
            }
        }

        return target;
    }
};
```
