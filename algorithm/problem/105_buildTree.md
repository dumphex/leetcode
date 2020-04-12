# [从前序与中序遍历序列构造二叉树](https://leetcode-cn.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/)

```
根据一棵树的前序遍历与中序遍历构造二叉树。

注意:
你可以假设树中没有重复的元素。

例如，给出

前序遍历 preorder = [3,9,20,15,7]
中序遍历 inorder = [9,3,15,20,7]
返回如下的二叉树：

    3
   / \
  9  20
    /  \
   15   7
```

# Solution

## Solution1: 直接递归
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
    TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
        if (preorder.empty() || inorder.empty()) {
            return nullptr;
        }

        int size = inorder.size();
        int i = 0;
        for(i = 0; i < size; i++) {
            if (preorder[0] == inorder[i]) {
                break;
            }
        }

        TreeNode *root = new TreeNode(preorder[0]);

        vector<int> preorder_ltree;
        int preorder_left = 1;
        for(int j = 0; j < i; j++) {
            preorder_ltree.push_back(preorder[preorder_left++]);
        }

        vector<int> inorder_ltree;
        for(int j = 0; j < i; j++) {
            inorder_ltree.push_back(inorder[j]);
        }

        root->left = buildTree(preorder_ltree, inorder_ltree);

        vector<int> preorder_rtree;
        for(int j = preorder_left; j < size; j++) {
            preorder_rtree.push_back(preorder[j]);
        }

        vector<int> inorder_rtree;
        for(int j = i + 1; j < size; j++) {
            inorder_rtree.push_back(inorder[j]);
        }
        
        root->right = buildTree(preorder_rtree, inorder_rtree);

        return root;
    }
};
```


## solutoin2: 优化递归
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
    TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
        return doBuildTree(preorder, 0, preorder.size() - 1, inorder, 0, inorder.size() - 1);
    }

private: 
    TreeNode * doBuildTree(vector<int>& preorder, int pre_lo, int pre_hi, vector<int>& inorder, int in_lo, int in_hi) {
        if (pre_lo > pre_hi || in_lo > in_hi) {
            return nullptr;
        }

        // build root/left/right
        int i = in_lo;
        while(i <= in_hi && inorder[i] != preorder[pre_lo]) {
            i++;
        }

        int len = i - in_lo;
        TreeNode * root = new TreeNode(preorder[pre_lo]);
        root->left = doBuildTree(preorder, pre_lo + 1, pre_lo + len, inorder, in_lo, i - 1);
        root->right = doBuildTree(preorder, pre_lo + len + 1, pre_hi, inorder, i + 1, in_hi);

        return root;
    }
};
```
