# [二叉树的后序遍历](https://leetcode-cn.com/problems/binary-tree-postorder-traversal/)

```
给定一个二叉树，返回它的 后序 遍历。

示例:

输入: [1,null,2,3]  
   1
    \
     2
    /
   3 

输出: [3,2,1]
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
    vector<int> postorderTraversal(TreeNode* root) {
        vector<int> result;
        result.reserve(16);

        doPostorderTraversal(root, result);
        
        return result;
    }
private:
    void doPostorderTraversal(TreeNode* root, vector<int>& result) {
        if (root == nullptr) {
            return;
        }

        doPostorderTraversal(root->left, result);
        doPostorderTraversal(root->right, result);
        result.push_back(root->val);
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
    vector<int> postorderTraversal(TreeNode* root) {
        vector<int> result;
        if (root == nullptr) {
            return result;
        }

        result.reserve(16);
        stack<TreeNode *> stack;
        TreeNode *cur = root, *last = nullptr;

        while(cur || !stack.empty()) {
            while(cur) {
                stack.push(cur);
                cur = cur->left;
            }

            cur = stack.top();
            if (cur->right == nullptr || cur->right == last) {
                result.push_back(cur->val);
                stack.pop();
                last = cur;
                cur = nullptr;
            } else {
                cur = cur->right;
            }
        }

        return result;
    }
};
```
