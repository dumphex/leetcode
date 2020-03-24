# [面试题 17.16. 按摩师](https://leetcode-cn.com/problems/the-masseuse-lcci/)

```
一个有名的按摩师会收到源源不断的预约请求，每个预约都可以选择接或不接。在每次预约服务之间要有休息时间，因此她不能接受相邻的预约。给定一个预约请求序列，替按摩师找到最优的预约集合（总预约时间最长），返回总的分钟数。

注意：本题相对原题稍作改动

 

示例 1：

输入： [1,2,3,1]
输出： 4
解释： 选择 1 号预约和 3 号预约，总时长 = 1 + 3 = 4。
示例 2：

输入： [2,7,9,3,1]
输出： 12
解释： 选择 1 号预约、 3 号预约和 5 号预约，总时长 = 2 + 9 + 1 = 12。
示例 3：

输入： [2,1,4,5,3,1,1,3]
输出： 12
解释： 选择 1 号预约、 3 号预约、 5 号预约和 8 号预约，总时长 = 2 + 4 + 3 + 3 = 12。
```

# Solution

## solution1: 递归剪枝
```cpp
class Solution {
public:
    int massage(vector<int>& nums) {
        m_map.clear();
        int m0 = do_massage(nums, 0);
        int m1 = do_massage(nums, 1);

        return std::max(m0, m1);
    }

private:
    int do_massage(vector<int> & nums, int idx) {
        int size = nums.size();
        if (idx >= size) {
            m_map[idx] = 0;
            return 0;
        }

        int m2 = m_map.find(idx + 2) != m_map.end() ? m_map[idx + 2] : do_massage(nums, idx + 2);
        int m3 = m_map.find(idx + 3) != m_map.end() ? m_map[idx + 3] : do_massage(nums, idx + 3);

        int m = nums[idx] + std::max(m2, m3);
        m_map[idx] = m;

        return m;
    }

    std::unordered_map<int, int> m_map;
};
```

## solution2: dp1
```cpp
class Solution {
public:
    int massage(vector<int>& nums) {
        int max = 0;
        vector<int> dp(nums);
        int size = dp.size();

        for(int i = size - 1; i >= 0; i--){
            int m2 = (i + 2) >= size ? 0 : dp[i + 2];
            int m3 = (i + 3) >= size ? 0 : dp[i + 3];
            dp[i] += std::max(m2, m3);
            max = std::max(max, dp[i]);
        }

        return max;
    }
};
```
