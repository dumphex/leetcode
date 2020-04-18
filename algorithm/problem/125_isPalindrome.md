# [验证回文串](https://leetcode-cn.com/problems/valid-palindrome/)

```
给定一个字符串，验证它是否是回文串，只考虑字母和数字字符，可以忽略字母的大小写。

说明：本题中，我们将空字符串定义为有效的回文串。

示例 1:

输入: "A man, a plan, a canal: Panama"
输出: true
示例 2:

输入: "race a car"
输出: false
```

# Solution

```cpp
class Solution {
public:
    bool isPalindrome(string s) {
        if (s.empty()) {
            return true;
        }


        int i = 0;
        int j = s.length() - 1;

        while(i <= j) {
            while(i <= j && !isValidChar(s[i])) {
                i++;
            }

            while(i <= j && !isValidChar(s[j])) {
                j--;
            }

            if (i >= j) {
                break;
            }
            
            char ch1 = s[i];
            if (s[i] >= 'A' && s[i] <= 'Z') {
                ch1 += 32;
            }

            char ch2 = s[j];
            if (s[j] >= 'A' && s[j] <= 'Z') {
                ch2 += 32;
            }

            if (ch1 == ch2) {
                i++;
                j--;
            } else {
                return false;
            }
        }

        return true;
    }

private:
    bool isValidChar(char ch) {
        if (ch >= 'A' && ch <= 'Z' || ch >= 'a' && ch <= 'z' || ch >= '0' && ch <= '9') {
            return true;
        }

        return false;
    }
};
```


## solution2: 双指针优化版
```cpp
class Solution {
public:
    bool isPalindrome(string s) {
        if (s.empty()) {
            return true;
        }

        int lo = 0;
        int hi = s.length() - 1;

        while(lo < hi) {
            while(lo < hi && !isalnum(s[lo])) {
                lo++;
            }

            while(lo < hi && !isalnum(s[hi])) {
                hi--;
            }

            if (lo >= hi) {
                break;
            }
            
            if (tolower(s[lo]) == tolower(s[hi])) {
                lo++;
                hi--;
            } else {
                return false;
            }
        }

        return true;
    }
};
```
