# [面试题54. 二叉搜索树的第k大节点](https://leetcode-cn.com/problems/er-cha-sou-suo-shu-de-di-kda-jie-dian-lcof/)

```
给定一棵二叉搜索树，请找出其中第k大的节点。

 

示例 1:

输入: root = [3,1,4,null,2], k = 1
   3
  / \
 1   4
  \
   2
输出: 4
示例 2:

输入: root = [5,3,6,2,4,null,null,1], k = 3
       5
      / \
     3   6
    / \
   2   4
  /
 1
输出: 4
 

限制：

1 ≤ k ≤ 二叉搜索树元素个数
```

# Solution

## Solution1: 从小到大排序(正规非递归中序遍历)
```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    int kthLargest(TreeNode* root, int k) {
        std::vector<int> result;
        result.reserve(32);
        std::stack<TreeNode *> stack;
        TreeNode *cur = root;

        while(cur || !stack.empty()) {
            while(cur) {
                stack.push(cur);
                cur = cur->left;
            }

            cur = stack.top();
            stack.pop();
            result.push_back(cur->val);
            cur = cur->right;
        }

        return result[result.size() - k];
    }
};
```


## Solution2: 从大到小排序(右子树->根结点->左子树)
```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    int kthLargest(TreeNode* root, int k) {
        std::stack<TreeNode *> stack;
        TreeNode *cur = root;

        while(cur || !stack.empty()) {
            while(cur) {
                stack.push(cur);
                cur = cur->right;
            }

            cur = stack.top();
            stack.pop();
            if (--k == 0) {
                break;
            }
            cur = cur->left;
        }

        return cur->val;
    }
};
```
