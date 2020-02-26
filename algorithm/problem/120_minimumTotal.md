# [三角形最小路径和](https://leetcode-cn.com/problems/triangle/)

```
给定一个三角形，找出自顶向下的最小路径和。每一步只能移动到下一行中相邻的结点上。

例如，给定三角形：

[
     [2],
    [3,4],
   [6,5,7],
  [4,1,8,3]
]
自顶向下的最小路径和为 11（即，2 + 3 + 5 + 1 = 11）。

说明：

如果你可以只使用 O(n) 的额外空间（n 为三角形的总行数）来解决这个问题，那么你的算法会很加分。
```

# Solution

## 递归
```cpp
class Solution {
public:
    int minimumTotal(vector<vector<int>>& triangle) {
        int result = doMinimumTotal(triangle, 0, 0);
        return result;
    }

private:
    int doMinimumTotal(vector<vector<int>>& triangle, int i, int j) {
        if (i == triangle.size() - 1) {
            return triangle[i][j];
        }

        int left = doMinimumTotal(triangle, i + 1, j);
        int right = doMinimumTotal(triangle, i + 1, j + 1);

        return triangle[i][j] + std::min(left, right);
    }
};
```


## 自顶向下DP

```cpp
class Solution {
public:
    int minimumTotal(vector<vector<int>>& triangle) {
        vector<vector<int>> dp(triangle);
        size_t size = triangle.size();

        for(size_t i = 1; i < size; i++) {
            size_t sub_size = triangle[i].size();

            for(size_t j = 0; j < sub_size; j++) {
                if (j == 0) {
                    dp[i][j] += dp[i - 1][j];
                } else if (j == sub_size - 1) {
                    dp[i][j] += dp[i - 1][j - 1];
                } else {
                    dp[i][j] += std::min(dp[i - 1][j], dp[i - 1][j - 1]);
                }
            }
        }

        size_t last_size = dp[size - 1].size();
        int min_sum = dp[size - 1][0];
        for (size_t i = 1; i < last_size; i++) {
            min_sum = dp[size - 1][i] < min_sum ? dp[size - 1][i] : min_sum;
        }

        return min_sum;
    }
};
```

### 自底向上DP

```cpp
class Solution {
public:
    int minimumTotal(vector<vector<int>>& triangle) {
        vector<vector<int>> dp(triangle);
        int size = triangle.size();

        for(int i = size - 2; i >= 0; i--) {
            size_t sub_size = triangle[i].size();

            for(size_t j = 0; j < sub_size; j++) {
                dp[i][j] += std::min(dp[i + 1][j], dp[i + 1][j + 1]);
            }
        }

        return dp[0][0];
    }
};
```
