# [每日温度](https://leetcode-cn.com/problems/daily-temperatures/)

```
根据每日 气温 列表，请重新生成一个列表，对应位置的输出是需要再等待多久温度才会升高超过该日的天数。如果之后都不会升高，请在该位置用 0 来代替。

例如，给定一个列表 temperatures = [73, 74, 75, 71, 69, 72, 76, 73]，你的输出应该是 [1, 1, 4, 2, 1, 1, 0, 0]。

提示：气温 列表长度的范围是 [1, 30000]。每个气温的值的均为华氏度，都是在 [30, 100] 范围内的整数
```

# Solution

## Solution 1: 暴力
```cpp
class Solution {
public:
    vector<int> dailyTemperatures(vector<int>& T) {
        int size = T.size();
        int max = -1;
        vector<int> result(size, 0);

        for(int i = size - 1; i >=0; i--) {
            if (T[i] < max) {
                for(int j = i + 1; j < size; j++) {
                    if (T[j] > T[i]) {
                        result[i] = j - i;
                        break;
                    }
                }
            }

            max = T[i] > max ? T[i] : max;
        }

        return result;
    }
};
```


## Solution2: 栈(从后往前遍历)
```cpp
class Solution {
public:
    vector<int> dailyTemperatures(vector<int>& T) {
        int size = T.size();
        vector<int> result(size, 0);
        std::stack<int> s;

        for(int i = size - 1; i >= 0; i--) {
            while(!s.empty() && T[i] >= T[s.top()]) {
                s.pop();
            }
            result[i] = s.empty() ? 0 : s.top() - i;
            s.push(i);
        }

        return result;
    }
};
```


## Solution3: 栈(从前往后遍历)
```cpp
class Solution {
public:
    vector<int> dailyTemperatures(vector<int>& T) {
        int size = T.size();
        vector<int> result(size, 0);
        std::stack<int> s;

        for(int i = 0; i < size; i++) {
            while(!s.empty() && T[i] > T[s.top()]) {
                result[s.top()] = i - s.top();
                s.pop();
            }
            s.push(i);
        }

        return result;
    }
};
```
