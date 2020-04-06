# [把二叉搜索树转换为累加树](https://leetcode-cn.com/problems/convert-bst-to-greater-tree/)

```
给定一个二叉搜索树（Binary Search Tree），把它转换成为累加树（Greater Tree)，使得每个节点的值是原来的节点值加上所有大于它的节点值之和。

 

例如：

输入: 原始二叉搜索树:
              5
            /   \
           2     13

输出: 转换为累加树:
             18
            /   \
          20     13
```

# Solution

## Solution1: 递归
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
    TreeNode* convertBST(TreeNode* root) {
        int data = 0;
        doConvertBST(root, data);
        return root;
    }

private:
    TreeNode* doConvertBST(TreeNode *root, int & data) {
        if (root == nullptr) {
            return root;
        }

        doConvertBST(root->right, data);
        root->val += data;
        data = root->val;
        doConvertBST(root->left, data);

        return root;
    }
};
```

## Solution2: 非递归
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
    TreeNode* convertBST(TreeNode* root) {
        std::stack<TreeNode *> stack;
        struct TreeNode node(0);
        TreeNode *last = &node;
        TreeNode *cur = root;

        while(cur || !stack.empty()) {
            while(cur) {
                stack.push(cur);
                cur = cur->right;
            }

            cur = stack.top();
            stack.pop();

            cur->val += last->val;
            last = cur;
            cur = cur->left;
        }

        return root;
    }
};
```
