# [字符串的最大公因子](https://leetcode-cn.com/problems/greatest-common-divisor-of-strings/)

```
对于字符串 S 和 T，只有在 S = T + ... + T（T 与自身连接 1 次或多次）时，我们才认定 “T 能除尽 S”。

返回最长字符串 X，要求满足 X 能除尽 str1 且 X 能除尽 str2。

 

示例 1：

输入：str1 = "ABCABC", str2 = "ABC"
输出："ABC"
示例 2：

输入：str1 = "ABABAB", str2 = "ABAB"
输出："AB"
示例 3：

输入：str1 = "LEET", str2 = "CODE"
输出：""
 

提示：

1 <= str1.length <= 1000
1 <= str2.length <= 1000
str1[i] 和 str2[i] 为大写英文字母
```

# Solution

## solution1
```cpp
class Solution {
public:
    string gcdOfStrings(string str1, string str2) {
        string result = "";
        size_t len1 = str1.length();
        size_t len2 = str2.length();

        string s = str1.substr(0, std::__gcd(len1, len2));
        if (compare(str1, s) && compare(str2, s)) {
            result = s;
        }

        return result;
    }

private:
    bool compare(string & original, string & substr){
        size_t size = original.length();
        size_t sub_size = substr.length();

        for(size_t i = 0; i < size; i += sub_size) {
            if (original.substr(i, sub_size) != substr) {
                return false;
            }
        }

        return true;
    }
};
```


## solution2

```cpp
class Solution {
public:
    string gcdOfStrings(string str1, string str2) {
        string result = "";

        if (str1 + str2 != str2 + str1) {
            return result;
        }

        return str1.substr(0, gcd(str1.length(), str2.length()));
    }

private:
    int gcd(int a, int b)
    {
        if (a < b) {
            std::swap(a, b);
        }

        if (b == 0) {
            return a;
        }

        return gcd(b, a % b);
    }
};
```
