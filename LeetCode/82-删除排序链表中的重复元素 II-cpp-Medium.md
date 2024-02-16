# 82 删除排序链表中的重复元素 II

给定一个已排序的链表的头 head ， 删除原始链表中所有重复数字的节点，只留下不同的数字 。返回 已排序的链表 。

示例 1：

![82](../Src/image/LeetCode-82-1.jpg)

    输入：head = [1,2,3,3,4,4,5]
    输出：[1,2,5]

示例 2：

![82](../Src/image/LeetCode-82-2.jpg)

    输入：head = [1,1,1,2,3]
    输出：[2,3]


提示：

- 链表中节点数目在范围 `[0, 300]` 内
- `-100 <= Node.val <= 100`
- 题目数据保证链表已经按升序 **排列**

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
    ListNode* deleteDuplicates(ListNode* head) {
        ListNode* temp = new ListNode(0);
        ListNode* ans = temp;
        int val = 200;
        while(head) {
            if(head->next && head->val != head->next->val && head->val != val) {
                temp->next = new ListNode(head->val);
                temp = temp->next;
            }
            else if((!head->next) && head->val != val) {
                temp->next = new ListNode(head->val);
                temp = temp->next;
                break;
            }
            else {
                val = head->val;
            }
            head = head->next;
        }
        return ans->next;
    }
};
```
