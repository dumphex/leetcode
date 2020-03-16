# [相交链表](https://leetcode-cn.com/problems/intersection-of-two-linked-lists/)

```
编写一个程序，找到两个单链表相交的起始节点。
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
    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
        if (headA == nullptr || headB == nullptr) {
            return nullptr;
        }

        if (headA == headB) {
            return headA;
        }

        ListNode *p = headA;
        ListNode *q = headB;

        while(p || q) {
            p = p->next;
            q = q->next;

            if (p == nullptr && q == nullptr) {
                break;
            }

            if (p == nullptr) {
                p = headB;
            }

            if (q == nullptr) {
                q = headA;
            }

            if (p == q) {
                break;
            }
        }

        return p;
    }
};
```

优化后
```
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
    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
        if (headA == nullptr || headB == nullptr) {
            return nullptr;
        }

        ListNode *p = headA;
        ListNode *q = headB;

        while(p != q) {
            p = p == nullptr ? headB : p->next;
            q = q == nullptr ? headA : q->next;
        }

        return p;
    }
};
```
