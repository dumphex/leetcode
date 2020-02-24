# [二叉树的前序遍历](https://leetcode-cn.com/problems/binary-tree-preorder-traversal/)

```
给定一个二叉树，返回它的 前序 遍历。

 示例:

输入: [1,null,2,3]  
   1
    \
     2
    /
   3 

输出: [1,2,3]
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
    vector<int> preorderTraversal(TreeNode* root) {
        vector<int> result;

        doPreorderTraversal(root, result);

        return result;
    }

private:
    void doPreorderTraversal(TreeNode* root, vector<int> & result) {
        if (root == nullptr) {
            return;
        }

        result.push_back(root->val);
        doPreorderTraversal(root->left, result);
        doPreorderTraversal(root->right, result);
    }
};
```


## 迭代1

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
    vector<int> preorderTraversal(TreeNode* root) {
        vector<int> result;
        if (root == nullptr) {
            return result;
        }
        
        stack<TreeNode *> stack;
        result.reserve(32);
        stack.push(root);

        while(!stack.empty()) {
            TreeNode *p = stack.top();
            result.push_back(p->val);
            stack.pop();

            if (p->right) {
                stack.push(p->right);
            }

            if (p->left) {
                stack.push(p->left);
            }
        }

        return result;
    }
};
```

## 迭代2

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
    vector<int> preorderTraversal(TreeNode* root) {
        vector<int> result;
        if (root == nullptr) {
            return result;
        }

        result.reserve(16);
        stack<TreeNode *> stack;
        TreeNode* cur = root;

        while(cur || !stack.empty()) {

            while(cur) {
                result.push_back(cur->val);
                stack.push(cur);
                cur = cur->left;
            }

            cur = stack.top();
            stack.pop();
            cur = cur->right;
        }

        return result;
    }
};
```

