# [二叉树中的最大路径和](https://leetcode-cn.com/problems/binary-tree-maximum-path-sum/)

```
给定一个非空二叉树，返回其最大路径和。

本题中，路径被定义为一条从树中任意节点出发，达到任意节点的序列。该路径至少包含一个节点，且不一定经过根节点。

示例 1:

输入: [1,2,3]

       1
      / \
     2   3

输出: 6
示例 2:

输入: [-10,9,20,null,null,15,7]

   -10
   / \
  9  20
    /  \
   15   7

输出: 42
```

# Solution

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
    int maxPathSum(TreeNode* root) {
        int max = 0x80000000;
        postorder(root, max);
        
        return max;
    }

private: 
    int postorder(TreeNode *root, int & max) {
        if (root == nullptr) {
            return 0;
        }

        int left = std::max(postorder(root->left, max), 0);
        int right = std::max(postorder(root->right, max), 0);    
        int result = std::max(root->val + left, root->val + right);

        max = std::max(root->val + left + right, max);
        
        return result;
    }
};
```
