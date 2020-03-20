# [面试题40. 最小的k个数](https://leetcode-cn.com/problems/zui-xiao-de-kge-shu-lcof/)

```
输入整数数组 arr ，找出其中最小的 k 个数。例如，输入4、5、1、6、2、7、3、8这8个数字，则最小的4个数字是1、2、3、4。

 

示例 1：

输入：arr = [3,2,1], k = 2
输出：[1,2] 或者 [2,1]
示例 2：

输入：arr = [0,1,2,1], k = 1
输出：[0]
 

限制：

0 <= k <= arr.length <= 10000
0 <= arr[i] <= 10000
通过次数30,782提交次数50,394
```

# Solution

```cpp
class Solution {
public:
    vector<int> getLeastNumbers(vector<int>& arr, int k) {
        vector<int> result;
        if (k == 0) {
            return result;
        }

        result.reserve(k);
        std::priority_queue<int> pq;
        
        for( auto & n : arr) {
            if (pq.size() < k) {
                pq.push(n);
            } else if (n < pq.top()) {
                pq.pop();
                pq.push(n);
            }
        }

        while(!pq.empty()) {
            result.push_back(pq.top());
            pq.pop();
        }

        return result;
    }
};
```
