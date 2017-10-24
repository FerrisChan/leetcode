
#### mergeTwoSortList
Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.

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
    ListNode *mergeTwoLists(ListNode *l1, ListNode *l2) {
        // 应该先保存头结点的问题！
        ListNode *dummy = new ListNode(0);
        ListNode *List = dummy;
        while (l1 && l2){
            if (l1->val < l2->val){
                List ->next= l1;
                l1  = l1-> next;
            } else {
                List ->next = l2;
                l2 = l2 -> next ;
            }
            List = List -> next;
        }
        List->next =  (NULL != l1) ? l1 : l2;
        return dummy->next;
    }
};

```


#### 对于k个list：
- 可以循环调用上述的函数

```
ListNode *mergeKLists(vector<ListNode *> &lists) {
  if(lists.size() == 0) return NULL;
  ListNode *p = lists[0];
  for(int i =1; i< lists.size(); i++)
    {
     p = mergeTwoSortList(p, lists[i]);
    }
   return p;
}
```

- 网上看到也可以使用堆?

```
class Solution {
public:
    // comparison structure, required by priority_queue template
    struct greaterListNode{
        bool operator() (ListNode* x, ListNode* y) {return x->val > y->val;}
    };

    ListNode *mergeKLists(vector<ListNode *> &lists) {
        if(lists.size() == 0)
            return NULL;

        if(lists.size() == 1)
            return lists[0];

        ListNode* dummy = new ListNode(-1);
        ListNode* pre = dummy;
        std::priority_queue<ListNode*, vector<ListNode*>, greaterListNode> pq;

        // Insert entries of every list into heap
        for(auto& lst:lists)
            if(lst != NULL)
                pq.push(lst);

        // Recursively parse every element in lists
        while (!pq.empty()) {
            pre->next = pq.top();
            pre = pre->next;
            pq.pop();
            if (pre != NULL && pre->next != NULL)
                pq.push(pre->next);
        }

        ListNode* head = dummy->next;
        delete dummy;
        return head;
    }
};
```
