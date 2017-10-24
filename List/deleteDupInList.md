#### deleteDupInList
[牛客url]
https://www.nowcoder.com/practice/fc533c45b73a41b0b44ccba763f866ef?tpId=13&tqId=11209&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking

##### 情景一
- 描述：
在一个排序的链表中，存在重复的结点，请删除该链表中重复的结点，重复的结点不保留，返回链表头指针。 例如，链表1->2->3->3->4->4->5 处理后为 1->2->5


- 代码：

```
/*
struct ListNode {
    int val;
    struct ListNode *next;
    ListNode(int x) :
        val(x), next(NULL) {
    }
};
*/
class Solution {
public:
    ListNode* deleteDuplication(ListNode* pHead)
    {
        if (!pHead) return NULL;
        // dummy node 技巧，头结点也可能删除
        ListNode *dummy = new ListNode(0);
        dummy->next = pHead;
        ListNode *node = dummy;

        while (node->next != NULL && node->next->next != NULL){
            if (node->next->val == node->next->next->val){
                // 删除值为val的多个节点
                int val_prev = node->next->val;
                while ( node->next != NULL && val_prev == node->next->val){
                    ListNode *temp = node->next;
                    node->next = node->next->next; // 删除一个节点
                    delete temp;//释放内存
                }

            } else{
                 node = node->next;
            }
        }
        return dummy->next;        
    }
};
```


##### 情景二：
- 描述：
在一个排序的链表中，存在重复的结点，请删除该链表中重复的结点，重复的结点保留，返回链表头指针。 例如，链表1->2->3->3->4->4->5 处理后为 1->2->3->4->5

- 代码类似
```
class Solution {
public:
    /**
     * @param head: The first node of linked list.
     * @return: head node
     */
    ListNode *deleteDuplicates(ListNode *head) {
        if (head == NULL) {
            return NULL;
        }
        // 头结点不删除
        ListNode *node = head;
        while (node->next != NULL) {
            if (node->val == node->next->val) {
                // 只需要删除重复的节点
                ListNode *temp = node->next;
                node->next = node->next->next;
                delete temp;
            } else {
                node = node->next;
            }
        }

        return head;
    }
};
```
