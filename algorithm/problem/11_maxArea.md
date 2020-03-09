# [盛最多水的容器](https://leetcode-cn.com/problems/container-with-most-water/)

```
给你 n 个非负整数 a1，a2，...，an，每个数代表坐标中的一个点 (i, ai) 。在坐标内画 n 条垂直线，垂直线 i 的两个端点分别为 (i, ai) 和 (i, 0)。找出其中的两条线，使得它们与 x 轴共同构成的容器可以容纳最多的水。

说明：你不能倾斜容器，且 n 的值至少为 2。

 



图中垂直线代表输入数组 [1,8,6,2,5,4,8,3,7]。在此情况下，容器能够容纳水（表示为蓝色部分）的最大值为 49。

 

示例：

输入：[1,8,6,2,5,4,8,3,7]
输出：49
```

# Solution

## 枚举
```cpp
class Solution {
public:
    int maxArea(vector<int>& height) {
        size_t size = height.size();

        int max = 0;
        int cur = 0;

        for(size_t i = 0; i < size; i++) {
            for(size_t j = i + 1; j < size; j++) {
                cur = (j - i) * std::min(height[i], height[j]);
                max = std::max(cur, max);
            }
        }

        return max;
    }
};
```

## 双指针
```
class Solution {
public:
    int maxArea(vector<int>& height) {
        int i = 0;
        int j = height.size() - 1;
        int max = 0;

        while(i < j) {
            max = std::max(max, (j - i) * std::min(height[i], height[j]));
            height[i] < height[j] ? i++ : j--;
        }

        return max;
    }
};
```
