# [回文链表](https://leetcode-cn.com/problems/palindrome-linked-list/)

```
请判断一个链表是否为回文链表。

示例 1:

输入: 1->2
输出: false
示例 2:

输入: 1->2->2->1
输出: true
```

# Solution

## 栈
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
    bool isPalindrome(ListNode* head) {
        if (head == nullptr) {
            return true;
        }

        stack<int> stack;
        ListNode *p = head;
        vector<int> ret1;
        ret1.reserve(32);
        while(p) {
            ret1.push_back(p->val);
            stack.push(p->val);
            p = p->next;
        }

        size_t size = ret1.size();
        vector<int> ret2;
        ret2.reserve(size);
        while(!stack.empty()) {
            ret2.push_back(stack.top());
            stack.pop();
        }

        for(size_t i = 0; i < size; i++) {
            if (ret1[i] != ret2[i]) {
                return false;
            }
        }

        return true;
    }
};
```


## 数组

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
    bool isPalindrome(ListNode* head) {
        if (head == nullptr) {
            return true;
        }

        vector<int> nums;
        nums.reserve(32);

        ListNode *p = head;
        while(p) {
            nums.push_back(p->val);
            p = p->next;
        }

        size_t size = nums.size();
        for(size_t i = 0, j = size - 1; i < j; i++, j--) {
            if (nums[i] != nums[j]) {
                return false;
            }
        }

        return true;
    }
};
```
