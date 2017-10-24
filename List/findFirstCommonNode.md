##### findFirstCommonNode
输入两个链表，找出它们的第一个公共结点。
[牛客 url]https://www.nowcoder.com/practice/6ab1d9a29e88450685099d45c9e31e46?tpId=13&tqId=11189&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking




- 解法一(书上解法)

找出2个链表的长度，然后让长的先走两个链表的长度差，然后再一起走（因为2个链表用公共的尾部）

时间复杂度O（m+n)

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
    ListNode* FindFirstCommonNode( ListNode* pHead1, ListNode* pHead2) {
        ListNode *p1=pHead1;
        ListNode *p2=pHead2;
        int len1=0,len2=0,diff=0;
        // 求长度
        while(p1!=NULL){
            p1=p1->next;
            len1++;
        }
        while(p2!=NULL){
            p2=p2->next;
            len2++;
        }

        // 求步数差,并且把p1置为长的List头结点
        if(len1>len2){
            diff=len1-len2;
            p1=pHead1;
            p2=pHead2;
        }
        else{
            diff=len2-len1;
            p1=pHead2;
            p2=pHead1;
        }

        // 追赶指针技巧
        for(int i=0;i<diff;i++){
            p1=p1->next;
        }
        while(p1!=NULL && p2!=NULL){
            if(p1==p2)
                break;
            p1=p1->next;
            p2=p2->next;
        }
        return p1;
    }
};

```

- 解法二（leetcode 神解法）:用两个指针扫描”两个链表“，最终两个指针到达 null 或者到达公共结点。

  解释：

    假定 List1长度: a+n  List2 长度:b+n, 且 a&lt;b

    那么 p1 会先到链表尾部, 这时p2 走到 a+n位置,将p1换成List2头部

    接着p2 再走b+n-(n+a) =b-a 步到链表尾部,这时p1也走到List2的b-a位置，还差a步就到可能的第一个公共节点。

    将p2 换成 List1头部，p2走a步也到可能的第一个公共节点。如果恰好p1==p2,那么p1就是第一个公共节点。

    或者p1和p2一起走n步到达列表尾部，二者没有公共节点，退出循环。 同理a>=b.
    


```

class Solution {
public:
    ListNode* FindFirstCommonNode( ListNode* pHead1, ListNode* pHead2) {
        ListNode *p1 = pHead1;
        ListNode *p2 = pHead2;
        while(p1 != p2){
            p1 = (p1 == NULL? pHead2: p1->next);
            p2 = (p2 == NULL? pHead1: p2->next);
        }
        return p1;

    }
};
```


- 讨论上其他解法：

    设表1长度n，表2长度m，暴力法嵌套遍历两个链表需要O(mn)的时间复杂度，

    可以采用hash的思想将其中一个转存为哈希表结构，这样建哈希表时间O(m)，

    而遍历链表时间O(n)，而遍历时查找哈希表的时间为O(1)，因此复杂度降为O(m+n)，

    但需要辅助空间。（这种哈希优化的策略是种一般性的思路，谨记！）

    链接：https://www.nowcoder.com/questionTerminal/6ab1d9a29e88450685099d45c9e31e46

```
class Solution {
public:
    ListNode* FindFirstCommonNode( ListNode* pHead1, ListNode* pHead2) {
          if(pHead1==NULL||pHead2==NULL)return NULL;
          unordered_multiset<ListNode*> hashset;
          ListNode *pNode1=pHead1,*pNode2=pHead2;
          //把链表2转存为哈希表
          while(pNode2!=NULL){
              hashset.insert(pNode2);
              pNode2=pNode2->next;
          }
          //遍历第一个链表
          while(pNode1!=NULL){
            if(hashset.find(pNode1)!=hashset.end()){
                return pNode1;
            }
            pNode1=pNode1->next;
          }
          return NULL;
    }
};
```


--------------------------------------------------------------
更新：重新想一下，当链表有环的时候，上述应该是不完全对的；
先判断两个链表是否有环，如果两个都没有环，上述走法；
如果一个有环一个没环，肯定不相交；
如果两个都有环，判断一个链表上的Z点是否在另一个链表上。 // 暂时没想到，待更
