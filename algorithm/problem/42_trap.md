# [接雨水](https://leetcode-cn.com/problems/trapping-rain-water/)

```
给定 n 个非负整数表示每个宽度为 1 的柱子的高度图，计算按此排列的柱子，下雨之后能接多少雨水。



上面是由数组 [0,1,0,2,1,0,1,3,2,1,2,1] 表示的高度图，在这种情况下，可以接 6 个单位的雨水（蓝色部分表示雨水）。 感谢 Marcos 贡献此图。

示例:

输入: [0,1,0,2,1,0,1,3,2,1,2,1]
输出: 6
```

# Solution

## solution1:
```cpp
class Solution {
public:
    int trap(vector<int>& height) {
        int size = height.size();
        int result = 0;
        for(int i = 0; i < size; i++) {
            int lmax = 0;
            int rmax = 0;

            for(int j = 0; j <= i; j++) {
                lmax = height[j] > lmax ? height[j] : lmax; 
            }

            for(int j = i; j < size; j++) {
                rmax = height[j] > rmax ? height[j] : rmax;
            }

            result += std::min(lmax, rmax) - height[i];
        }

        return result;
    }
};
```


## solution2:
```cpp
class Solution {
public:
    int trap(vector<int>& height) {
        int size = height.size();
        if (size == 0) {
            return 0;
        }

        vector<int> lmax(size, 0);
        lmax[0] = height[0];
        for(int i = 1; i < size; i++) {
            lmax[i] = std::max(lmax[i - 1], height[i]);
        }

        vector<int> rmax(size, 0);
        rmax[size - 1] = height[size - 1];
        for(int i = size - 2; i >= 0; i--) {
            rmax[i] = std::max(height[i], rmax[i + 1]);
        }

        int result = 0;
        for(int i = 0; i < size; i++) {
            result += std::min(lmax[i], rmax[i]) - height[i];
        }

        return result;
    }
};
```
