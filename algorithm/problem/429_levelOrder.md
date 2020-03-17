# [N叉树的层序遍历]()

```
给定一个 N 叉树，返回其节点值的层序遍历。 (即从左到右，逐层遍历)。

例如，给定一个 3叉树 :
返回其层序遍历:

[
     [1],
     [3,2,4],
     [5,6]
]
 

说明:

树的深度不会超过 1000。
树的节点总数不会超过 5000。
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
    vector<vector<int>> levelOrder(Node* root) {
        vector<vector<int>> result;
        if (root == nullptr) {
            return result;
        }

        std::queue<Node *> queue;
        queue.push(root);
        while(!queue.empty()) {
            size_t size = queue.size();
            vector<int> cur;
            while(size--) {
                Node *p = queue.front();
                queue.pop();
                for(auto child : p->children) {
                    if (child != nullptr) {
                        queue.push(child);
                    }
                }

                cur.push_back(p->val);
            }

            result.push_back(cur);
        }

        return result;
    }
};
```
