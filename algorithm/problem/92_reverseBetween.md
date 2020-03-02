# [反转链表 II](https://leetcode-cn.com/problems/reverse-linked-list-ii/)

```
反转从位置 m 到 n 的链表。请使用一趟扫描完成反转。

说明:
1 ≤ m ≤ n ≤ 链表长度。

示例:

输入: 1->2->3->4->5->NULL, m = 2, n = 4
输出: 1->4->3->2->5->NULL
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
    ListNode* reverseBetween(ListNode* head, int m, int n) {
        if (head == nullptr) { 
            return nullptr;
        }

        ListNode dummy(-1);
        dummy.next = head;

        ListNode *pre = &dummy;
        for(int i = 0; i < m - 1; i++) {
            pre = pre->next;
        }

        ListNode *p = pre->next, *next = nullptr;

        ListNode reverse_node(-1);
        ListNode *q = reverse_node.next;
        for(int i = m; i <= n; i++){
            next = p->next;
            p->next = q;
            reverse_node.next = p;
            q = p;

            p = next;
        }

        q = reverse_node.next;
        while (q->next != nullptr) {
            q = q->next;
        }

        q->next = next;
        pre->next = reverse_node.next;

        return dummy.next;
    }
};
```

## solution2: stack
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
    ListNode* reverseBetween(ListNode* head, int m, int n) {
        if (head == nullptr) {
            return nullptr;
        }

        ListNode dummy(-1);
        dummy.next = head;
        ListNode *pre = &dummy;

        std::stack<ListNode *> stack;
        for(int i = 1; i < m; i++) {
            pre = pre->next;
        }

        ListNode *p = pre->next;
        for(int i = m; i <= n; i++) {
            stack.push(p);
            p = p->next;
        }

        while(!stack.empty()) {
            pre->next = stack.top();
            stack.pop();
            pre = pre->next;
        }

        pre->next = p;
        
        return dummy.next;
    }
};
```
