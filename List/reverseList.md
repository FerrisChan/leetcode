
#### Reverse a singly linked list.
[leetcode url]https://leetcode.com/problems/reverse-linked-list/description/
- 递归实现

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
    ListNode* reverseList(ListNode* head) {
        if (head == nullptr) return  head;
        if (head -> next == nullptr) return head;

        ListNode *tail= reverseList(head->next);
        head->next->next = head;  // 翻转了指针
        head ->next = nullptr;    // head指向null
        return tail;


    }
};

```

- 非递归实现：

```

class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        ListNode *prev = NULL;
        while (head != NULL) {
          /*
            重复做下面操作：
             pre -> curr(head) -> next;
                    pre <-      curr(head) -> next;
          */

          // 重新生成一个node，指针反转
             ListNode *curr = head;
             curr->next = prev;
             prev = curr;
             head = head->next;
        }
        // 最后返回最尾节点
        return prev;
    }

```
