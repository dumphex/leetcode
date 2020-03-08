# [零钱兑换](https://leetcode-cn.com/problems/coin-change/)

```
给定不同面额的硬币 coins 和一个总金额 amount。编写一个函数来计算可以凑成总金额所需的最少的硬币个数。如果没有任何一种硬币组合能组成总金额，返回 -1。

示例 1:

输入: coins = [1, 2, 5], amount = 11
输出: 3 
解释: 11 = 5 + 5 + 1
示例 2:

输入: coins = [2], amount = 3
输出: -1
说明:
你可以认为每种硬币的数量是无限的。
```

# Solution

## 直接递归(超时)

```cpp
class Solution {
public:
    int coinChange(vector<int>& coins, int amount) {
        if (amount < 0) {
            return -1;
        }

        if (amount == 0) {
            return 0;
        }

        int result = INT_MAX;
        for(auto & c : coins) {
            int ret = coinChange(coins, amount - c);
            if (ret < 0) {
                continue;
            }

            result = std::min(result, ret + 1);
        }

        return result == INT_MAX ? -1 : result;
    }
};
```


## 递归优化

```cpp
class Solution {
public:
    int coinChange(vector<int>& coins, int amount) {
        if (amount < 0) {
            return -1;
        }

        if (amount == 0) {
            return 0;
        }

        if (m_map.find(amount) != m_map.end()) {
            return m_map[amount];
        }

        int result = INT_MAX;
        for(auto & c : coins) {
            int ret = coinChange(coins, amount - c);
            if (ret < 0) {
                continue;
            }

            result = std::min(result, ret + 1);
        }

        m_map[amount] = result == INT_MAX ? -1 : result;

        return m_map[amount];
    }

private:
    std::unordered_map<int, int> m_map;
};
```

## DP

```cp
class Solution {
public:
    int coinChange(vector<int>& coins, int amount) {
        vector<int> dp(amount + 1, amount + 1);
        dp[0] = 0;
        size_t size = coins.size();
        for(size_t i = 1; i < amount + 1; i++){
            for(size_t j = 0; j < size; j++) {
                if (i >= coins[j]) {
                    dp[i] = std::min(dp[i], dp[i - coins[j]] + 1);
                }
            }
        }

        if (dp[amount] == amount + 1) {
            return -1;
        }

        return dp[amount];
    }
};
```
