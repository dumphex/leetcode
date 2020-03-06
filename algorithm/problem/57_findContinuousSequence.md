# [面试题57 - II. 和为s的连续正数序列](https://leetcode-cn.com/problems/he-wei-sde-lian-xu-zheng-shu-xu-lie-lcof/)

```
输入一个正整数 target ，输出所有和为 target 的连续正整数序列（至少含有两个数）。

序列内的数字由小到大排列，不同序列按照首个数字从小到大排列。

 

示例 1：

输入：target = 9
输出：[[2,3,4],[4,5]]
示例 2：

输入：target = 15
输出：[[1,2,3,4,5],[4,5,6],[7,8]]
 

限制：

1 <= target <= 10^5
```

# Solution

## 方案1: 暴力枚举
```cpp
class Solution {
public:
    vector<vector<int>> findContinuousSequence(int target) {
        vector<vector<int>> results;
        vector<int> v;
        v.reserve(16);

        size_t size = (target - 1) / 2;

        for(size_t i = 1; i <= size; i++) {
            int sum = 0;
            for(size_t j = i; j <= size + 1; j++) {
                sum += j;
                if (sum > target) {
                    break;
                } else if(sum == target) {
                    v.clear();
                    int idx = i;
                    while(idx <= j) {
                        v.push_back(idx);
                        idx++;
                    }

                    results.push_back(v);
                }
            }
        }

        return results;
    }
};
```


## 方案2: 滑动窗口
```
class Solution {
public:
    vector<vector<int>> findContinuousSequence(int target) {
        int size = (target - 1) / 2;
        int i = 1;
        int j = 1;
        int sum = 0;
        vector<vector<int>> results;
        vector<int> v;
        v.reserve(16);

        while(i <= size) {
            if (sum < target) {
                sum += j;
                j++;
            } else if (sum > target) {
                sum -= i;
                i++;
            } else {
                v.clear();

                for(int idx = i; idx < j; idx++) {
                    v.push_back(idx);
                }
                results.push_back(v);

                sum -= i;
                i++;
            }
        }

        return results;
    }
};
```
