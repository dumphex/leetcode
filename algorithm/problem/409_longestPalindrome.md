# [最长回文串](https://leetcode-cn.com/problems/longest-palindrome/)

```

给定一个包含大写字母和小写字母的字符串，找到通过这些字母构造成的最长的回文串。

在构造过程中，请注意区分大小写。比如 "Aa" 不能当做一个回文字符串。

注意:
假设字符串的长度不会超过 1010。

示例 1:

输入:
"abccccdd"

输出:
7

解释:
我们可以构造的最长的回文串是"dccaccd", 它的长度是 7。
```

# Solution

## solution1: 哈希表
```cpp
class Solution {
public:
    int longestPalindrome(string s) {
        std::unordered_map<char, int> map;

        for(auto & ch : s) { 
            map[ch]++;
        }

        int length = 0;
        bool has_odd = false;
        for (auto & m : map) {
            int len = m.second;

            if (len & 1) {
                len = len - 1;
                has_odd = true;
            }

            length += len;
        }

        return length + (has_odd ? 1 : 0);
    }
};
```


## solution2: 数组
```cpp
class Solution {
public:
    int longestPalindrome(string s) {
        std::array<int, 58> map = {0};
        int length = 0;
        bool has_odd = false;

        for(auto & ch : s) {
            int idx = ch - 'A'; 
            map[idx]++;
        }

        for (auto & m : map) {
            if (m & 1) {
                length += m - 1;
                has_odd = true;
            } else {
                length += m;
            }
        }

        return length + (has_odd ? 1 : 0);
    }
};
```
