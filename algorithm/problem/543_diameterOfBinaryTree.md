# [二叉树的直径](https://leetcode-cn.com/problems/diameter-of-binary-tree/)

```
给定一棵二叉树，你需要计算它的直径长度。一棵二叉树的直径长度是任意两个结点路径长度中的最大值。这条路径可能穿过根结点。

示例 :
给定二叉树

          1
         / \
        2   3
       / \     
      4   5    
返回 3, 它的长度是路径 [4,2,1,3] 或者 [5,2,1,3]。

注意：两结点之间的路径长度是以它们之间边的数目表示。
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
    int diameterOfBinaryTree(TreeNode* root) {
        m_max = 0;
        preOrder(root);
        return m_max;
    }

private:
    int preOrder(TreeNode *root) {
        if (root == nullptr) {
            return 0;
        }

        int left = preOrder(root->left);
        int right = preOrder(root->right);

        m_max = std::max(left + right, m_max);
        return 1 + std::max(left, right);
    }

    int m_max;
};
```
