# [二叉树的中序遍历](https://leetcode-cn.com/problems/binary-tree-inorder-traversal/)

```
i给定一个二叉树，返回它的中序 遍历。

示例:

输入: [1,null,2,3]
   1
    \
     2
    /
   3

输出: [1,3,2]
```

# Solution

## 递归
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
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> result;
        result.reserve(16);

        doInorderTraversal(root, result);
        return result;
    }
private:
    void doInorderTraversal(TreeNode* root, vector<int> & result) {
        if (root == nullptr) {
            return;
        }

        doInorderTraversal(root->left, result);
        result.push_back(root->val);
        doInorderTraversal(root->right, result);
    }
};
```

## 迭代
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
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> result;

        if (root == nullptr) {
            return result;
        }

        result.reserve(16);
        stack<TreeNode*> stack;
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

        return result;
    }
};
```
