# [N叉树的后序遍历](https://leetcode-cn.com/problems/n-ary-tree-postorder-traversal/)

```
给定一个 N 叉树，返回其节点值的后序遍历。

例如，给定一个 3叉树 :

 



 

返回其后序遍历: [5,6,3,2,4,1].
```

# Solution

```cpp
/*
// Definition for a Node.
class Node {
public:
    int val;
    vector<Node*> children;

    Node() {}

    Node(int _val) {
        val = _val;
    }

    Node(int _val, vector<Node*> _children) {
        val = _val;
        children = _children;
    }
};
*/
class Solution {
public:
    vector<int> postorder(Node* root) {
        vector<int> result;
        result.reserve(32);

        doPostorder(root, result);

        return result;
    }

private:
    void doPostorder(Node* root, vector<int> & result) {
        if (root == nullptr) {
            return;
        }

        // children
        for(auto & child : root->children) {
            doPostorder(child, result);
        }

        // root
        result.push_back(root->val);
    }
};
```
