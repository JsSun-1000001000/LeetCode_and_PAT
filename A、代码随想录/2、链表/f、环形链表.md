## [142. 环形链表 II - 力扣（LeetCode）](https://leetcode.cn/problems/linked-list-cycle-ii/description/)

随想录的方法是用快慢指针遍历，通过让快慢指针扣圈相遇的方式看环是否存在

但是我觉得最直接的方式是用哈希表，看是否能遇到之前写过的节点

先用快慢指针：
```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */

class Solution {
public:
    ListNode *detectCycle(ListNode *head) {
        ListNode* fast = head;

        ListNode* slow = head;

  
		//注意不能写反
        while( fast != NULL && fast->next != NULL ){        

            slow = slow->next;

            fast = fast->next->next;

            if(fast == slow){

                ListNode* index1 = fast;

                ListNode* index2 = head;

                while(index1 != index2){

                    index1 = index1->next;

                    index2 = index2->next;

                }

                return index1;

            }

        }

        return NULL;

    }

};
```