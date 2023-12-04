# 19 删除链表的倒数第 N 个结点

给你一个链表，删除链表的倒数第 `n` 个结点，并且返回链表的头结点。

![LeetCode-19-1](../Src/image/LeetCode-19-1.jpg)

示例 1：


    输入：head = [1,2,3,4,5], n = 2
    输出：[1,2,3,5]

示例 2：

    输入：head = [1], n = 1
    输出：[]

示例 3：

    输入：head = [1,2], n = 1
    输出：[1]
 

提示：

- 链表中结点的数目为 `sz`
- `1 <= sz <= 30`
- `0 <= Node.val <= 100`
- `1 <= n <= sz`
 

**进阶**：你能尝试使用一趟扫描实现吗？

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        int size = 0;
        if(head) size++;
        else return head;
        ListNode* p = head;
        while(p->next)
        {
            size++;
            p = p->next;
        }
        int m = size - n + 1;
        if(m == 1) return head->next;
        if(m <= 0) return head;
        p = head;
        for(int i = 2; i < m; i++)
        {
            p = p->next;
        }
        p->next = p->next->next;
        return head;
    }
};
```
