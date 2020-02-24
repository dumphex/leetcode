# [二叉树的层次遍历 II](https://leetcode-cn.com/problems/binary-tree-level-order-traversal-ii/)

```
给定一个二叉树，返回其节点值自底向上的层次遍历。 （即按从叶子节点所在层到根节点所在的层，逐层从左向右遍历）

例如：
给定二叉树 [3,9,20,null,null,15,7],

    3
   / \
  9  20
    /  \
   15   7
返回其自底向上的层次遍历为：

[
  [15,7],
  [9,20],
  [3]
]
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
    vector<vector<int>> levelOrderBottom(TreeNode* root) {
        vector<vector<int> > result;

        if (root == nullptr) {
            return result;
        }

        queue<TreeNode *> queue;
        queue.push(root);
        vector<int> cur_level;
        cur_level.reserve(16);

        while(!queue.empty()) {
            size_t size = queue.size();
            for(size_t i = 0; i < size; i++) {
                TreeNode *p = queue.front();
                queue.pop();
                cur_level.push_back(p->val);

                if (p->left) {
                    queue.push(p->left);
                }

                if (p->right) {
                    queue.push(p->right);
                }
            }

            result.push_back(cur_level);
            cur_level.clear();
        }

        reverse(result.begin(), result.end());

        return result;
    }
};
```
