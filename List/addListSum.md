#### addListSum
Given two linked lists, each element of the lists is a integer. Write a
function to return a new list, which is the “sum” of the given two lists.
Part a. Given input (7->1->6) + (5->9->2), output 2->1->9.

[牛客url]https://www.nowcoder.com/practice/56f8d422eae04f129c8e5a05299ae275?tpId=46&tqId=29174&tPage=1&rp=1&ru=/ta/leetcode&qru=/ta/leetcode/question-ranking

解法：前节点的解不依赖靠后节点，因此顺序遍历求解即可

```
class Solution {
public:
    ListNode *addTwoNumbers(ListNode *l1, ListNode *l2) {
        ListNode dummy(0);
        ListNode* p = &dummy;

        int cn = 0;

        while (l1 || l2) {
            int val = cn + (l1 ? l1->val : 0) + (l2 ? l2->val : 0);
            cn = val / 10;    // carry in 进位
            val = val % 10;   // sum
            p->next = new ListNode(val);
            p = p->next;
            if(l1) {
                l1 = l1->next;
            }
            if(l2) {
                l2 = l2->next;
            }
        }
        // 保存最后一个进位
        if(cn != 0) {
            p->next = new ListNode(cn);
            p = p->next;
        }

        return dummy.next;
    }
};

```
