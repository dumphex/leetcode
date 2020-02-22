# [路径总和 II](https://leetcode-cn.com/problems/path-sum-ii/)

```
i给定一个二叉树和一个目标和，找到所有从根节点到叶子节点路径总和等于给定目标和的路径。

说明: 叶子节点是指没有子节点的节点。

示例:
给定如下二叉树，以及目标和 sum = 22，

              5
             / \
            4   8
           /   / \
          11  13  4
         /  \    / \
        7    2  5   1
返回:

[
   [5,4,11,2],
   [5,8,4,5]
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
    vector<vector<int>> pathSum(TreeNode* root, int sum) {
        vector<vector<int>> result;
        vector<int> record;
        doPathSum(root, sum, result, record);

        return result;
    }

private:
    void doPathSum(TreeNode* root, int sum, vector<vector<int>> &result, vector<int> record) {
        if (root == nullptr) {
            return;
        }

        record.push_back(root->val);
        
        int diff = sum - root->val;
        if (diff == 0 && root->left == nullptr && root->right == nullptr) {
            result.push_back(record);
            return;
        }

        doPathSum(root->left, diff, result, record);        
        doPathSum(root->right, diff,result, record);
    }
};
```
