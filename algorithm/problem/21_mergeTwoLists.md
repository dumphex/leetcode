# [合并两个有序链表](https://leetcode-cn.com/problems/merge-two-sorted-lists/)

```
将两个升序链表合并为一个新的升序链表并返回。新链表是通过拼接给定的两个链表的所有节点组成的。 

示例：

输入：1->2->4, 1->3->4
输出：1->1->2->3->4->4
```

# Solution

## solution1: 递归
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
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        if (l1 == nullptr) {
            return l2;
        }

        if (l2 == nullptr) {
            return l1;
        }

        ListNode *p = nullptr;
        if (l1->val <= l2->val) {
            l1->next = mergeTwoLists(l1->next, l2);
            p = l1;
        } else {
            l2->next = mergeTwoLists(l1, l2->next);
            p = l2;
        }

        return p;
    }
};
```

## solution2: 迭代
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
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        ListNode dummy(-1);
        ListNode *pn = &dummy;

        while(l1 && l2) {
            if (l1->val <= l2->val) {
                pn->next = l1;
                l1 = l1->next;
            } else {
                pn->next = l2;
                l2 = l2->next;
            }

            pn = pn->next;
        }

        pn->next = l1 == nullptr ? l2 : l1;

        return dummy.next;
    }
};
```
