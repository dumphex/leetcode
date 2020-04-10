# [排序链表](https://leetcode-cn.com/problems/sort-list/)

```
在 O(n log n) 时间复杂度和常数级空间复杂度下，对链表进行排序。

示例 1:

输入: 4->2->1->3
输出: 1->2->3->4
示例 2:

输入: -1->5->3->4->0
输出: -1->0->3->4->5
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
    ListNode* sortList(ListNode* head) {
        if (head == nullptr || head->next == nullptr) {
            return head;
        }

        ListNode *prev = nullptr;
        ListNode *slow = head;
        ListNode *fast = head;
        while(fast && fast->next) {
            prev = slow;
            slow = slow->next;
            fast = fast->next->next;
        }

        prev->next = nullptr;
        return merge(sortList(head), sortList(slow));
    }

private:
    ListNode *merge(ListNode *l1, ListNode *l2) {
        if (l1 == nullptr) {
            return l2;
        }

        if (l2 == nullptr) {
            return l1;
        }

        ListNode *p = nullptr;
        if (l1->val <= l2->val) {
            l1->next = merge(l1->next, l2);
            p = l1;
        } else {
            l2->next = merge(l1, l2->next);
            p = l2;
        }

        return p;
    }
};
```
