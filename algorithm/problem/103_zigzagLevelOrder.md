# [二叉树的锯齿形层次遍历](https://leetcode-cn.com/problems/binary-tree-zigzag-level-order-traversal/)

```
给定一个二叉树，返回其节点值的锯齿形层次遍历。（即先从左往右，再从右往左进行下一层遍历，以此类推，层与层之间交替进行）。

例如：
给定二叉树 [3,9,20,null,null,15,7],

    3
   / \
  9  20
    /  \
   15   7
返回锯齿形层次遍历如下：

[
  [3],
  [20,9],
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
    vector<vector<int>> zigzagLevelOrder(TreeNode* root) {
        vector<vector<int>> result;
        if (root == nullptr) {
            return result;
        } 

        std::queue<TreeNode*> queue;
        queue.push(root);
        int level = 0;
        int size = 0;
        while(!queue.empty()) {
            level++;
            size = queue.size();
            vector<int> tmp;
            tmp.reserve(size);
            while(size--) {
                TreeNode *p = queue.front();
                queue.pop();
                tmp.push_back(p->val);
                if (p->left) {
                    queue.push(p->left);
                }

                if (p->right) {
                    queue.push(p->right);
                }
            }

            if (level % 2 == 0) {
                std::reverse(tmp.begin(), tmp.end());
            }

            result.push_back(tmp);
        }

        return result;
    }
};
```
