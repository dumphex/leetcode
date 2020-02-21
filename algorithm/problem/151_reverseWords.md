# [ 翻转字符串里的单词]()

```
给定一个字符串，逐个翻转字符串中的每个单词。

 

示例 1：

输入: "the sky is blue"
输出: "blue is sky the"
示例 2：

输入: "  hello world!  "
输出: "world! hello"
解释: 输入字符串可以在前面或者后面包含多余的空格，但是反转后的字符不能包括。
示例 3：

输入: "a good   example"
输出: "example good a"
解释: 如果两个单词间有多余的空格，将反转后单词间的空格减少到只含一个。
 

说明：

无空格字符构成一个单词。
输入字符串可以在前面或者后面包含多余的空格，但是反转后的字符不能包括。
如果两个单词间有多余的空格，将反转后单词间的空格减少到只含一个。
```

# Solution
```cpp
class Solution {
public:
    string reverseWords(string s) {
        string result;
        stack<string> stack;
        size_t len = s.length();
        
        for(size_t i = 0; i < len; i++) {
            if(s[i] == ' ') {
                continue;
            }

            size_t j = i + 1;
            while(j < len) {
                if (s[j] == ' ') {
                    break;
                }
                j++;
            }

            string substr = s.substr(i, j - i);
            stack.push(substr);
            i = j;
        }
        
        while(!stack.empty()) {
            result += stack.top() + ' ';
            stack.pop();
        }
        
        len = result.length();
        if (len > 0) {
            result.erase(len - 1, 1);
        }
        
        return result;
    }
};
```
