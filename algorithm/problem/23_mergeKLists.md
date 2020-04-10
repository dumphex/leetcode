# [合并K个排序链表](https://leetcode-cn.com/problems/merge-k-sorted-lists/)

```
合并 k 个排序链表，返回合并后的排序链表。请分析和描述算法的复杂度。

示例:

输入:
[
  1->4->5,
  1->3->4,
  2->6
]
输出: 1->1->2->3->4->4->5->6
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
class Solution {
public:
    struct mycompare {
        bool operator()(ListNode* p, ListNode * q) {
            return p->val >= q->val ? true : false;
        }
    };

    ListNode* mergeKLists(vector<ListNode*>& lists) {
        std::priority_queue<ListNode *, std::vector<ListNode *>, mycompare> pq;
        for(auto p : lists) {
            while(p) {
                pq.push(p);
                p = p->next;
            }
        }

        ListNode dummy(-1);
        ListNode *p = &dummy;
        while(!pq.empty()) {
            p->next = pq.top();
            pq.pop();
            p = p->next;
        }
        
        p->next = nullptr;
        return dummy.next;
    }
};
```
