# [二叉树展开为链表](https://leetcode-cn.com/problems/flatten-binary-tree-to-linked-list/)

```
给定一个二叉树，原地将它展开为链表。

例如，给定二叉树

    1
   / \
  2   5
 / \   \
3   4   6
将其展开为：

1
 \
  2
   \
    3
     \
      4
       \
        5
         \
          6
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
    void flatten(TreeNode* root) {
        vector<TreeNode*> vec;
        vec.reserve(32);

        preorder(root, vec);

        TreeNode dummy(-1);
        TreeNode *p = &dummy;
        for(auto & v : vec) {
            v->left = nullptr;
            p->right = v;
            p = p->right;
        }
    }
    
private:
    void preorder(TreeNode * root, vector<TreeNode*> & vec) {
        if (root == nullptr) {
            return;
        }

        vec.push_back(root);
        preorder(root->left, vec);
        preorder(root->right, vec);
    }
};
```
