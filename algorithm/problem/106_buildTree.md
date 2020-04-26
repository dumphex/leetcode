# [从中序与后序遍历序列构造二叉树](https://leetcode-cn.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal/)

```
根据一棵树的中序遍历与后序遍历构造二叉树。

注意:
你可以假设树中没有重复的元素。

例如，给出

中序遍历 inorder = [9,3,15,20,7]
后序遍历 postorder = [9,15,7,20,3]
返回如下的二叉树：

    3
   / \
  9  20
    /  \
   15   7
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
    TreeNode* buildTree(vector<int>& inorder, vector<int>& postorder) {
        return doBuildTree(inorder, 0, inorder.size() - 1, postorder, 0, postorder.size() - 1);
    }

private:
    TreeNode * doBuildTree(vector<int> & inorder, int in_lo, int in_hi, vector<int> & postorder, int post_lo, int post_hi) {
        if (in_lo > in_hi || post_lo > post_hi) {
            return nullptr;
        }

        int i = in_lo;
        for(; i <= in_hi; i++) {
            if (inorder[i] == postorder[post_hi]) {
                break;
            }
        }

        int post_right_start = post_lo + i - in_lo;
        TreeNode *root = new TreeNode(postorder[post_hi]);
        root->left = doBuildTree(inorder, in_lo, i - 1, postorder, post_lo, post_right_start - 1);
        root->right = doBuildTree(inorder, i + 1, in_hi, postorder, post_right_start, post_hi - 1);
        
        return root;
    }
};
```
