# [N叉树的前序遍历](https://leetcode-cn.com/problems/n-ary-tree-preorder-traversal/)

```
给定一个 N 叉树，返回其节点值的前序遍历。

例如，给定一个 3叉树 :
返回其前序遍历: [1,3,5,6,2,4]。
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
    vector<int> preorder(Node* root) {
        vector<int> result;
        if (root == nullptr) {
            return result;
        }

        result.reserve(16);
        stack<Node*> stack;
        stack.push(root);
        while(!stack.empty()) {
            Node *p = stack.top();
            result.push_back(p->val);
            stack.pop();

            for(auto it = p->children.rbegin(); it != p->children.rend();it++) {
                if (*it != nullptr) {
                    stack.push(*it);
                }
            }
        }

        return result;
    }
};
```
