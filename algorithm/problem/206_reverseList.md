# [反转链表](https://leetcode-cn.com/problems/reverse-linked-list/)

```
反转一个单链表。

示例:

输入: 1->2->3->4->5->NULL
输出: 5->4->3->2->1->NULL
进阶:
你可以迭代或递归地反转链表。你能否用两种方法解决这道题？
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
    ListNode* reverseList(ListNode* head) {
        if (head == nullptr) {
            return head;
        }

        ListNode *p = head;
        ListNode dummy(-1);
        ListNode *q = dummy.next;

        while(p) {
            head = head->next;
            p->next = q;
            dummy.next = p;
            q = p;
            p = head;
        }

        return dummy.next;
    }
};
```
