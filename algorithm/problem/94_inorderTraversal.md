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
        result.reserve(16);

        if (root == nullptr) {
            return result;
        }

        stack<TreeNode*> stack;
        TreeNode *p = root;

        while(p || !stack.empty()) {
            while(p) {
                stack.push(p);
                p = p->left;
            }

            p = stack.top();
            stack.pop();
            result.push_back(p->val);

            p = p->right;
        }

        return result;
    }
};
```
