#### 剑指offer题目6：
输入一个链表，从尾到头打印链表每个节点的值
[]https://www.nowcoder.com/practice/d0267f7f55b3412ba93bd35cfa8e8035?tpId=13&tqId=11156&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking

- 使用栈：

```
/**
*  struct ListNode {
*        int val;
*        struct ListNode *next;
*        ListNode(int x) :
*              val(x), next(NULL) {
*        }
*  };
*/
class Solution {
public:
    vector<int> printListFromTailToHead(ListNode* head) {

        std::stack<int> ans;
        std::vector<int> vec;

        while (head){
            int temp = head->val;
            ans.push(temp);
            head = head->next;
        }

        while(!ans.empty()){
            int t = ans.top();
            vec.push_back(t);
            ans.pop();

        }

        return vec;
    }

}

```

- 递归调用：
```
void PrintListReversingly_Recursively(ListNode* pHead)
{
    if(pHead != nullptr)
    {
        if (pHead->m_pNext != nullptr)
        {
            PrintListReversingly_Recursively(pHead->m_pNext);
        }

        printf("%d\t", pHead->m_nValue);
    }
}
```
