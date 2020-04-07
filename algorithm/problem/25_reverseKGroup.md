# [K 个一组翻转链表](https://leetcode-cn.com/problems/reverse-nodes-in-k-group/)

```
给你一个链表，每 k 个节点一组进行翻转，请你返回翻转后的链表。

k 是一个正整数，它的值小于或等于链表的长度。

如果节点总数不是 k 的整数倍，那么请将最后剩余的节点保持原有顺序。

 

示例：

给你这个链表：1->2->3->4->5

当 k = 2 时，应当返回: 2->1->4->3->5

当 k = 3 时，应当返回: 3->2->1->4->5

 

说明：

你的算法只能使用常数的额外空间。
你不能只是单纯的改变节点内部的值，而是需要实际进行节点交换。
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
    ListNode* reverseKGroup(ListNode* head, int k) {
        ListNode dummy(-1);
        dummy.next = head;
        ListNode *p = &dummy;
        ListNode *q = head;
        ListNode *q_bak = q;

        stack<ListNode *> stack;
        while(q) {
            int i = 0;
            q_bak = q;
            while(q && i++ != k) {
                stack.push(q);
                q = q->next;
            }
            
            if(i >= k) {
                while (!stack.empty()) {
                    p->next = stack.top();
                    stack.pop();
                    p = p->next;
                }
                p->next = nullptr;
            } else {
                p->next = q_bak;
            }
        }

        return dummy.next;
    }
};
```
