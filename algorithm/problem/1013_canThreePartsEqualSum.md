# [将数组分成和相等的三个部分](https://leetcode-cn.com/problems/partition-array-into-three-parts-with-equal-sum/)

```
给你一个整数数组 A，只有可以将其划分为三个和相等的非空部分时才返回 true，否则返回 false。

形式上，如果可以找出索引 i+1 < j 且满足 (A[0] + A[1] + ... + A[i] == A[i+1] + A[i+2] + ... + A[j-1] == A[j] + A[j-1] + ... + A[A.length - 1]) 就可以将数组三等分。

 

示例 1：

输出：[0,2,1,-6,6,-7,9,1,2,0,1]
输出：true
解释：0 + 2 + 1 = -6 + 6 - 7 + 9 + 1 = 2 + 0 + 1
示例 2：

输入：[0,2,1,-6,6,7,9,-1,2,0,1]
输出：false
示例 3：

输入：[3,3,6,5,-2,2,5,1,-9,4]
输出：true
解释：3 + 3 = 6 = 5 - 2 + 2 + 5 + 1 - 9 + 4
 

提示：

3 <= A.length <= 50000
-10^4 <= A[i] <= 10^4
```

# Solution

```cpp
class Solution {
public:
    bool canThreePartsEqualSum(vector<int>& A) {
        size_t size = A.size();
        int sum = 0;

        for(auto & n : A) {
            sum += n;
        }

        if (sum % 3 != 0) {
            return false;
        }

 
        size_t i = 0, j = 0;
        int counter = 3;
        int local_sum = sum / counter;

        while(i < size && counter--) {
            int s = A[i];
            j = i + 1;
            if (counter != 0) {
                while(j < size && s != local_sum) {
                    s += A[j++];
                }
            } else {
                while(j < size) {
                    s += A[j++];
                }

                if (s != local_sum) {
                    return false;
                }
            }

            i = j;
        }

        if (counter) {
            return false;
        }

        return true;
    }
};
```
