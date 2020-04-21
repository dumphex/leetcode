# [面试题33. 二叉搜索树的后序遍历序列](https://leetcode-cn.com/problems/er-cha-sou-suo-shu-de-hou-xu-bian-li-xu-lie-lcof/)

```
输入一个整数数组，判断该数组是不是某二叉搜索树的后序遍历结果。如果是则返回 true，否则返回 false。假设输入的数组的任意两个数字都互不相同。

 

参考以下这颗二叉搜索树：

     5
    / \
   2   6
  / \
 1   3
示例 1：

输入: [1,6,3,2,5]
输出: false
示例 2：

输入: [1,3,2,6,5]
输出: true
 

提示：

数组长度 <= 1000
```

# Solution

## solution1
```cpp
class Solution {
public:
    bool verifyPostorder(vector<int>& postorder) {
        if (postorder.empty()) {
            return true;
        }

        int size = postorder.size();
        int root = size - 1;

        vector<int> left;
        int i = 0;
        while (i < root && postorder[i] < postorder[root]) {
            left.push_back(postorder[i++]);
        }

        vector<int> right;
        while(i < root) {
            if (postorder[i] < postorder[root]) {
                return false;
            }
            right.push_back(postorder[i++]);
        }

        return verifyPostorder(left) && verifyPostorder(right);
    }
};
```

## solution2: 进一步优化
```cpp
class Solution {
public:
    bool verifyPostorder(vector<int>& postorder) {
        return doVerifyPostOrder(postorder, 0, postorder.size() - 1);
    }

private:
    bool doVerifyPostOrder(vector<int> & nums, int start, int end) {
        if (start >= end) {
            return true;
        }
        
        int i = start;
        for(; i <= end; i++) {
            if (nums[i] >= nums[end]) {
                break;
            }
        }

        int j = i;
        for(; j <= end; j++) {
            if (nums[j] < nums[end]) {
                return false;
            }
        }

        return doVerifyPostOrder(nums, start, i - 1) && doVerifyPostOrder(nums, i, end - 1);
    }
};
```
