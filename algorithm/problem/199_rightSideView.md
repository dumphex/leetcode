# [二叉树的右视图](https://leetcode-cn.com/problems/binary-tree-right-side-view/)

```
给定一棵二叉树，想象自己站在它的右侧，按照从顶部到底部的顺序，返回从右侧所能看到的节点值。

示例:

输入: [1,2,3,null,5,null,4]
输出: [1, 3, 4]
解释:

   1            <---
 /   \
2     3         <---
 \     \
  5     4       <---
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
    vector<int> rightSideView(TreeNode* root) {
        std::vector<int> result;
        std::queue<TreeNode *> queue;
        TreeNode *p = nullptr;
        if (root != nullptr) {
            queue.push(root);
        }

        result.reserve(16);
        while(!queue.empty()) {
            size_t size = queue.size();
            while(size--) {
                p = queue.front();
                queue.pop();

                if (p->left) {
                    queue.push(p->left);
                }

                if (p->right) {
                    queue.push(p->right);
                }
            }

            result.push_back(p->val);
        }

        return result;
    }
};
```
