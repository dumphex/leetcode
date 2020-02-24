# [二叉树的层次遍历](https://leetcode-cn.com/problems/binary-tree-level-order-traversal/)

```
给定一个二叉树，返回其按层次遍历的节点值。 （即逐层地，从左到右访问所有节点）。

例如:
给定二叉树: [3,9,20,null,null,15,7],

    3
   / \
  9  20
    /  \
   15   7
返回其层次遍历结果：

[
  [3],
  [9,20],
  [15,7]
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
    vector<vector<int>> levelOrder(TreeNode* root) {
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

        return result;
    }
};
```
