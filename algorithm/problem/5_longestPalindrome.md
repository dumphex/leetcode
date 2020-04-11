# [最长回文子串](https://leetcode-cn.com/problems/longest-palindromic-substring/)

```
给定一个字符串 s，找到 s 中最长的回文子串。你可以假设 s 的最大长度为 1000。

示例 1：

输入: "babad"
输出: "bab"
注意: "aba" 也是一个有效答案。
示例 2：

输入: "cbbd"
输出: "bb"
```

# Solution

## solution1: 暴力(超时)
```cpp
class Solution {
public:
    string longestPalindrome(string s) {
        int i = 0;
        int size = s.length();
        std::string result;

        for(int i = 0; i < size; i++) {
            for(int j = i; j < size; j++) {
                string str = s.substr(i, j - i + 1);
                if (isPalindrome(str) && str.length() > result.length()) {
                    result = str;
                }
            }
        }

        return result;
    }

private:
    bool isPalindrome(string & s) {
        int i = 0; 
        int j = s.length() - 1;
        while(i <= j && s[i] == s[j]) {
            i++;
            j--;
        }

        return i > j ? true : false;
    }
};
```


## solution2: 动态规划
```cpp
class Solution {
public:
    string longestPalindrome(string s) {
        int size = s.length();
        if (size < 2) {
            return s;
        }

        vector<vector<bool>> dp(size, vector<bool>(size, false));
        int start = 0;
        int max_len = 1;

        for(int j = 1; j < size; j++) {
            for(int i = 0; i < j; i++) {
                int len = j - i + 1;
                if (s[i] == s[j]) {
                    if (len <= 3) {
                        dp[i][j] = true;
                    } else {
                        dp[i][j] = dp[i + 1][j - 1];
                    }
                }

                if (dp[i][j] && len > max_len) {
                    start = i;
                    max_len = len;
                }
            }
        }

        return s.substr(start, max_len);
    }
};
```
