# [有序链表转换二叉搜索树](https://leetcode-cn.com/problems/convert-sorted-list-to-binary-search-tree/)

```
给定一个单链表，其中的元素按升序排序，将其转换为高度平衡的二叉搜索树。

本题中，一个高度平衡二叉树是指一个二叉树每个节点 的左右两个子树的高度差的绝对值不超过 1。

示例:

给定的有序链表： [-10, -3, 0, 5, 9],

一个可能的答案是：[0, -3, 9, -10, null, 5], 它可以表示下面这个高度平衡二叉搜索树：

      0
     / \
   -3   9
   /   /
 -10  5
```

# Solution

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
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
    TreeNode* sortedListToBST(ListNode* head) {
        if (head == nullptr) {
            return nullptr;
        }

        // push nodes into vector
        vector<ListNode*> nodes;
        nodes.reserve(32);
        ListNode *p = head;
        while(p) {
            nodes.push_back(p);
            p = p->next;
        }

        //recursive vector to generate AVL tree
        return genAVL(nodes, 0, nodes.size() - 1);
    }

private:
    TreeNode *genAVL(vector<ListNode*> & nodes, int lo, int hi) {
        // check
        if (lo > hi) {
            return nullptr;
        }

        int mid = lo + ((hi - lo) >> 1);
        TreeNode *root = new TreeNode(nodes[mid]->val);
        if (lo < hi) {
            root->left = genAVL(nodes, lo, mid - 1);
            root->right = genAVL(nodes, mid + 1, hi);
        }

        return root;
    }
};
```
