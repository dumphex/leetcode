# [x 的平方根](https://leetcode-cn.com/problems/sqrtx/)

```
实现 int sqrt(int x) 函数。

计算并返回 x 的平方根，其中 x 是非负整数。

由于返回类型是整数，结果只保留整数的部分，小数部分将被舍去。

示例 1:

输入: 4
输出: 2
示例 2:

输入: 8
输出: 2
说明: 8 的平方根是 2.82842..., 
     由于返回类型是整数，小数部分将被舍去。
```

# Solution

```cpp
class Solution {
public:
    int mySqrt(int x) {
        if (x == 0 || x== 1) {
            return x;
        }

        bool negative = false;
        long long num = x;
        if (num < 0) {
            negative = true;
            num *= -1;
        }

        long long result = do_sqrt(num);
        return negative ? (-1) *result : result;
    }

private:
    long long do_sqrt(long long num) {
        long long lo = 1;
        long long hi = num / 2;

        while(lo <= hi) {
            long long mid = lo + (hi - lo) / 2;
            long long product = mid * mid;

            if (product == num) {
                return mid;
            } else if (product < num) {
                lo = mid + 1;
            } else {
                hi = mid - 1;
            }
        }

        return hi;
    }
};
```
