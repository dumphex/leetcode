# [无重复字符的最长子串](https://leetcode-cn.com/problems/longest-substring-without-repeating-characters/)

```
给定一个字符串，请你找出其中不含有重复字符的 最长子串 的长度。

示例 1:

输入: "abcabcbb"
输出: 3 
解释: 因为无重复字符的最长子串是 "abc"，所以其长度为 3。
示例 2:

输入: "bbbbb"
输出: 1
解释: 因为无重复字符的最长子串是 "b"，所以其长度为 1。
示例 3:

输入: "pwwkew"
输出: 3
解释: 因为无重复字符的最长子串是 "wke"，所以其长度为 3。
     请注意，你的答案必须是 子串 的长度，"pwke" 是一个子序列，不是子串。
```

# Solution

## solution1:
```cpp
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        int max = 0;
        std::queue<char> queue;
        std::unordered_map<char, int> map;

        int size = s.length();
        int len = 0;
        int start = 0;
        for(int i = 0; i < size; i++) {
            if (map.find(s[i]) == map.end()) {
                map[s[i]] = i;
                queue.push(s[i]);
            } else {
                len = queue.size();
                max = len > max ? len : max;

                bool poped = false;
                while(!poped) {
                    char ch = queue.front();
                    poped = ch == s[i] ? true : false;
                    queue.pop();
                    map.erase(ch);
                }
                queue.push(s[i]);
                map[s[i]] = i;
            }
        }

        len = map.size();
        max = len > max ? len : max;

        return max;
    }
};
```

## solution2:
```cpp
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        std::unordered_set<char> set;
        int max = 0;
        int size = s.length();
        int start = 0;

        for(int i = 0; i < size; i++) {
            while(set.find(s[i]) != set.end()) {
                set.erase(s[start++]);
            }
            
            set.insert(s[i]);
            int len = i - start + 1;
            max = len > max ? len : max;
        }

        return max;
    }
};
```
