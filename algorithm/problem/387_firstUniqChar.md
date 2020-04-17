# [字符串中的第一个唯一字符](https://leetcode-cn.com/problems/first-unique-character-in-a-string/)

```
给定一个字符串，找到它的第一个不重复的字符，并返回它的索引。如果不存在，则返回 -1。

案例:

s = "leetcode"
返回 0.

s = "loveleetcode",
返回 2.
 

注意事项：您可以假定该字符串只包含小写字母。
```

# Solution

```cpp
class Solution {
public:
    int firstUniqChar(string s) {
        //vector<int> nums(26, 0);
        int nums[26] = {0};

        for(auto ch : s) {
            nums[ch - 'a']++;
        }

        int size = s.length();
        for(int i = 0; i < size; i++) {
            if (nums[s[i] - 'a'] == 1) {
                return i;
            }
        }

        return -1;
    }
};
```
