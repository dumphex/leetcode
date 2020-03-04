# [将有序数组转换为二叉搜索树](https://leetcode-cn.com/problems/convert-sorted-array-to-binary-search-tree/)

```

将一个按照升序排列的有序数组，转换为一棵高度平衡二叉搜索树。

本题中，一个高度平衡二叉树是指一个二叉树每个节点 的左右两个子树的高度差的绝对值不超过 1。

示例:

给定有序数组: [-10,-3,0,5,9],

一个可能的答案是：[0,-3,9,-10,null,5]，它可以表示下面这个高度平衡二叉搜索树：

      0
     / \
   -3   9
   /   /
 -10  5
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
    TreeNode* sortedArrayToBST(vector<int>& nums) {
        return doSortedArrayToBST(nums, 0, nums.size() - 1);
    }

private:
    TreeNode* doSortedArrayToBST(vector<int>& nums, int l, int r) {
        if (l > r) {
            return nullptr;
        }

        int mid = l + (r - l + 1) / 2 ;

        TreeNode * root = new TreeNode(nums[mid]);
        root->left = doSortedArrayToBST(nums, l, mid - 1);
        root->right = doSortedArrayToBST(nums, mid + 1, r);

        return root;
    }
};
```
